# 04-ContainerApps部署SpringBoot

## 实验目标

将本地 Spring Boot 项目容器化后，上传到 Azure Container Registry（ACR），再通过 Azure Container Apps 运行容器，并通过公网访问接口。

这是第一次接触 Azure 云原生部署。

---

# 一、实验原理

在前面实验中：

## Azure VM

```text
Spring Boot
↓
Jar
↓
Linux VM
↓
安装Java
↓
运行
```

---

## App Service

```text
Spring Boot
↓
Jar
↓
上传
↓
Azure运行
```

---

## Docker

```text
Spring Boot
↓
Jar
↓
Dockerfile
↓
Image
↓
Container
```

---

## Container Apps

```text
Spring Boot
↓
Jar
↓
Docker Image
↓
ACR
↓
Container Apps
↓
公网访问
```

---

# 二、准备工作

## 已完成 Docker 实验

本地已经存在镜像：

```text
springboot-demo:v1
```

查看：

```cmd
docker images
```

输出：

```text
springboot-demo:v1
```

说明镜像准备完成。

---

# 三、创建 Azure Container Registry（ACR）

Azure Portal：

```text
Container Registries
↓
Create
```

---

## 配置

```text
Registry Name
xiaoxueacr001

Region
Central US

SKU
Basic

Resource Group
rg0721
```

---

## 创建完成

进入：

```text
ACR
↓
Overview
```

获取：

```text
Login Server
```

例如：

```text
xiaoxueacr001.azurecr.io
```

---

# 四、上传镜像到 ACR

这一部分非常重要。

Container Apps 不能直接访问本地镜像。

必须先上传 Azure 镜像仓库。

---

## 1. 开启管理员账号

进入：

```text
ACR
↓
Access Keys
```

开启：

```text
Admin User
```

获得：

```text
Username

Password1
```

---

## 2. 登录 ACR

执行：

```cmd
docker login xiaoxueacr001.azurecr.io
```

输入：

```text
Username

Password
```

成功输出：

```text
Login Succeeded
```

---

## 3. 给镜像重新打标签

本地镜像：

```text
springboot-demo:v1
```

执行：

```cmd
docker tag springboot-demo:v1 xiaoxueacr001.azurecr.io/springboot-demo:v1
```

---

## 4. 上传镜像

执行：

```cmd
docker push xiaoxueacr001.azurecr.io/springboot-demo:v1
```

上传后：

```text
Pushed
```

---

## 5. 验证镜像

ACR：

```text
Repositories
```

看到：

```text
springboot-demo
```

说明：

```text
本地Docker
↓
ACR
```

链路成功。

---

# 五、创建 Container Apps

进入 Azure：

```text
Container Apps
↓
Create
```

注意：

```text
不要选
Container Instances
```

正确的是：

```text
Container Apps
```

---

# 六、基本配置

填写：

```text
Name
springboot-ca

Resource Group
rg0721

Region
Central US
```

---

## 创建 Container Apps Environment

选择：

```text
Create New Environment
```

Azure 自动创建：

```text
Managed Environment
```

---

# 七、配置镜像

Container 页面：

```text
Image Source
Azure Container Registry
```

---

选择：

```text
Registry
xiaoxueacr001
```

---

Repository：

```text
springboot-demo
```

---

Tag：

```text
v1
```

---

资源配置：

```text
CPU
0.5

Memory
1Gi
```

---

# 八、配置公网访问

Ingress：

```text
Enable Ingress
✅
```

---

设置：

```text
Accept traffic from anywhere
```

---

Target Port：

```text
8080
```

非常重要！

因为：

```java
Spring Boot
默认监听8080
```

如果填错：

```text
80

443

3000
```

会导致访问失败。

---

# 九、创建失败问题

第一次创建失败。

报错：

```text
Authorization failed

roleAssignments/write
```

原因：

```text
当前账号没有Owner权限
```

Container Apps 无法自动创建：

```text
AcrPull
```

权限。

---

## 解决方案

获得：

```text
Owner
```

角色。

然后重新创建。

---

## 第二次创建成功

状态：

```text
springboot-ca
OK

AcrPullRoleAssignment
OK

managedEnvironment
OK
```

说明：

```text
Container Apps 已成功连接 ACR
```

---

# 十、获取公网地址

进入：

```text
springboot-ca
↓
Overview
```

找到：

```text
Application URL
```

类似：

```text
https://springboot-ca.xxxxx.azurecontainerapps.io
```

---

# 十一、访问接口

代码：

```java
@GetMapping("/hello")
```

访问：

```text
https://springboot-ca.xxxxx.azurecontainerapps.io/hello
```

返回：

```text
Hello Azure!
```

部署成功。

---

# 整体流程图

```text
Spring Boot
↓
Jar

demo-0.0.1-SNAPSHOT.jar
↓
Dockerfile
↓
docker build
↓
springboot-demo:v1
↓
docker push
↓
ACR
xiaoxueacr001
↓
Container Apps
springboot-ca
↓
公网域名
↓
Hello Azure!
```

---

# 本次实验收获

掌握：

✅ Azure Container Registry（ACR）

✅ Docker Image Push

✅ Container Apps

✅ Managed Environment

✅ Ingress

✅ Target Port

✅ AcrPull权限

✅ 云原生容器部署

---

# 与前面实验对比

## VM

```text
Jar
↓
Linux
↓
Java
↓
运行
```

---

## App Service

```text
Jar
↓
上传
↓
运行
```

---

## Docker

```text
Jar
↓
Image
↓
Container
```

---

## Container Apps

```text
Jar
↓
Image
↓
ACR
↓
Container Apps
↓
公网访问
```

---

# 学习路线进度

```text
01-AzureVM部署SpringBoot ✅

02-AppService部署SpringBoot ✅

03-Docker部署SpringBoot ✅

04-ContainerApps部署SpringBoot ✅

05-AKS部署SpringBoot（下一步）
```

---

# 实验总结

Container Apps 可以理解为：

```text
Docker
+
Azure托管
```

开发者无需管理：

```text
VM

Linux

Kubernetes
```

只需：

```text
Docker镜像
↓
上传ACR
↓
创建Container Apps
```

即可完成云原生应用发布。

这也是目前很多 AI 应用、Agent 项目、RAG 项目和中小型微服务项目最常见的部署模式。
``
