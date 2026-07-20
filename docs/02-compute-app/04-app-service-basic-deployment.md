# App Service 基础部署

<br>

## 1. 是什么

<br>

前面已经学习了：

<br>

- App Service 是什么
- VM 和 App Service 的区别
- 网站和 API 怎么上 Azure

<br>

接下来就要真正开始动手。

<br>

这一篇的目标非常简单：

<br>

> 在 Azure 中创建一个 App Service，并成功访问它。

<br>

这是很多 Azure Web 应用学习路径里的第一个实战实验。

<br>

---

<br>

## 2. 为什么要学这一篇

<br>

如果只是知道 App Service 的概念，而没有真正创建过资源，很难理解：

<br>

- App Service 长什么样
- 创建时需要配置什么
- 创建完成后怎么访问
- 默认域名在哪里
- 一个应用在 Azure 中是如何运行的

<br>

所以这一篇的核心不是部署复杂项目。

<br>

而是先完成：

<br>

> 第一个能够真正访问的 Azure Web App

<br>

---

<br>

## 3. App Service 部署过程中会创建什么

<br>

最简单的 App Service 通常包含：

<br>

```text
Resource Group
        │
        ▼
App Service Plan
        │
        ▼
Web App
```

<br>

---

<br>

### Resource Group

<br>

用于管理资源。

<br>

相当于项目文件夹。

<br>

---

<br>

### App Service Plan

<br>

定义运行资源。

<br>

例如：

<br>

- 区域
- 性能规格
- CPU
- 内存

<br>

很多新手容易误以为：

<br>

> App Service 和 Plan 是同一个东西

<br>

实际上：

<br>

Plan 提供计算资源。

<br>

Web App 运行在 Plan 上面。

<br>

---

<br>

### Web App

<br>

真正运行网站或 API 的地方。

<br>

访问地址通常类似：

<br>

```text
https://mydemo.azurewebsites.net
```

<br>

---

<br>

## 4. 创建前准备

<br>

确保已经具备：

<br>

- Azure Subscription
- Contributor 权限
- 可正常登录 Azure Portal

<br>

Portal：

<br>

```text
https://portal.azure.com
```

<br>

---

<br>

## 5. 创建 App Service

<br>

### 第一步：进入 Portal

<br>

登录 Azure Portal。

<br>

搜索：

<br>

```text
App Service
```

<br>

点击：

<br>

```text
Create
```

<br>

---

<br>

### 第二步：选择基础信息

<br>

填写：

<br>

#### Subscription

<br>

选择自己的订阅。

<br>

---

<br>

#### Resource Group

<br>

选择已有资源组。

<br>

或者创建：

<br>

```text
rg-appservice-lab
```

<br>

---

<br>

#### Name

<br>

应用名称。

<br>

例如：

<br>

```text
my-first-appservice
```

<br>

名称需要全局唯一。

<br>

---

<br>

#### Publish

<br>

选择：

<br>

```text
Code
```

<br>

---

<br>

#### Runtime stack

<br>

根据应用选择。

<br>

例如：

<br>

- .NET
- Java
- Node.js
- Python

<br>

学习实验任选一个即可。

<br>

---

<br>

#### Region

<br>

选择部署区域。

<br>

例如：

<br>

```text
Southeast Asia
East Asia
```

<br>

---

<br>

## 6. 创建 App Service Plan

<br>

在创建流程中选择：

<br>

```text
Create new App Service Plan
```

<br>

例如：

<br>

```text
asp-demo-lab
```

<br>

然后选择规格。

<br>

学习实验建议：

<br>

```text
B1
```

或

```text
Free
```

<br>

这样成本更低。

<br>

---

<br>

## 7. 完成部署

<br>

点击：

<br>

```text
Review + Create
```

<br>

确认配置后：

<br>

```text
Create
```

<br>

等待部署完成。

<br>

通常几分钟内即可完成。

<br>

---

<br>

## 8. 如何访问应用

<br>

部署成功后进入资源页面。

<br>

可以看到：

<br>

```text
Default Domain
```

<br>

类似：

<br>

```text
https://my-first-appservice.azurewebsites.net
```

<br>

浏览器打开即可访问。

<br>

