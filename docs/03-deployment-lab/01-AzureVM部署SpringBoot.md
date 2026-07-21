# 01-AzureVM部署SpringBoot

## 实验目标

将本地 Spring Boot 项目打包为 Jar，并部署到 Azure Linux 虚拟机（VM）上，通过公网 IP 成功访问接口。

---

# 一、准备工作

## 1. Spring Boot 项目

确保项目能够正常运行。

示例：

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

## 2. 打包 Jar

项目根目录执行：

```bash
mvn clean package
```

生成：

```text
target/demo-0.0.1-SNAPSHOT.jar
```

---

# 二、创建 Azure VM

进入 Azure Portal：

```text
Virtual Machines
↓
Create
↓
Azure Virtual Machine
```

配置：

```text
资源组：
新建或选择已有资源组

区域：
Central US（可选）

镜像：
Ubuntu Server 24.04 LTS

认证类型：
SSH Public Key

用户名：
azureuser
```

创建完成后等待部署成功。

---

# 三、获取公网 IP

方式一：

```text
VM
↓
Overview（概述）
↓
Public IP Address
```

方式二：

```text
VM
↓
Networking（网络）
↓
Public IP
```

例如：

```text
20.80.73.227
```

---

# 四、使用 SSH 登录 VM

## 1. 下载 SSH Key

创建 VM 时 Azure 会自动下载：

```text
vm1001_key.pem
```

例如：

```text
D:\vm1001_key.pem
```

---

## 2. 修复 PEM 权限

Windows 默认权限过高。

管理员 PowerShell：

```powershell
icacls "D:\vm1001_key.pem" /inheritance:r

icacls "D:\vm1001_key.pem" /remove "Users"

icacls "D:\vm1001_key.pem" /grant:r Administrator:F
```

验证：

```powershell
icacls "D:\vm1001_key.pem"
```

---

## 3. SSH 登录

```powershell
ssh -i "D:\vm1001_key.pem" azureuser@20.80.73.227
```

成功后进入：

```bash
azureuser@vm1001:~$
```

---

# 五、安装 Java

更新软件源：

```bash
sudo apt update
```

安装 Java 17：

```bash
sudo apt install openjdk-17-jdk -y
```

验证：

```bash
java -version
```

输出类似：

```text
openjdk version "17.x.x"
```

说明安装成功。

---

# 六、上传 Jar

本地执行：

```powershell
scp -i "D:\vm1001_key.pem" "D:\github\Azure部署\target\demo-0.0.1-SNAPSHOT.jar" azureuser@20.80.73.227:/home/azureuser/
```

查看：

```bash
ls -lh
```

输出：

```text
demo-0.0.1-SNAPSHOT.jar
```

说明上传成功。

---

# 七、启动 Spring Boot

执行：

```bash
java -jar demo-0.0.1-SNAPSHOT.jar
```

成功日志：

```text
Tomcat initialized with port 8080
Tomcat started on port(s): 8080
Started DemoApplication
```

说明项目启动成功。

---

# 八、开放 8080 端口

如果浏览器无法访问：

```text
VM
↓
Networking
↓
Inbound Port Rules
↓
Add inbound rule
```

配置：

```text
Source：
Any

Protocol：
TCP

Destination Port：
8080

Action：
Allow

Priority：
310
```

保存。

---

# 九、访问项目

公网 IP：

```text
20.80.73.227
```

接口：

```java
@GetMapping("/hello")
```

所以访问：

```text
http://20.80.73.227:8080/hello
```

返回：

```text
Hello Azure!
```

部署成功。

---

# 常见问题

## 1. Permission denied (publickey)

原因：

```text
SSH Key 未配置正确
```

解决：

```powershell
ssh -i "D:\vm1001_key.pem" azureuser@公网IP
```

---

## 2. Bad permissions

报错：

```text
UNPROTECTED PRIVATE KEY FILE
```

解决：

```powershell
icacls "D:\vm1001_key.pem" /inheritance:r
icacls "D:\vm1001_key.pem" /remove "Users"
icacls "D:\vm1001_key.pem" /grant:r Administrator:F
```

---

## 3. 浏览器打不开

检查：

```text
NSG 是否开放 8080
```

---

## 4. 出现 Whitelabel Error Page

说明：

```text
程序已经运行成功
```

但访问路径错误。

例如：

```java
@GetMapping("/hello")
```

正确地址：

```text
http://公网IP:8080/hello
```

错误地址：

```text
http://公网IP:8080
```

会返回：

```text
404
Whitelabel Error Page
```

---

# 本次实验收获

掌握了以下 Azure 基础能力：

✅ Resource Group

✅ Azure VM

✅ SSH Key

✅ Linux

✅ Java 环境部署

✅ SCP 文件上传

✅ NSG 网络安全组

✅ Spring Boot Jar 部署

✅ 公网访问

---

# 下一步学习

```text
01-AzureVM部署SpringBoot ✅

02-AppService部署SpringBoot

03-Docker部署SpringBoot

04-ContainerApps部署SpringBoot

05-AKS部署SpringBoot
```
``
