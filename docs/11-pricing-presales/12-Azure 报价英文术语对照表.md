# Azure 报价英文术语对照表

这篇文档主要解决一个非常常见的问题：

> **中文概念大概懂，但一看到 Azure 门户、价格页、英文报价单，就容易看不懂。**

例如你可能见过这些词：

- Virtual Machine
- Region
- vCPU
- Reserved Instance
- Pay as you go
- Managed Disk
- Blob Storage
- Load Balancer
- Defender for Cloud
- Backup
- SKU

如果这些词不熟，实际工作里就会很难受，因为你经常会遇到：

- Azure 官网价格页是英文或中英混杂
- Azure 门户里的资源名是英文
- 历史报价单喜欢写英文缩写
- 客户或销售有时直接发英文资源名

所以这一篇的目标是：

1. 帮你建立常见 Azure 报价英文词汇表  
2. 帮你理解这些词不是“死翻译”，而是对应什么资源和场景  
3. 让你以后看报价单、Azure 页面、历史表格时更顺手  
4. 给你一份适合直接查表的中英对照  

---

# 一、先记住一个原则：报价最常见的英文词，主要集中在 8 类

你不需要一开始就背全 Azure 所有英文。  
先掌握报价最常见的这 8 类就够用了：

1. 基础报价词  
2. 计算类  
3. 磁盘与存储类  
4. 数据库与缓存类  
5. 网络类  
6. 安全类  
7. 备份与监控类  
8. 价格与优惠类  

---

# 二、基础报价高频英文对照

这部分是最常见、最基础的词，建议优先记。

| 英文 | 中文 | 新手怎么理解 |
| ---- | ---- | ---- |
| Azure | 微软云平台 | 你现在报的整体平台 |
| Subscription | 订阅 | 一个 Azure 资源计费与管理单位 |
| Resource | 资源 | 云上的一个具体服务项 |
| Resource Group | 资源组 | 用来管理一组资源的“文件夹” |
| Region | 区域 | 资源部署在哪个地区 |
| Pricing | 定价 | 价格 |
| Pricing Calculator | 价格计算器 | 用来估算资源费用的工具 |
| Cost Estimate | 成本估算 | 预估费用 |
| SKU | 规格 / 型号 | 某个服务的具体档位或型号 |
| Configuration | 配置 | 资源设置 |
| Instance | 实例 | 一份实际运行的资源 |
| Usage | 用量 | 实际使用情况 |
| Meter | 计费项 | Azure 后台用来计费的细分项 |

---

# 三、计算类英文对照

这是你做报价最常见的一类。

| 英文 | 中文 | 新手怎么理解 |
| ---- | ---- | ---- |
| Virtual Machine (VM) | 虚拟机 | 云服务器 |
| VM Size | 虚拟机规格 | 服务器型号 |
| vCPU | 虚拟 CPU 核数 | 可以先理解为 CPU 核数 |
| Memory | 内存 | RAM |
| Operating System (OS) | 操作系统 | Linux / Windows |
| Linux | Linux 系统 | 常见开源服务器系统 |
| Windows Server | Windows 服务器系统 | 微软服务器操作系统 |
| Compute | 计算 | 程序跑的地方 |
| App Service | 应用服务 | Azure 托管 Web 应用服务 |
| Kubernetes Service (AKS) | Azure Kubernetes 服务 | 容器集群服务 |
| Function / Azure Functions | 函数服务 | 按调用执行的小型无服务器服务 |
| Availability Zone | 可用区 | 提高高可用的物理隔离区域 |
| Scale Up | 升配 | 规格变大 |
| Scale Out | 横向扩容 | 增加机器数量 |

---

## 计算类你最常见的几个表达

### 1）Virtual Machine
就是：
> 一台云服务器

### 2）VM Size
就是：
> 这台云服务器选什么规格

例如：
- D4as v5
- D8as v5
- F4s v2

### 3）vCPU
就是：
> 你可以先理解成“几核 CPU”

