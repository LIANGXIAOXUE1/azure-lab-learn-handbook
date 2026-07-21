# 02-AppService部署SpringBoot

## 实验目标

将本地 Spring Boot 项目打包为 Jar，并部署到 Azure App Service，通过 Azure 自动生成的域名访问接口。

相比 Azure VM，无需手动安装 Java、配置 Linux、开放端口和 SSH 登录。

---

# 一、准备工作

## 1. Spring Boot 项目

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

# 二、创建 App Service

进入 Azure Portal：

```text
App Services
↓
Create
↓
Web App
```

---

## Web App 配置

填写：

```text
名称：
app-xiaoxue-demo

发布模型：
代码

运行时堆栈：
Java 17 SE

Web 服务器：
Java SE (Embedded Web Server)

操作系统：
Linux

区域：
Central US
```

---

## 应用服务计划

选择：

```text
Basic B1
```

实验环境可使用：

```text
Free F1
```

（如果订阅支持）

---

点击：

```text
Review + Create
↓
Create
```

等待部署完成。

---

# 三、获取访问域名

创建完成后进入：

```text
Web App
↓
概述（Overview）
```

找到：

```text
默认域
```

例如：

```text
app-xiaoxue-demo-ejgbaufchmdsa3ge.centralus-01.azurewebsites.net
```

这就是 Azure 自动提供的访问域名。

---

# 四、部署 Jar

进入：

```text
部署中心
↓
设置
```

选择：

```text
发布文件（新）
```

---

上传：

```text
demo-0.0.1-SNAPSHOT.jar
```

点击：

```text
保存
```

开始部署。

---

# 五、查看部署结果

进入：

```text
部署中心
↓
日志
```

看到：

```text
状态：
已成功（活动）

消息：
OneDeploy
```

说明部署成功。

---

# 六、配置运行环境

进入：

```text
配置
↓
堆栈设置
```

确认：

```text
Java 版本：
17

Web 服务器：
Java SE (Embedded Web Server)
```

---

# 七、访问接口

假设接口：

```java
@GetMapping("/hello")
```

则访问：

```text
https://app-xiaoxue-demo-ejgbaufchmdsa3ge.centralus-01.azurewebsites.net/hello
```

返回：

```text
Hello Azure!
```

说明部署成功。

---

#
