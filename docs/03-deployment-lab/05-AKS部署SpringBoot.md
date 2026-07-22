# 05-AKS部署SpringBoot

## 实验目标

将已经上传到 Azure Container Registry（ACR）的 Spring Boot Docker 镜像部署到 Azure Kubernetes Service（AKS），通过 Kubernetes Deployment 和 Service 暴露公网访问。

---

# 一、实验架构

本次实验完整链路：

```text
Spring Boot
↓
Jar
↓
Dockerfile
↓
Docker Image
↓
ACR
↓
AKS
↓
Deployment
↓
Pod
↓
Service
↓
LoadBalancer
↓
公网IP
↓
Hello Azure!
```

---

# 二、知识点理解

## Node

Node 可以理解为：

```text
Azure VM
```

AKS 底层仍然是虚拟机。

---

## Node Pool

Node Pool 可以理解为：

```text
VM组
```

例如：

```text
System Pool
User Pool
Spot Pool
```

---

## Pod

Pod 是 Kubernetes 最小运行单元。

可以简单理解：

```text
Pod ≈ Docker Container
```

本次运行：

```text
springboot-demo
```

实际上是运行在：

```text
Pod
```

里面。

---

## Deployment

Deployment 负责：

```text
创建Pod

管理Pod

自动恢复Pod

扩缩容Pod
```

可以理解为：

```text
Pod管理员
```

---

## Service

Service 提供：

```text
稳定访问入口
```

否则：

```text
Pod重建后IP变化
```

无法访问。

---

# 三、创建 AKS

Azure Portal：

```text
Kubernetes Services
↓
Create
```

---

## 配置

```text
Cluster Name
aks-xiaoxue-demo

Resource Group
rg0721

Location
West US 2
```

---

## Node Pool

实验环境配置：

```text
System Pool

Node Count
2

VM Size
Standard_D2ls_v5
```

---

# 四、踩坑记录1

创建 AKS 时：

```text
AvailabilityZoneNotSupported
```

报错：

```text
The zone(s) '1' for resource 'userpool' is not supported
```

---

## 原因

当前区域：

```text
West US 2
```

不支持配置：

```text
Zone 1
```

---

## 解决

修改：

```text
Availability Zone
```

为：

```text
None
```

或者：

```text
无
```

重新创建成功。

---

# 五、连接 AKS

打开：

```text
Cloud Shell
```

执行：

```powershell
az account set --subscription e13cf7e0-12f7-4f05-b0e3-9c35b198d4fe
```

---

获取集群凭证：

```powershell
az aks get-credentials `
--resource-group rg0721 `
--name aks-xiaoxue-demo `
--overwrite-existing
```

成功：

```text
Merged "aks-xiaoxue-demo"
```

---

# 六、验证连接

执行：

```powershell
kubectl get deployments --all-namespaces=true
```

看到：

```text
coredns

metrics-server

azure-policy
```

说明：

```text
成功连接 AKS
```

---

# 七、创建 Deployment

创建：

```text
deployment.yaml
```

内容：

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: springboot-demo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: springboot-demo
  template:
    metadata:
      labels:
        app: springboot-demo
    spec:
      containers:
      - name: springboot-demo
        image: xiaoxueacr001.azurecr.io/springboot-demo:v1
        ports:
        - containerPort: 8080
```

---

部署：

```powershell
kubectl apply -f deployment.yaml
```

结果：

```text
deployment.apps/springboot-demo created
```

---

# 八、踩坑记录2

第一次查看 Pod：

```powershell
kubectl get pods
```

结果：

```text
ErrImagePull
```

---

继续查看：

```powershell
kubectl describe pod springboot-demo-xxxxx
```

发现：

```text
401 Unauthorized
```

以及：

```text
ImagePullBackOff
```

---

## 原因

AKS 无权限访问：

```text
ACR
```

即：

```text
xiaoxueacr001.azurecr.io
```

---

# 九、解决 ACR 权限

执行：