### 4）Memory
就是：
> 内存多少 GB

---

# 四、常见机型相关英文

这类你做 VM 报价时会经常看到。

| 英文 | 中文 | 说明 |
| ---- | ---- | ---- |
| General Purpose | 通用型 | 比较均衡，常见业务用 |
| Compute Optimized | 计算优化型 | CPU 更强，内存相对少 |
| Memory Optimized | 内存优化型 | 更适合吃内存的业务 |
| Burstable | 突发型 | 轻量低成本场景 |
| Series | 系列 | 某一类机型家族 |
| D Series | D 系列 | 常见通用型 |
| F Series | F 系列 | 偏计算型 |
| GPU VM | GPU 虚拟机 | AI / 图像 / 视频等场景 |

---

# 五、磁盘与存储类英文对照

这类也是高频。

| 英文 | 中文 | 新手怎么理解 |
| ---- | ---- | ---- |
| Managed Disk | 托管磁盘 | Azure 的云硬盘 |
| OS Disk | 系统盘 | 装操作系统的盘 |
| Data Disk | 数据盘 | 放业务数据的盘 |
| Standard SSD | 标准 SSD | 一般性能，成本较低 |
| Premium SSD | 高级 SSD / 高性能 SSD | 更高性能，更适合数据库 |
| Ultra Disk | 超高性能磁盘 | 更高性能场景 |
| Storage Account | 存储账户 | 存储服务的资源容器 |
| Blob Storage | 对象存储 | 放图片、附件、文件 |
| Azure Files | 文件存储 | 共享文件服务 |
| Capacity | 容量 | 存储大小 |
| Redundancy | 冗余 | 数据副本方式 |
| Hot Tier | 热层 | 常访问数据存储层 |
| Cool Tier | 冷层 | 较少访问数据存储层 |
| Archive Tier | 归档层 | 很少访问、低成本存储层 |

---

## 这几个词最容易遇到

### OS Disk
系统盘

### Data Disk
数据盘

### Blob Storage
对象存储，常用于：
- 商品图片
- 官网图片
- 附件
- 文件

### Storage Account
很多时候你会看到这个词，它更像是：
> 存储服务的“容器账号”

---

# 六、数据库与缓存类英文对照

| 英文 | 中文 | 新手怎么理解 |
| ---- | ---- | ---- |
| Database | 数据库 | 存业务数据 |
| Azure SQL Database | Azure SQL 数据库 | 托管 SQL 数据库 |
| SQL Server | SQL Server | 微软数据库 |
| MySQL | MySQL 数据库 | 常见开源数据库 |
| PostgreSQL | PostgreSQL 数据库 | 常见开源数据库 |
| Managed Database | 托管数据库 | 平台帮你托管更多底层工作 |
| Self-managed Database | 自建数据库 | 自己在 VM 上安装数据库 |
| Redis | Redis 缓存 | 高速缓存 |
| Cache | 缓存 | 提升访问速度，减轻数据库压力 |
| Connection | 连接 | 数据库连接数 |
| Read Replica | 只读副本 | 用于分担读请求 |
| High Availability (HA) | 高可用 | 主备或故障切换能力 |
| Backup Retention | 备份保留期 | 备份保存多久 |

---

## 常见理解

### Managed Database
托管数据库  
你可以理解成：
> 不重点买服务器，而是直接买数据库服务

### Self-managed Database
自建数据库  
你可以理解成：
> 先买 VM，再自己装数据库

### Redis / Cache
缓存服务  
在电商和 APP 场景非常常见。

---

# 七、网络类英文对照

网络类在报价里非常重要，也很容易混。

