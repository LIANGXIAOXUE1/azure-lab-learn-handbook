# 创建 Linux VM

## 1. 是什么

Linux VM（Linux Virtual Machine）就是运行在 Azure 云上的一台 Linux 虚拟机。

你可以先把它理解成：

> 一台放在 Azure 数据中心里的远程 Linux 服务器。

它和本地安装的 Linux 主机在使用方式上类似，但有几个明显区别：

- 它运行在 Azure 云上
- 你可以按需创建和删除
- 你通常通过 SSH 远程连接
- 你不需要自己购买物理服务器

在 Azure 里，Linux VM 和 Windows VM 一样，都是非常基础的计算资源。  
很多网站、API、容器基础环境、开发测试环境，都会优先使用 Linux VM。

---

## 2. 解决什么问题

创建 Linux VM 主要是为了解决下面这些问题：

### 2.1 需要一台可远程登录的 Linux 服务器
很多应用、脚本、开发环境、Web 服务、代理服务，都运行在 Linux 环境中。

### 2.2 需要快速搭建测试环境
如果你想快速准备一个实验环境，例如：

- 测试 Linux 命令
- 安装 Nginx / Apache
- 部署简单 Web 服务
- 跑脚本或开发工具
- 模拟服务器环境

Linux VM 是很常见的选择。

### 2.3 不想自己维护本地服务器硬件
和 Windows VM 一样，Linux VM 可以直接在云上按需创建，不需要自己准备硬件。

### 2.4 需要更灵活地控制系统环境
如果你希望自己决定：

- 安装哪些软件
- 开哪些端口
- 用什么用户和密钥
- 怎么做系统配置

那 Linux VM 会比纯平台型服务更灵活。

---

## 3. 什么时候会用到 Linux VM

Linux VM 常见使用场景包括：

- 部署网站或 API
- 安装 Nginx / Apache / Docker
- 运行 Python / Node.js / Java / Go 等应用
- 做 SSH 远程运维
- 搭建跳板机
- 做学习实验
- 验证网络、端口、安全组规则
- 运行脚本任务或自动化工具

对 Azure 初学者来说，创建 Linux VM 是非常重要的基础实验，因为它会把下面这些概念串起来：

- Subscription
- Resource Group
- Region
- VM Size
- Username
- SSH Key
- Public IP
- NSG
- SSH 远程连接

---

## 4. 创建 Linux VM 前先理解什么

### 4.1 Linux VM 通常通过 SSH 连接，不是 RDP
Windows VM 常见远程方式是 RDP。  
Linux VM 最常见的远程连接方式是：

- SSH（Secure Shell）

默认常用端口是：

- TCP 22

所以创建 Linux VM 时，要重点关注的不是 3389，而是 22 端口是否放通。

---

### 4.2 建议优先使用 SSH Key，而不是只用密码
Linux VM 在 Azure 中通常更推荐使用：

- SSH 公钥 / 私钥

这样比单纯使用密码更常见，也更符合很多实际场景。

你可以理解为：

- 公钥放到 Azure VM 上
- 私钥保存在你自己的本地电脑上
- 后续连接时，用私钥完成身份验证

---

### 4.3 VM 创建成功，不代表 SSH 一定能连通
很多初学者会遇到这种情况：

- VM 创建成功
- Public IP 也有
- 但是 SSH 连不上

这通常和下面这些因素有关：

- 没有放通 22 端口
- SSH Key 不匹配
- 用户名输错
- 本地网络限制
- VM 还没完全启动
- 公网 IP 看错了

---

### 4.4 Linux VM 也会持续产生费用
只要 VM 处于运行状态，通常就会产生计算费用。  
所以学习实验要注意：

- 不用时及时停止
- 实验结束及时删除
- 避免长期空转

---

## 5. 怎么创建

下面以 Azure Portal 为例，演示最基础的 Linux VM 创建流程。

### 5.1 进入创建页面

1. 登录 Azure Portal
2. 搜索 `Virtual machines`
3. 点击 `Create`
4. 选择 `Azure virtual machine`

---

### 5.2 基础信息（Basics）

在 `Basics` 页签中，通常需要填写这些内容：