```powershell
az aks update `
--resource-group rg0721 `
--name aks-xiaoxue-demo `
--attach-acr xiaoxueacr001
```

为 AKS 添加：

```text
AcrPull
```

权限。

---

## 验证

执行：

```powershell
az role assignment list `
--scope $(az acr show -n xiaoxueacr001 --query id -o tsv) `
-o table
```

看到：

```text
AcrPull
```

说明绑定成功。

---

# 十、重新创建 Pod

删除失败 Pod：

```powershell
kubectl delete pod springboot-demo-65875c5587-v94wp
```

---

Deployment 自动创建新 Pod：

```powershell
kubectl get pods -w
```

结果：

```text
springboot-demo-65875c5587-hxmks

1/1 Running
```

---

## 重要理解

删除 Pod 后：

```text
Deployment
```

会自动：

```text
创建新的 Pod
```

这正是 Deployment 的作用。

---

# 十一、创建 Service

创建：

```text
service.yaml
```

内容：

```yaml
apiVersion: v1
kind: Service
metadata:
  name: springboot-service
spec:
  selector:
    app: springboot-demo
  ports:
  - port: 80
    targetPort: 8080
  type: LoadBalancer
```

---

部署：

```powershell
kubectl apply -f service.yaml
```

结果：

```text
service/springboot-service created
```

---

# 十二、获取公网IP

执行：

```powershell
kubectl get svc
```

第一次：

```text
EXTERNAL-IP

<pending>
```

---

等待几十秒：

```powershell
kubectl get svc
```

结果：

```text
NAME                 TYPE            EXTERNAL-IP

springboot-service   LoadBalancer    4.242.76.73
```

说明：

```text
Azure Load Balancer
```

创建成功。

---

# 十三、访问应用

访问：

```text
http://4.242.76.73/hello
```

返回：

```text
Hello Azure!
```

部署成功。

---

# 本次实验踩坑总结

## 坑1：Availability Zone 不支持

报错：

```text
AvailabilityZoneNotSupported
```

解决：

```text
关闭 Zone 配置
```

---

## 坑2：PowerShell 与 Bash 不兼容

执行：

```bash
cat > deployment.yaml <<EOF
```

失败。

原因：

```text
Cloud Shell 使用 PowerShell
```

不是 Bash。

解决：

```text
nano deployment.yaml
```

手工创建文件。

---

## 坑3：ImagePullBackOff

现象：

```text
Pod无法启动
```

原因：

```text
AKS无法访问ACR
```

解决：

```powershell
az aks update --attach-acr
```

---

## 坑4：Pod重建

权限修复后：

```text
旧Pod不会自动恢复
```

解决：

```powershell
kubectl delete pod
```

Deployment 自动创建新 Pod。

---

# 整体流程图

```text
Spring Boot
↓
Jar
↓
Dockerfile
↓
Docker Build
↓
springboot-demo:v1
↓
Push
↓
ACR
xiaoxueacr001
↓
AKS
aks-xiaoxue-demo
↓
Deployment
↓
Pod
↓
Service
↓
LoadBalancer
↓
公网IP
4.242.76.73
↓
Hello Azure!
```

---

# 实验收获

掌握：

✅ AKS

✅ Kubernetes

✅ Node

✅ Node Pool

✅ Deployment

✅ Pod

✅ Service

✅ LoadBalancer

✅ ACR 权限绑定

✅ kubectl

✅ ImagePullBackOff 排障

✅ Pod 生命周期

✅ Kubernetes YAML

---

# 学习路线进度

```text
01 Azure VM部署SpringBoot ✅

02 App Service部署SpringBoot ✅

03 Docker部署SpringBoot ✅

04 ContainerApps部署SpringBoot ✅

05 AKS部署SpringBoot ✅
```

---

# 实验总结

AKS 是 Azure 提供的 Kubernetes 服务。

相比 Container Apps：

```text
Container Apps
=
简单部署
```

AKS：

```text
AKS
=
企业级容器编排平台
```

可以支持：

```text
微服务

自动扩缩容

Ingress

CI/CD

AI服务

大规模生产环境
```

本实验成功完成 Spring Boot 在 AKS 上的完整部署，并掌握了 Kubernetes 基础资源对象及常见故障排查方法。