| 英文 | 中文 | 新手怎么理解 |
| ---- | ---- | ---- |
| Public IP | 公网 IP | 系统对外访问地址 |
| Private IP | 内网 IP | 内部网络地址 |
| Virtual Network (VNet) | 虚拟网络 | Azure 云上的内网 |
| Subnet | 子网 | VNet 里的更小网段 |
| Load Balancer | 负载均衡 | 把请求分到多台服务器 |
| Application Gateway | 应用网关 | 更偏应用层入口控制 |
| VPN Gateway | VPN 网关 | 本地和云上打通 |
| ExpressRoute | 专线接入 | 企业专线到 Azure |
| CDN (Content Delivery Network) | 内容分发网络 | 加速静态资源访问 |
| Bandwidth | 带宽 | 网络传输能力 |
| Data Transfer | 数据传输 | 网络流量传输 |
| Egress Traffic | 出网流量 | 流量从 Azure 往外发 |
| Ingress Traffic | 入网流量 | 流量进入 Azure |
| DNS | 域名解析 | 域名指向资源 |

---

## 网络类最重要的几个词

### Public IP
公网 IP  
有公网访问，一般就容易看到它。

### Load Balancer
负载均衡  
多台 Web / API 服务器时非常常见。

### CDN
内容分发网络  
特别适合：
- 图片
- CSS / JS
- 视频
- 下载文件

### Egress Traffic
出网流量  
这是很关键的计费词。  
很多账单差异就出在这。

---

# 八、安全类英文对照

| 英文 | 中文 | 新手怎么理解 |
| ---- | ---- | ---- |
| Microsoft Defender for Cloud | 云安全防护 | Azure 上的基础安全能力 |
| Firewall | 防火墙 | 控制进出流量 |
| Web Application Firewall (WAF) | Web 应用防火墙 | 防 Web 攻击 |
| DDoS Protection | DDoS 防护 | 防大流量攻击 |
| Key Vault | 密钥保管库 | 存密钥、证书、密码 |
| Identity | 身份 | 账号身份体系 |
| Access Control | 访问控制 | 谁可以访问什么 |
| Role-Based Access Control (RBAC) | 基于角色的访问控制 | 给不同人不同权限 |
| Encryption | 加密 | 数据加密保护 |
| Secret | 密钥 / 密文项 | 密码、Token 等 |
| Certificate | 证书 | HTTPS 证书等 |

---

## 这几个尤其常见

### Defender for Cloud
基础安全防护、威胁检测

### Firewall
防火墙

### WAF
Web 应用防火墙  
通常比普通 Firewall 更偏网站安全。

### Key Vault
保管：
- 密码
- API Key
- 证书
- 密钥

---

# 九、备份、监控、运维类英文对照

| 英文 | 中文 | 新手怎么理解 |
| ---- | ---- | ---- |
| Backup | 备份 | 资源恢复能力 |
| Recovery Services Vault | 恢复服务保管库 | 备份相关资源容器 |
| Site Recovery | 灾难恢复 | 故障切换 / 容灾 |
| Disaster Recovery (DR) | 灾备 | 出事后恢复能力 |
| Restore | 恢复 | 从备份恢复数据 |
| Monitoring / Monitor | 监控 | 观察资源运行状态 |
| Log Analytics | 日志分析 | 收集和分析日志 |
| Metrics | 指标 | CPU、内存等监控项 |
| Alerts | 告警 | 资源异常提醒 |
| Diagnostic Logs | 诊断日志 | 资源运行日志 |
| Retention | 保留期 | 日志或备份保留多久 |

---

## 重点理解

### Backup
备份  
你报价里常直接写 Backup 就行。

### Site Recovery / DR
灾备  
不是每个项目都需要，但关键项目很常见。

### Monitor / Log Analytics
监控和日志  
不一定每次单独列，但要知道它们的意义。

---

# 十、价格与优惠类英文对照

这部分在报价里非常高频，建议重点记。