#### Subscription
选择资源所属订阅。

#### Resource Group
选择已有资源组，或者新建，例如：

```text
rg-azure-learning-linuxvm
```

#### Virtual machine name
输入虚拟机名称，例如：

```text
vm-linux-learn-01
```

#### Region
选择部署区域，例如：

- East Asia
- Southeast Asia
- Japan East

#### Image
选择 Linux 镜像，例如：

- Ubuntu Server 22.04 LTS
- Ubuntu Server 20.04 LTS
- CentOS
- Debian

学习阶段建议先选 Ubuntu，资料通常更多。

#### Size
选择适合测试的小规格即可。

#### Authentication type
这里通常会让你选择认证方式，例如：

- SSH public key
- Password

学习阶段建议优先使用：

- **SSH public key**

#### Username
设置登录用户名，例如：

```text
azureuser
```

> 注意：有些用户名可能受限制，尽量使用常见安全命名。

---

### 5.3 SSH 密钥配置

如果选择 `SSH public key`，通常需要：

- 使用已有公钥
- 或让 Azure 自动生成一对密钥

如果你本地已经有 SSH Key，可以把公钥填进去。  
如果没有，也可以先让 Azure 帮你生成。

学习阶段建议你重点记住：

- 私钥要保存在本地
- 公钥配置到 VM 上
- 后续 SSH 登录通常依赖私钥

---

### 5.4 入站端口（Inbound port rules）

为了后续通过 SSH 登录 Linux VM，通常需要允许：

- **SSH (22)**

常见做法是：

- 选择 `Allow selected ports`
- 勾选 `SSH (22)`

> 学习测试环境可以这样做，但正式环境应尽量限制来源 IP，避免公网过度暴露。

---

### 5.5 磁盘（Disks）

学习阶段一般保持默认即可。  
重点先放在：

- 能否创建成功
- 能否成功 SSH 连接
- 能否理解 VM 相关资源

---

### 5.6 网络（Networking）

这里通常会涉及：

- Virtual Network
- Subnet
- Public IP
- NIC network security group

学习阶段重点关注：

- 是否有 Public IP
- 是否允许 SSH 22 端口
- 是否自动创建了 NSG
- 是否自动创建或使用了 VNet / Subnet

---

### 5.7 检查并创建（Review + create）

1. 填完参数后，点击 `Review + create`
2. 等待 Azure 校验配置
3. 如果没有报错，点击 `Create`

然后等待部署完成。

---

## 6. 创建后会同时生成什么资源

和 Windows VM 类似，创建 Linux VM 时通常不只是生成一个 VM 对象，还会带出一组配套资源。

常见包括：

- Virtual Machine
- Network Interface（NIC）
- Public IP
- Network Security Group（有时会自动创建）
- Virtual Network / Subnet（如果之前没有）
- OS Disk

所以建议你创建完成后，去资源组里看一下资源列表。  
这样你会更容易建立一个认知：

> 创建 VM，其实是在创建一整组互相配合的资源。

---

## 7. 怎么测试

创建完成后，建议做下面几个基础测试。

### 7.1 测试 1：确认 VM 创建成功

进入 VM 详情页，检查：

- VM 状态是否为 `Running`
- 是否分配了 Public IP
- 操作系统是否为 Linux

---

### 7.2 测试 2：检查 SSH 22 端口是否已放通

查看：

- VM 的 Networking 页面
- NSG 入站规则
- 是否允许 TCP 22

如果没有放通，你通常无法通过 SSH 连接。

---

### 7.3 测试 3：使用 SSH 远程连接

在本地终端中，可以使用类似命令：

```bash
ssh azureuser@<Public-IP>
```

如果你使用的是私钥文件，命令可能类似：

```bash
ssh -i ~/.ssh/id_rsa azureuser@<Public-IP>
```

首次连接时，系统通常会提示你确认指纹，输入：

```bash
yes
```

如果成功进入命令行界面，说明 SSH 连接成功。

---

### 7.4 测试 4：执行简单 Linux 命令

连接成功后，可以执行一些基础命令，例如：

```bash
whoami
hostname
pwd
ls
```

