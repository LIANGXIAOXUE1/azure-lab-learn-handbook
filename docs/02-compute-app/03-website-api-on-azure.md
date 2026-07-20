# 网站和 API 怎么上 Azure

<br>

## 1. 是什么

<br>

学完 App Service 和 VM 的区别后，很多人都会产生一个问题：

<br>

> 网站和 API 到底应该怎么部署到 Azure？

<br>

对于刚开始接触云平台的人来说，经常会有一个习惯性的想法：

<br>

- 网站需要服务器
- API 需要服务器
- 上云就是买一台 VM

<br>

实际上 Azure 并不是这样工作的。

<br>

Azure 提供了多种应用部署方案，而服务器只是其中一种选择。

<br>

这一篇的核心目标是：

<br>

> 理解网站和 API 在 Azure 上有哪些常见部署方式，以及不同方案适用于什么场景。

<br>

---

<br>

## 2. 网站和 API 分别是什么

<br>

在学习部署之前，需要先理解这两个概念。

<br>

### 网站（Website）

<br>

网站主要面向用户访问。

<br>

例如：

<br>

- 企业官网
- 产品展示页
- 电商网站
- 后台管理系统

<br>

访问方式通常是：

<br>

```text
https://www.contoso.com
```

<br>

用户通过浏览器直接访问页面。

<br>

---

<br>

### API

<br>

API 主要面向程序调用。

<br>

例如：

<br>

- 登录接口
- 用户接口
- 文件上传接口
- AI调用接口

<br>

访问方式通常是：

<br>

```text
https://api.contoso.com/users
```

<br>

调用者通常是：

<br>

- Web前端
- 手机APP
- 第三方系统
- AI应用

<br>

---

<br>

## 3. 在 Azure 看来它们是什么

<br>

虽然网站和 API 的使用方式不同。

<br>

但对于 Azure 来说：

<br>

> 网站和 API 本质上都是应用程序。

<br>

因此很多情况下：

<br>

- 网站可以部署到 App Service
- API 可以部署到 App Service
- 网站与 API 可以共同组成一个系统

<br>

---

<br>

## 4. Azure 中常见的部署方式

<br>

在实际项目中，最常见的是下面三种方式。

<br>

### 4.1 VM

<br>

部署流程：

<br>

```text
代码
 ↓
VM
 ↓
安装运行环境
 ↓
部署应用
 ↓
开放访问
```

<br>

例如：

<br>

- IIS
- Nginx
- Apache

<br>

都可以部署在 VM 中。

<br>

特点：

<br>

- 灵活性高
- 控制权限大
- 运维工作较多

<br>

---

<br>

### 4.2 App Service

<br>

部署流程：

<br>

```text
代码
 ↓
App Service
 ↓
Azure负责运行平台
```

<br>

特点：

<br>

- 部署简单
- 上线速度快
- 运维成本低

<br>

对于大多数网站和 API 场景：

<br>

> App Service 都是优先考虑的方案。

<br>

---

<br>

### 4.3 AKS

<br>

部署流程：

<br>

```text
代码
 ↓
Docker镜像
 ↓
AKS集群
```

<br>

特点：

<br>

- 适合容器化应用
- 适合大型系统
- 学习成本较高

<br>

当前阶段只需要先知道它的存在即可。

<br>

后续学习容器和 Kubernetes 时会深入接触。

<br>

---

<br>

## 5. 学习阶段应该优先掌握什么

<br>

对于 Azure 初学者来说：

<br>

### 第一优先：App Service

<br>

因为它能够帮助你快速理解：

<br>

- Web应用部署
- API部署
- 域名绑定
- HTTPS
- 配置管理

<br>

同时不需要维护服务器操作系统。

<br>

---

<br>

### 第二优先：VM

<br>

学习 VM 的目的是理解：

<br>

- 服务器管理
- 操作系统
- 网络配置
- 环境安装
- 基础排障

<br>

而不是因为所有应用都必须运行在 VM 上。

<br>

---

<br>

## 6. 一个网站上线示例

<br>

假设客户有一个企业官网：

<br>

```text
www.contoso.com
```

<br>

最常见的上线流程如下：

<br>

```text
开发完成
 ↓
创建App Service
 ↓
上传代码
 ↓
绑定域名
 ↓
启用HTTPS
 ↓
正式上线
```

<br>

最终用户访问：

<br>

```text
https://www.contoso.com
```

<br>

即可打开网站。

<br>

---

<br>

## 7. 一个 API 上线示例

<br>

假设客户开发了一个 Spring Boot 项目。