| 英文 | 中文 | 新手怎么理解 |
| ---- | ---- | ---- |
| Pay as you go | 按量付费 | 用多少算多少 |
| Reserved Instance (RI) | 预留实例 | 1年 / 3年承诺换折扣 |
| Savings Plan | 节省计划 | 另一种承诺优惠方式 |
| Monthly Cost | 月度费用 | 每月大概多少钱 |
| Annual Cost | 年度费用 | 每年大概多少钱 |
| Estimated Cost | 预估费用 | 估算值 |
| Billing | 计费 | 账单相关 |
| Pricing Tier | 价格层级 | 服务档位 |
| Consumption | 使用量 / 消耗量 | 实际用掉多少 |
| Commitment | 承诺量 | 预留 / CPP 这类承诺 |
| Renewal | 续费 | 到期后续买 |
| Discount | 折扣 | 优惠 |

---

## 最关键的几个

### Pay as you go
按量付费  
最灵活，但通常单价更高。

### RI (Reserved Instance)
预留实例  
适合长期稳定运行的资源。

### Monthly Cost / Annual Cost
月度 / 年度费用  
你做报价汇总时最常写。

---

# 十一、中国版（世纪互联）相关高频词

这部分你也要熟。

| 英文 / 缩写 | 中文 | 说明 |
| ---- | ---- | ---- |
| Azure operated by 21Vianet | 由世纪互联运营的 Azure | Azure 中国版正式说法 |
| 21Vianet | 世纪互联 | 中国版运营方 |
| portal.azure.cn | 中国版 Azure 门户 | 中国版后台地址 |
| CNY | 人民币 | 中国版常见币种 |
| CPP | 承诺套餐 / 承诺优惠 | 中国版常见优惠方式 |

---

## 记忆重点

### Azure operated by 21Vianet
看到这个，就想到：
> Azure 中国版 / 世纪互联

### CPP
中国版常见优惠方式  
不要和 RI 混着写。

---

# 十二、报价单里常见缩写对照

这个部分特别适合查表。

| 缩写 | 全称 | 中文 |
| ---- | ---- | ---- |
| VM | Virtual Machine | 虚拟机 |
| OS | Operating System | 操作系统 |
| CPU | Central Processing Unit | 处理器 |
| vCPU | virtual CPU | 虚拟 CPU 核数 |
| RAM | Random Access Memory | 内存 |
| SSD | Solid State Drive | 固态硬盘 |
| DB | Database | 数据库 |
| LB | Load Balancer | 负载均衡 |
| CDN | Content Delivery Network | 内容分发网络 |
| IP | Internet Protocol Address | IP 地址 |
| VNet | Virtual Network | 虚拟网络 |
| VPN | Virtual Private Network | 虚拟专用网络 |
| WAF | Web Application Firewall | Web 应用防火墙 |
| HA | High Availability | 高可用 |
| DR | Disaster Recovery | 灾备 |
| RI | Reserved Instance | 预留实例 |
| SKU | Stock Keeping Unit | 规格 / 型号 |
| CPP | Commitment Plan / 中国版承诺套餐写法 | 中国版优惠方式 |

---

# 十三、英文报价单里常见句子怎么理解

下面是一些你在实际表格或邮件里很常见的表达。

---

## 1）Estimated monthly cost
意思是：
> 预估月度费用

---

## 2）Pay as you go price
意思是：
> 按量付费价格

---

## 3）1-year Reserved Instance price
意思是：
> 1 年预留实例价格

---

## 4）Storage capacity
意思是：
> 存储容量

---

## 5）Outbound data transfer
意思是：
> 出网数据流量

---

## 6）Backup retention
意思是：
> 备份保留期

---

## 7）High availability enabled
意思是：
> 已启用高可用

---

## 8）Region: East US
意思是：
> 区域：美国东部

---

# 十四、报价时最容易混淆的几个英文词

这部分特别重要。

---

## 1）Storage 和 Disk 不完全一样

### Disk
更偏：
- VM 的系统盘
- VM 的数据盘

### Storage
更偏：
- Blob
- Files
- 存储服务整体

所以不要看到 Storage 就默认是“磁盘”。

---

## 2）Instance 和 VM 不完全一样

### VM
明确是虚拟机

### Instance
更广义，意思是某个服务实例  
例如：
- Redis instance
- Database instance
- VM instance

---