如果这些命令可以正常运行，说明 VM 基础使用正常。

---

### 7.5 测试 5：停止和启动 VM

可以在 Azure Portal 中测试：

- Stop
- Start
- Restart

观察 VM 状态变化，理解它的生命周期管理方式。

---

### 7.6 测试 6：删除资源组

如果这是测试环境，实验结束后可以删除整个资源组，确认配套资源是否被一起删除。

---

## 8. 这个实验想让你理解什么

创建 Linux VM 不只是“建出一台机器”，更重要的是理解下面这些事。

### 8.1 Linux VM 通常依赖 SSH 进行远程管理
和 Windows VM 依赖 RDP 不同，Linux VM 更常见的是 SSH。

### 8.2 连接问题通常和网络、安全、密钥有关
很多 SSH 连不上，并不是 Linux 坏了，而是：

- 22 端口没放通
- 公钥私钥不匹配
- 用户名不对
- Public IP 输错
- 本地网络限制
- NSG 规则配置不对

### 8.3 一台 VM 背后往往是一组资源
VM 本身只是其中一部分，后面还会带出磁盘、网卡、IP、NSG、VNet 等资源。

### 8.4 学 Azure 不只是会创建，还要会验证
真正有价值的是：

- 你能创建
- 你能连上
- 你能解释为什么能连上
- 出问题时你知道先查哪几层

---

## 9. 常见问题

### 问题 1：Linux VM 创建成功了，为什么 SSH 连不上？

常见原因包括：

- 没有 Public IP
- NSG 没有放通 22 端口
- SSH Key 不匹配
- 用户名错误
- 本地网络限制了 SSH
- VM 还没完全启动
- 连接命令写错

---

### 问题 2：Linux VM 一定要用 SSH Key 吗？

不一定。  
某些情况下也可以使用密码登录，但在很多实际环境中，更常见、更推荐的是 SSH Key。

因为它通常更安全，也更符合服务器管理习惯。

---

### 问题 3：为什么我输入 IP 后提示 Connection timed out？

这通常表示网络层没通，常见检查方向包括：

- Public IP 是否正确
- NSG 是否放通 TCP 22
- 本地网络是否限制 SSH
- VM 是否真的处于 Running 状态

---

### 问题 4：为什么提示 Permission denied (publickey)？

这通常表示 SSH 身份验证失败，常见原因包括：

- 私钥不对
- 公钥没有正确配置到 VM
- 使用了错误用户名
- SSH 命令没有指定正确私钥文件

---

### 问题 5：学习阶段该选什么 Linux 镜像？

学习阶段通常建议优先选 Ubuntu。  
原因一般包括：

- 社区资料多
- 教程多
- 命令示例多
- 上手相对容易

---

## 10. 客户常问的问题

这一部分重点不是只记录客户怎么问，而是练习你该怎么回答。

---

### 问题 1：Azure Linux VM 是什么？

**简短回答：**  
Azure Linux VM 可以理解为一台运行在 Azure 云上的 Linux 服务器。

**展开回答：**  
如果客户需要自己控制 Linux 操作系统、安装软件、远程执行命令、部署服务，那么 Linux VM 是非常常见的选择。  
它本质上就是云上的虚拟服务器。

---

### 问题 2：什么时候该用 Linux VM？

**简短回答：**  
当客户需要较高系统控制权、要安装和管理自己的运行环境时，Linux VM 很适合。

**展开回答：**  
比如这些场景常见会用 Linux VM：

- 部署 Web 服务
- 跑 API
- 安装 Nginx / Docker
- 运行业务脚本
- 需要 SSH 管理
- 需要对系统做自定义配置

如果客户只是想把应用快速托管上线，不一定非要用 VM，也可能更适合 App Service 或容器平台。

---

### 问题 3：Linux VM 和 Windows VM 怎么选？

**简短回答：**  
要看应用依赖的运行环境，以及团队运维习惯。

**展开回答：**  
如果客户的应用明确依赖 Windows 环境，例如某些传统系统、Windows 服务或 RDP 管理方式，就更适合 Windows VM。  
如果客户更偏 Web 服务、开源组件、容器、命令行运维，很多时候 Linux VM 会更常见。

