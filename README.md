# Azure 学习手册

这是一个面向**系统学习 Azure** 的学习仓库。  
它不是单纯记录“我会创建哪些资源”，而是按照**学习路径 + 实验记录 + 排障速查 + 客户问答**的方式，逐步建立对 Azure 的完整理解。

这个仓库的核心目标不是“把 Azure 所有服务都学一遍”，而是先掌握**最常用、最容易被客户问到、最容易落地实践**的内容。

---

## 一、这个仓库在做什么

这个仓库主要记录以下内容：

- Azure 各核心服务的基础学习笔记
- Portal 创建与测试步骤
- 常见问题与排障思路
- 客户高频问题及回答方式
- 每个阶段的小实验和组合实践
- 后续面向项目落地的知识沉淀

简单说，这个仓库既是：

- 我的 Azure 学习笔记
- 我的 Azure 实验手册
- 我的 Azure 客户问答手册
- 我的 Azure 项目知识库雏形

---

## 二、学习目标

我希望通过这个仓库，逐步达到下面这些目标：

1. 能理解 Azure 的核心资源模型  
2. 能独立完成基础资源创建、访问、测试与排障  
3. 能说清楚常见服务分别解决什么问题  
4. 能回答客户高频问题，而不是只会“点 Portal”  
5. 能做出几个小型组合方案  
6. 最终形成一套可复用的 Azure 学习手册  

---

## 三、这个仓库的学习原则

这个仓库遵循几个原则：

### 1. 先有主线，不求全
学习顺序优先走这条主线：

**云基础 → 应用平台 → 身份安全 → AI 应用 → ML / IoT**

不是先把所有服务背一遍，而是先把高频主线打通。

---

### 2. 每学一个服务，都回答固定问题
每篇文档尽量回答下面这些问题：

1. 是什么  
2. 解决什么问题  
3. 怎么创建  
4. 怎么测试  
5. 常见问题  
6. 客户怎么问  
7. 你怎么回答  

这样学完以后，不只是“知道”，而是能讲、能做、能排障。

---

### 3. 每个阶段都留实验记录
每个模块除了概念，还会保留：

- 创建过程
- 测试过程
- 现象记录
- 排障记录
- 截图位置
- 自己的总结

---

### 4. 学习一定要能落地
每学完一个阶段，都尽量做一个小项目，例如：

- 基础阶段：VM + VNet + NSG + Blob + SAS
- 应用阶段：App Service + SQL + Key Vault
- AI 阶段：Azure OpenAI + AI Search + Speech
- IoT 阶段：IoT Hub + Storage + 简单分析

---

## 四、适合谁看

这个仓库适合：

- Azure 初学者
- 想系统梳理 Azure 学习路径的人
- 面向客户的售前 / 顾问 / 解决方案岗位
- 需要把 Azure 学习内容沉淀成文档的人
- 想从“会用服务”进阶到“能解释方案”的人

---

## 五、推荐学习路径

### 第一阶段：基础资源层
目标：掌握 Azure 最基本的资源创建、网络访问、存储、远程连接和基础排障能力。

学习内容包括：

- Azure 基础概念
- Subscription / Resource Group / Region
- 创建 Windows VM
- 创建 Linux VM
- 远程连接测试（RDP / SSH）
- VM 常见问题与排障
- NSG 规则测试
- VNet / Subnet / NSG / Public IP 概览
- Blob Storage 基础测试
- SAS Token 测试
- Azure OpenAI 模型部署基础

通过标准：

- 能独立创建 VM
- 能解释 Subscription / RG / Region
- 能理解网络放通与阻断
- 能创建 Blob 并生成 SAS
- 能完成 Azure OpenAI 基础部署

---

### 第二阶段：应用平台层
目标：掌握 Azure 上网站、API、应用托管的核心选择与部署思路。

重点包括：

- VM 和 App Service 怎么选
- 网站 / API 怎么上 Azure
- App Service 基础部署
- 应用配置管理
- 连接数据库的基本方式
- Key Vault 的基础使用
- 应用上线后的验证方式

通过标准：

- 能解释 VM 和 App Service 的区别
- 能部署一个简单网站或 API
- 能理解应用配置与密钥分离
- 能回答客户关于“怎么上 Azure”的问题

---

### 第三阶段：网络与存储层
目标：掌握 Azure 中最常用的网络与存储基础知识，能理解访问路径、权限边界和成本认知。

重点包括：

- 公网 IP / 私网 IP
- DNS 基础
- 网络排障速查
- Blob Storage
- SAS Token
- Disk 基础
- Azure Files
- 网络与存储成本认知

通过标准：

- 能说清公网与私网的区别
- 能做基础网络排障
- 能做 Blob / SAS 场景演示
- 能理解基础存储选型

---

### 第四阶段：数据库层
目标：掌握 Azure 上最常见数据库服务的认知、连接、安全、成本和选型思路。

重点包括：

- Azure SQL Database
- SQL Server on VM 与 Azure SQL 对比
- Azure Database for MySQL
- Azure Database for PostgreSQL
- 数据库访问控制
- 数据库备份与高可用基础
- 数据库常见连接问题排查

通过标准：