## 3）Backup 和 Restore 不一样

### Backup
备份

### Restore
恢复

---

## 4）Ingress 和 Egress 不一样

### Ingress
入网流量

### Egress
出网流量

实际计费时，很多时候更要关注 Egress。

---

## 5）Availability 和 High Availability 不一样

### Availability
可用性，广义概念

### High Availability
高可用，指更具体的高可用架构能力

---

# 十五、给新手的最实用记忆法

如果你现在不想背太多，可以先只记这 20 个最常见词：

- VM
- vCPU
- Memory
- OS
- Region
- SKU
- Disk
- OS Disk
- Data Disk
- Blob Storage
- Database
- Redis
- Public IP
- Load Balancer
- CDN
- Defender
- Backup
- Pay as you go
- RI
- Monthly Cost

如果这 20 个你都熟了，已经足够支撑你看大多数基础报价单。

---

# 十六、给销售 / 新手可直接用的中英对照小抄

下面这段很适合单独贴出来。

---

## Azure 报价常用中英小抄

- 虚拟机 = Virtual Machine (VM)
- 虚拟机规格 = VM Size
- 区域 = Region
- 核数 = vCPU
- 内存 = Memory
- 操作系统 = Operating System (OS)
- 系统盘 = OS Disk
- 数据盘 = Data Disk
- 标准 SSD = Standard SSD
- 高级 SSD = Premium SSD
- 对象存储 = Blob Storage
- 文件存储 = Azure Files
- 数据库 = Database
- 缓存 = Cache / Redis
- 公网 IP = Public IP
- 负载均衡 = Load Balancer
- 内容分发网络 = CDN
- 备份 = Backup
- 高可用 = High Availability (HA)
- 灾备 = Disaster Recovery (DR)
- 按量付费 = Pay as you go
- 预留实例 = Reserved Instance (RI)
- 月度费用 = Monthly Cost
- 年度费用 = Annual Cost

---

# 十七、新手最容易犯的 6 个英文理解错误

---

## 错误 1：把 Storage 都理解成磁盘
其实 Storage 也可能指 Blob、Files 等存储服务。

---

## 错误 2：把 Instance 都理解成 VM
其实很多服务都叫 instance，不只是虚拟机。

---

## 错误 3：把 RI 和 CPP 混为一谈
- RI 常见于国际版
- CPP 常见于中国版

---

## 错误 4：看到 SKU 不知道是什么意思
SKU 一般就理解成：
> 规格、型号、档位

---

## 错误 5：分不清 Backup 和 DR
- Backup = 备份
- DR = 灾备 / 容灾

不是一个层级的概念。

---

## 错误 6：看到 Egress 不知道它就是出网流量
这个会直接影响你对账单的理解。

---

# 十八、这篇你要记住的核心结论

## 1. Azure 报价英文不用一开始全背
先掌握高频词就够用了。

## 2. 报价最常见英文主要集中在几类
- 基础词
- 计算
- 磁盘与存储
- 数据库
- 网络
- 安全
- 备份
- 价格与优惠

## 3. 最重要的英文词建议优先熟悉
例如：
- VM
- Region
- vCPU
- Disk
- Blob Storage
- Redis
- Load Balancer
- Backup
- Pay as you go
- RI

## 4. 中国版相关英文也要单独记
尤其是：
- Azure operated by 21Vianet
- portal.azure.cn
- CPP
- CNY

## 5. 术语不是只会翻译，还要知道它在系统里是干什么的
这才真正有用。

---

# 十九、建议下一篇接着看什么

如果你后面继续扩展这套仓库，建议下一篇优先补：

## [13-Azure计算器使用说明.md](./13-Azure计算器使用说明.md)

因为当你已经能看懂：
- 资源是什么
- 需求怎么拆
- 英文是什么意思

下一步最自然的问题就是：

> **那我到底怎么去 Azure 官方计算器里把这些价格查出来？**

下一篇如果写“Azure 计算器使用说明”，会非常适合新手实操。