---

### 问题 4：Linux VM 和 App Service 怎么选？

**简短回答：**  
如果客户需要更多系统控制权，选 VM；如果更关注省运维，优先考虑 App Service。

**展开回答：**  
Linux VM 的优点是灵活，你可以自己控制系统和软件环境。  
但代价是你要自己承担更多运维工作。

App Service 更适合标准化的网站和 API 托管。  
所以关键要看客户是更需要“控制力”，还是更需要“托管能力”。

---

### 问题 5：Linux VM 安全吗？

**简短回答：**  
Azure 提供很多安全能力，但安全最终还取决于权限、网络和系统管理方式。

**展开回答：**  
如果 SSH 端口直接暴露公网，弱口令、密钥管理混乱、补丁不打，那一定有风险。  
一般要结合：

- SSH Key 管理
- 限制来源 IP
- NSG 规则
- 最小权限
- 日志审计
- 系统补丁更新

来一起看。

---

## 11. 你可以怎么对客户解释

如果客户第一次接触 Azure Linux VM，可以先从价值角度解释，不要一上来就讲很多技术参数。

你可以这样说：

> Azure Linux VM 可以理解为一台运行在云上的 Linux 服务器。  
> 如果客户需要自己控制操作系统、安装软件、部署服务、通过 SSH 远程管理环境，那么 Linux VM 是很常见的选择。  
> 它的优势是灵活、上线快，不需要自己采购物理服务器。  
> 但同时也意味着客户要自己承担更多系统层面的管理工作，比如 SSH、端口、安全配置和补丁维护。  
> 所以 Linux VM 更适合需要较高控制权的场景；如果只是想更轻量地托管应用，也可以进一步考虑 App Service 或容器服务。

---

## 12. 实践建议

学习完这一篇后，建议至少做下面几个动作：

### 12.1 创建一台测试用 Linux VM
尽量命名清晰，例如：

```text
vm-linux-learn-01
```

### 12.2 记录创建时的关键参数
例如：

- Subscription
- Resource Group
- Region
- Image
- Size
- Username
- Authentication type
- Public IP
- SSH 22 是否放通

### 12.3 创建完成后去资源组里看资源清单
确认除了 VM 之外，是否还生成了：

- NIC
- Disk
- Public IP
- NSG
- VNet

### 12.4 尝试 SSH 登录
实际用终端连接一次，确认这台 VM 真正可访问。

### 12.5 执行几个基础命令
例如：

```bash
whoami
hostname
ls
pwd
```

### 12.6 做一次停止和删除实验
理解成本控制和生命周期管理。

---

## 13. 实践记录

- **使用的订阅：**
- **资源组名称：**
- **VM 名称：**
- **部署区域：**
- **镜像版本：**
- **VM 规格：**
- **管理员用户名：**
- **认证方式（SSH Key / Password）：**
- **是否配置 Public IP：**
- **是否放通 SSH 22：**
- **是否成功 SSH 登录：**
- **资源组中自动创建了哪些配套资源：**
- **是否测试了停止 / 启动：**
- **是否测试了删除资源组：**
- **遇到的问题：**
- **解决方式：**
- **相关截图：** 后续补充

---

## 14. 本篇总结

Linux VM 是 Azure 中非常基础、也非常常见的计算资源之一。  
它的核心价值是：在云上快速提供一台可以通过 SSH 管理的 Linux 服务器。

学习这一步时，真正重要的不只是“创建成功”，而是理解：

- Linux VM 需要放在哪个 Subscription / Resource Group / Region
- Linux VM 通常依赖 SSH 远程连接
- VM 背后通常还会带出网卡、磁盘、公网 IP、NSG 等资源
- 创建成功后还要验证 SSH、端口、密钥和网络配置
- Linux VM 灵活，但也意味着要承担更多运维责任
- 学习和测试环境要注意及时停机或删除，避免浪费成本


## 15. 下一篇建议

建议下一篇继续学习：

- `05-远程连接测试-RDP-SSH.md`

因为学完 Windows VM 和 Linux VM 之后，最自然的下一步就是把远程连接和基础排查串起来。
```