---

<br>

## 9. 第一次看到什么是正常的

<br>

很多同学第一次访问时发现：

<br>

```text
Your App Service app is up and running.
```

<br>

或者默认欢迎页。

<br>

这是正常现象。

<br>

因为：

<br>

> App Service 已经创建成功，但还没有部署自己的代码。

<br>

---

<br>

## 10. 怎么验证部署成功

<br>

建议检查下面几个项目。

<br>

### 检查一

<br>

资源状态：

<br>

```text
Running
```

<br>

---

<br>

### 检查二

<br>

默认域名可访问。

<br>

浏览器返回页面。

<br>

---

<br>

### 检查三

<br>

Overview 页面无错误提示。

<br>

---

<br>

## 11. 常见问题

<br>

### 问题1：名字无法创建

<br>

原因：

<br>

```text
Name already exists
```

<br>

App Service 名称全局唯一。

<br>

解决：

<br>

更换名称。

<br>

例如：

<br>

```text
myapp-2026-demo
```

<br>

---

<br>

### 问题2：没有免费规格

<br>

原因：

<br>

不同订阅可能支持情况不同。

<br>

解决：

<br>

选择 B1 进行实验。

<br>

---

<br>

### 问题3：打开页面失败

<br>

原因可能包括：

<br>

- 部署未完成
- 网络问题
- DNS刷新延迟

<br>

解决：

<br>

等待几分钟再次访问。

<br>

---

<br>

### 问题4：不知道选什么 Runtime

<br>

学习阶段不用纠结。

<br>

例如：

<br>

```text
.NET
```

或

```text
Java
```

<br>

均可。

<br>

后续会根据项目类型选择。

<br>

---

<br>

## 12. 客户常问的问题

<br>

### 问题1：App Service 创建完是不是就能访问网站？

<br>

简短回答：

<br>

可以访问。

<br>

但通常看到的是默认页面。

<br>

还需要部署业务代码。

<br>

---

<br>

### 问题2：为什么还要 App Service Plan？

<br>

简短回答：

<br>

Plan 提供运行资源。

<br>

Web App 运行在 Plan 上。

<br>

---

<br>

### 问题3：一个 Plan 可以放多个 App Service 吗？

<br>

简短回答：

<br>

可以。

<br>

多个 Web App 可以共享同一个 Plan。

<br>

---

<br>

### 问题4：App Service 算服务器吗？

<br>

简短回答：

<br>

底层依然有计算资源。

<br>

但客户不需要直接管理服务器。

<br>

---

<br>

## 13. 学习阶段真正要理解什么

<br>

### 13.1 App Service 不只是一个网站

<br>

它本质是：

<br>

> Azure 提供的应用托管平台

<br>

---

<br>

### 13.2 Plan 和 App 要区分

<br>

很多新手最容易混淆这两个概念。

<br>

记住：

<br>

```text
Plan = 资源
App = 应用
```

<br>

---

<br>

### 13.3 创建成功不等于业务上线

<br>

只是平台准备完成。

<br>

后面还需要部署代码。

<br>

---

<br>

## 14. 实践记录

<br>

- **测试日期：**
- **使用订阅：**
- **资源组名称：**
- **App Service Plan 名称：**
- **App Service 名称：**
- **部署区域：**
- **运行时：**
- **默认访问地址：**
- **访问结果：**
- **遇到的问题：**
- **解决方式：**
- **相关截图：** 后续补充

<br>

---

<br>

## 15. 本篇总结

<br>

通过本次实验，你应该能够：

<br>

- 创建 App Service
- 创建 App Service Plan
- 理解两者关系
- 访问默认域名
- 验证应用运行状态

<br>

记住一句话：

<br>

> App Service Plan 提供资源，App Service 运行应用。

<br>

这是后面学习应用部署、配置管理和自动化发布的重要基础。

<br>

---

<br>

## 16. 下一篇建议

<br>

建议继续学习：

<br>

`05-application-configuration-management.md`

<br>

因为应用创建完成后，下一步最常见的问题就是：

<br>

> 数据库连接串放哪里？API Key 放哪里？环境变量怎么管理？

<br>

这就是 Azure 应用配置管理要解决的问题。