<br>

接口包括：

<br>

```text
/api/user
/api/order
/api/upload
```

<br>

Azure 上部署流程：

<br>

```text
打包应用
 ↓
部署到App Service
 ↓
配置环境变量
 ↓
开放访问
```

<br>

调用方式：

<br>

```text
https://api.contoso.com/user
```

<br>

其它系统即可使用这些接口。

<br>

---

<br>

## 8. 网站和 API 为什么经常一起出现

<br>

很多新手会把网站和 API 理解成两个独立系统。

<br>

事实上很多企业应用架构如下：

<br>

```text
浏览器
 ↓
网站前端
 ↓
API
 ↓
数据库
```

<br>

用户访问的是网页。

<br>

网页调用的是 API。

<br>

API 再访问数据库。

<br>

这是最常见的企业 Web 架构之一。

<br>

---

<br>

## 9. 怎么快速判断部署方案

<br>

学习阶段先记住下面这组规则。

<br>

### 优先考虑 App Service

<br>

场景：

<br>

- 官网
- Web网站
- 后台系统
- Web API
- 演示系统

<br>

特点：

<br>

- 快速上线
- 维护简单

<br>

---

<br>

### 优先考虑 VM

<br>

场景：

<br>

- 老系统迁移
- 特殊软件依赖
- 系统权限要求高
- 自定义环境较多

<br>

特点：

<br>

- 灵活
- 控制能力强

<br>

---

<br>

## 10. 客户常问的问题

<br>

### 问题1：网站上 Azure 一定需要服务器吗？

<br>

**简短回答：**

<br>

不一定。

<br>

很多标准网站可以直接部署到 App Service。

<br>

---

<br>

### 问题2：API 能部署到 App Service 吗？

<br>

**简短回答：**

<br>

可以。

<br>

App Service 本身就是非常常见的 API 托管平台。

<br>

---

<br>

### 问题3：为什么越来越多项目推荐 App Service？

<br>

**简短回答：**

<br>

因为服务器管理工作更少，团队可以更专注业务开发。

<br>

---

<br>

### 问题4：以后是不是就不用 VM 了？

<br>

**简短回答：**

<br>

不是。

<br>

VM 仍然是 Azure 最重要的基础服务之一。

<br>

只是不同场景有不同选择。

<br>

---

<br>

## 11. 怎么测试

<br>

建议完成一个最基础实验。

<br>

### 实验目标

<br>

创建一个 App Service。

<br>

成功访问默认页面。

<br>

---

<br>

### 测试步骤

<br>

1. 创建 Resource Group
2. 创建 App Service Plan
3. 创建 Web App
4. 等待部署完成
5. 打开默认 URL

<br>

记录：

<br>

- App Name
- Region
- Runtime
- 默认域名
- 访问结果

<br>

---

<br>

## 12. 学习阶段真正要理解什么

<br>

### 12.1 上云不等于买服务器

<br>

服务器只是应用部署方式之一。

<br>

---

<br>

### 12.2 网站和 API 本质都是应用

<br>

Azure 更关注应用运行，而不是服务器本身。

<br>

---

<br>

### 12.3 现代云平台更强调应用托管

<br>

随着业务发展，你会越来越多接触：

<br>

- App Service
- Functions
- Container Apps
- AKS

<br>

这些服务都体现了 Azure 的平台化思想。

<br>

---

<br>

## 13. 实践记录

<br>

- **测试日期：**
- **使用订阅：**
- **资源组名称：**
- **App Service 名称：**
- **运行时：**
- **部署区域：**
- **默认访问地址：**
- **访问结果：**
- **遇到的问题：**
- **解决方式：**
- **相关截图：** 后续补充

<br>

---

<br>

## 14. 本篇总结

<br>

网站和 API 在 Azure 上最常见的部署方式包括：

<br>

- VM
- App Service
- AKS

<br>

对于大多数学习和普通业务场景：

<br>

> App Service 是最值得优先掌握的方案。

<br>

因为它能帮助你理解：

<br>

- 应用部署
- 应用访问
- 应用配置
- 应用上线

<br>

记住一句话：

<br>

> 客户真正关心的不是有没有服务器，而是应用能不能稳定运行。

<br>

---

<br>

## 15. 下一篇建议

<br>

建议继续学习：

<br>

`04-app-service-basic-deployment.md`

<br>

因为已经知道：

<br>

> 网站和 API 可以部署到 App Service。

<br>

下一步就需要真正创建一个 App Service，并完成第一次应用部署实验。