- 能解释常见数据库服务的区别
- 能完成基础连接测试
- 能回答“数据库放哪里”的问题
- 能理解数据库安全和成本基本思路

---

### 第五阶段：身份与安全层
目标：掌握 Azure 中最核心的身份、权限、密钥和访问控制能力。

重点包括：

- Microsoft Entra ID 基础
- Azure RBAC
- Key Vault
- 密钥、证书、Secret 管理
- 私有网络访问
- 日志与审计基础
- 谁能访问、怎么管权限

通过标准：

- 能解释身份和权限边界
- 能说清密钥该放哪里
- 能理解私有访问和公网访问的差异
- 能回答客户关于安全和权限的高频问题

---

### 第六阶段：监控与成本层
目标：掌握 Azure 资源的观察、告警、日志、基础运维与成本控制能力。

重点包括：

- Azure Monitor
- Log Analytics
- Alerts
- Activity Log
- 成本分析
- 预算与成本控制
- 常见资源的成本构成

通过标准：

- 能查看基础监控指标
- 能理解日志和告警的作用
- 能解释成本不只是“资源单价”
- 能回答客户“怎么看监控、怎么控成本”

---

### 第七阶段：AI 应用层
目标：掌握 Azure 中最常见的 AI 服务及其组合方式，能回答企业 AI 落地的高频问题。

重点包括：

- Azure OpenAI
- Azure AI Services
- AI Search
- Speech
- Document Intelligence
- Translation
- 企业知识库的基础组合方式

通过标准：

- 能解释 Azure OpenAI 和 AI Services 的区别
- 能回答“是不是一定要训练模型”
- 能理解知识库问答的基本组成
- 能做最基础的 AI 服务组合演示

---

### 第八阶段：ML / IoT 扩展层
目标：在已有基础上，扩展到机器学习和物联网场景。

重点包括：

- Azure Machine Learning
- Azure IoT Hub
- IoT 数据接入与存储
- 简单分析链路
- ML 与 AI 服务的区别

通过标准：

- 能理解 Azure ML 和 Azure OpenAI 的边界
- 能理解 IoT Hub 的作用
- 能搭一个最基础的 IoT 数据链路示例

---

## 六、当前仓库结构

建议目录结构如下：

```text
.
├─ README.md
├─ docs/
│  ├─ 01-foundation/
│  │  ├─ 00-第一阶段目录任务总表.md
│  │  ├─ 01-Azure基础概念.md
│  │  ├─ 02-Subscription-ResourceGroup-Region.md
│  │  ├─ 03-创建WindowsVM.md
│  │  ├─ 04-创建LinuxVM.md
│  │  ├─ 05-远程连接测试-RDP-SSH.md
│  │  ├─ 06-VM常见问题与排障.md
│  │  ├─ 07-NSG规则测试.md
│  │  ├─ 08-VNet-Subnet-NSG-PublicIP概览.md
│  │  ├─ 09-BlobStorage基础测试.md
│  │  ├─ 10-SASToken测试.md
│  │  └─ 11-AzureOpenAI模型部署基础.md
│  │
│  ├─ 02-compute-app/
│  │  ├─ app-service-overview.md
│  │  ├─ vm-vs-app-service.md
│  │  ├─ website-api-on-azure.md
│  │  └─ app-service-basic-deployment.md
│  │
│  ├─ 03-network/
│  │  ├─ public-private-ip-basics.md
│  │  ├─ network-troubleshooting-checklist.md
│  │  └─ network-pricing-basics.md
│  │
│  ├─ 04-storage/
│  │  ├─ storage-account-overview.md
│  │  ├─ blob-storage-step-by-step.md
│  │  ├─ sas-token-test.md
│  │  ├─ disk-overview.md
│  │  ├─ azure-files-overview.md
│  │  ├─ storage-common-issues-and-troubleshooting.md
│  │  └─ storage-pricing-basics.md
│  │
│  ├─ 05-database/
│  │  ├─ README.md
│  │  ├─ database-overview.md
│  │  ├─ azure-sql-database-overview.md
│  │  ├─ azure-sql-create-and-connect.md
│  │  ├─ sql-server-on-vm-vs-azure-sql.md
│  │  ├─ azure-database-for-mysql-overview.md
│  │  ├─ azure-database-for-postgresql-overview.md
│  │  ├─ database-network-access-basics.md
│  │  ├─ database-security-basics.md
│  │  ├─ database-backup-and-ha-basics.md
│  │  ├─ database-pricing-basics.md
│  │  ├─ database-troubleshooting-checklist.md
│  │  └─ customer-faq-database.md
│  │
│  ├─ 06-identity-security/
│  ├─ 07-monitoring-cost/
│  ├─ 08-ai/
│  ├─ 09-ml/
│  └─ 10-iot/
│
├─ projects/
│  ├─ phase1-basic-lab/
│  ├─ phase2-appservice-sql-keyvault/
│  ├─ phase4-openai-search-speech/
│  └─ phase6-iot-storage-analytics/
│
├─ templates/
│  ├─ service-note-template.md
│  ├─ practice-record-template.md
│  └─ customer-faq-template.md
│
└─ assets/
   └─ screenshots/
