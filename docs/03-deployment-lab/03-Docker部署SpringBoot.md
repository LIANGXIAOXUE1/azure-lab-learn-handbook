# 03-Docker部署SpringBoot

## 实验目标

将 Spring Boot 项目打包为 Jar，通过 Docker 打包为镜像（Image），运行容器（Container），并在本机访问接口。

---

# 一、准备工作

## Spring Boot 项目

示例接口：

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello Azure!";
    }

}
```

---

## 打包 Jar

生成：

```text
target/demo-0.0.1-SNAPSHOT.jar
```

最终目录：

```text
target
└── demo-0.0.1-SNAPSHOT.jar
```

---

# 二、检查 Docker 环境

验证 Docker 是否启动：

```cmd
docker ps
```

正常输出：

```text
CONTAINER ID   IMAGE   COMMAND   CREATED   STATUS   PORTS   NAMES
```

---

## 测试 Docker Hub 联通性

执行：

```cmd
docker pull hello-world
```

成功输出：

```text
Status: Image is up to date for hello-world:latest
```

说明：

```text
Docker正常

Docker Hub可访问

可以下载镜像
```

---

# 三、创建 Dockerfile

项目根目录：

```text
D:\github\Azure部署
```

创建：

```text
Dockerfile
```

注意：

```text
没有后缀

不是 Dockerfile.txt
```

---

## Dockerfile内容

```dockerfile
FROM eclipse-temurin:17-jre

COPY target/demo-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java","-jar","/app.jar"]
```

---

# 四、理解 Dockerfile

## 指定基础镜像

```dockerfile
FROM eclipse-temurin:17-jre
```

表示：

```text
使用 Java17 运行环境
```

---

## 复制 Jar

```dockerfile
COPY target/demo-0.0.1-SNAPSHOT.jar app.jar
```

表示：

```text
将本地 Jar

复制到容器内

命名为 app.jar
```

---

## 开放端口

```dockerfile
EXPOSE 8080
```

表示：

```text
应用运行在 8080
```

---

## 启动命令

```dockerfile
ENTRYPOINT ["java","-jar","/app.jar"]
```

表示：

```text
容器启动后自动执行

java -jar app.jar
```

---

# 五、构建镜像

在项目目录执行：

```cmd
docker build --no-cache -t springboot-demo:v1 .
```

参数说明：

```text
springboot-demo
镜像名称

v1
镜像版本

.
当前目录
```

---

## 构建成功

输出类似：

```text
Successfully tagged springboot-demo:v1
```

---

# 六、查看镜像

执行：

```cmd
docker images
```

查看：

```text
springboot-demo    v1
```

说明镜像创建成功。

---

# 七、启动容器

执行：

```cmd
docker run -d -p 8080:8080 --name springboot-demo springboot-demo:v1
```

---

## 参数解释

容器名称：

```text
springboot-demo
```

镜像：

```text
springboot-demo:v1
```

端口映射：

```text
-p 8080:8080
```

表示：

```text
本机8080

映射到

容器8080
```

---

# 八、查看容器

执行：

```cmd
docker ps
```

输出：

```text
CONTAINER ID
IMAGE
springboot-demo:v1

STATUS
Up

PORTS
0.0.0.0:8080->8080/tcp
```

说明容器运行成功。

---

# 九、查看日志

执行：

```cmd
docker logs springboot-demo
```

成功日志：

```text
Tomcat started on port(s): 8080

Started DemoApplication
```

说明 Spring Boot 启动成功。

---

# 十、访问项目

由于代码：

```java
@GetMapping("/hello")
```

浏览器访问：

```text
http://localhost:8080/hello
```

返回：

```text
Hello Azure!
```

说明部署成功。

---

# 常用 Docker 命令

## 查看镜像

```cmd
docker images
```

---

## 查看运行中的容器

```cmd
docker ps
```

---

## 查看日志

```cmd
docker logs springboot-demo
```

---

## 停止容器

```cmd
docker stop springboot-demo
```

---

## 删除容器

```cmd
docker rm springboot-demo
```

---

## 删除镜像

```cmd
docker rmi springboot-demo:v1
```

---

# 本次实验踩过的坑

## Dockerfile写成Dockerfile.txt

错误：

```text
Dockerfile.txt
```

正确：

```text
Dockerfile
```

---

## Docker Hub访问超时

错误：

```text
TLS handshake timeout
```

解决：

```text
配置 Docker 镜像加速器
```

---

## Jar被误删

错误：

```text
target/demo-0.0.1-SNAPSHOT.jar
不存在
```

解决：

```text
重新生成 Jar
```

---

## Docker COPY失败

错误：

```text
COPY target/demo.jar app.jar
```

原因：

```text
Jar文件不存在
```

解决：

```text
重新打包
```

---

# 与前面实验的区别

## Azure VM

```text
Spring Boot
↓
Jar
↓
上传服务器
↓
安装Java
↓
java -jar
```

---

## App Service

```text
Spring Boot
↓
Jar
↓
上传到App Service
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

# 本次实验收获

掌握：

✅ Docker Desktop

✅ Dockerfile

✅ Docker Hub

✅ Docker Image

✅ Docker Container

✅ 端口映射

✅ Spring Boot容器化

✅ docker build

✅ docker run

✅ docker logs

---

# 下一步学习

```text
01-AzureVM部署SpringBoot ✅

02-AppService部署SpringBoot ✅

03-Docker部署SpringBoot ✅

04-ContainerApps部署SpringBoot

05-AKS部署SpringBoot
```

---

# 实验总结

Docker 的核心思想是：

```text
把应用和运行环境一起打包
```

传统部署：

```text
服务器
+
Java
+
Jar
```

Docker部署：

```text
Image
+
Container
```

实现：

```text
一次构建

到处运行
```

这也是 Azure Container Apps、AKS、Kubernetes 等容器平台的基础。
