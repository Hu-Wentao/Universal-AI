---
timezone: UTC+8
---

# jianlin chen

**GitHub ID:** Airjiannan05

**Telegram:** @none

## Self-introduction

在校计算机大学生一枚，专攻ai前沿技术，有相关的链上开发基础，对区块链加ai的发展有浓厚的兴趣。Blockchain is the future.

## Notes

<!-- Content_START -->
# 2025-11-25
<!-- DAILY_CHECKIN_2025-11-25_START -->
**学习目标**

-   本地 / 云端完成基础开发环境落地。
    
-   能描述自己接下来 2 周的学习目标。
    

**学习资料**

-   ZetaChain CLI
    
-   [https://github.com/zeta-chain/cli](https://github.com/zeta-chain/cli)
    
-   ZetaChain Node / RPC / Faucet / Explorer / 测试币获取
    
-   [https://www.zetachain.com/docs/reference/](https://www.zetachain.com/docs/reference/)
    
-   Qwen API 参考（含 OpenAI 兼容方式）
    
-   [https://www.alibabacloud.com/help/zh/model-studio/qwen-api-reference](https://www.alibabacloud.com/help/zh/model-studio/qwen-api-reference)
    

**扩展资料（可选）**

-   再快速浏览一遍 ZetaChain Developers
    
-   [https://www.zetachain.com/docs/developers](https://www.zetachain.com/docs/developers)
    

**实践 / 作业**

-   安装或尝试使用 ZetaChain CLI（本地或云端环境均可）。
    
-   了解测试网 RPC、Faucet、Explorer 的入口，记录在自己的笔记中。
    
-   在终端或 Postman 里完成一次 Qwen API 的简单请求（哪怕只是 200 报错也可以，先打通连通性）。
    

# 1.安装ZetaChain CLI

## ZetaChain CLI

ZetaChain CLI：用于构建和交互 [ZetaChain](https://www.zetachain.com/) 通用应用的命令行接口。它是开发者、节点验证者（Validators）和高级用户用来“控制”和“查询”ZetaChain 网络的“遥控器”。由于 ZetaChain 是基于 Cosmos SDK 构建的，其 CLI 的操作逻辑与大多数 Cosmos 生态的链非常相似。

### 核心组件：`zetacored`

ZetaChain 的主要二进制文件通常被称为 `zetacored`。它集成了运行节点和作为客户端交互的所有功能。

### 主要功能模块

ZetaChain CLI 的功能主要分为以下几大类：

A. 钱包与密钥管理 (Key Management)

用于生成和管理账户。

-   **创建账户：** 生成新的助记词和私钥。
    
-   **恢复账户：** 导入助记词。
    
-   **查看地址：** 获取你的 ZetaChain 地址（通常以 `zeta` 开头）。
    
-   _命令示例：_ `zetacored keys add mywallet`
    

B. 查询网络状态 (Querying)

用于从区块链上获取只读信息，不需要消耗 Gas 费。

-   **查余额：** 查看 ZETA 代币余额。
    
-   **查交易：** 追踪跨链交易的状态。
    
-   **查区块信息：** 查看当前区块高度。
    
-   **查跨链信息：** 查询 ZetaChain 观察到的比特币或以太坊网络的状态（这是 ZetaChain 特有的，涉及 `observer` 模块）。
    
-   _命令示例：_ `zetacored query bank balances [地址]`
    

C. 发送交易 (Transactions)

用于向网络写入数据，需要消耗 ZETA 作为 Gas 费。

-   **转账：** 发送 ZETA 代币给其他人。
    
-   **质押 (Staking)：** 将代币质押给验证者以获得奖励。
    
-   **治理 (Governance)：** 对网络提案进行投票。
    
-   **部署合约：** 尽管通常使用 Hardhat/Foundry 部署 EVM 合约，但 CLI 也可用于底层交互。
    
-   _命令示例：_ `zetacored tx bank send [发送者] [接收者] 1000000azeta`
    

D. 节点运营 (Node Operations)

这是验证者使用的功能。

-   **启动节点：** 运行全节点或验证者节点，同步区块数据。
    
-   **初始化：** 配置创世文件 (genesis.json)。
    
-   _命令示例：_ `zetacored start`
    

## 先决条件

-   Node.js ≥ 18
    
-   Git（用于模板克隆）
    
-   （可选）Docker ≥ 24 for`localnet`
    

## 本地运行

```PowerShell
npx zetachain@next new
```

## 全局安装

```PowerShell
npm install -g zetachain@latest
```

## 验证

```PowerShell
zetachain query chains list
// 此命令会打印出当前连接到 ZetaChain 的所有链，即成功
```

![](https://av1ln7qpa6l.feishu.cn/space/api/box/stream/download/asynccode/?code=NjVhODdjZGNjOWM0NmQ1NTJlZDBhMjkwNmJjNGFjNmVfbWwzMWIwV1p5N3dsdm41dkVmbHhkQUNDd3dCbHpCWVJfVG9rZW46TmlNWmJuQm96b2U5TjZ4YVJnV2N1ZmkwbndkXzE3NjQwNjQ2ODQ6MTc2NDA2ODI4NF9WNA)

## Example

创建一个新项目：

```Plain
zetachain new
```

启动localnet：

```Plain
zetachain localnet start
```

![](https://av1ln7qpa6l.feishu.cn/space/api/box/stream/download/asynccode/?code=NDVmMTc3MDRiMDg4Mzc5MWY2OTA5NTE3YmUwNmUyOGVfZFo1UHEwUTVxMHpEVk5TV09RQWZ5MFAzT29DUFdudWpfVG9rZW46U1lGYWJQZHZwb0J6WDR4WGdZT2NJNUowblJnXzE3NjQwNjQ2ODQ6MTc2NDA2ODI4NF9WNA)

查询跨链余额：

```Plain
zetachain query balances --evm <钱包地址>
```

注意：要有钱包（无则创建： npx zetachain accounts create --name <name> ）

![](https://av1ln7qpa6l.feishu.cn/space/api/box/stream/download/asynccode/?code=YmEwOWNmODg0MGQ5NGJlNGE3NDUxNjBhZDA2ZmZkYjNfR0M3OWh0ZkJTS1pqRkZZSTRyMDhTdG5oVU5Dcnh5dzNfVG9rZW46VUx5VmJveWllb3M5NXp4SlYwbWNuM09IbmNoXzE3NjQwNjQ2ODQ6MTc2NDA2ODI4NF9WNA)

## CLI参考

完整指挥文件：

[https://www.zetachain.com/docs/reference/cli/](https://www.zetachain.com/docs/reference/cli/)

```Plain
zetachain docs
```

或者配合任何命令使用：`--help`

```Plain
zetachain accounts --help
```

# 2.项目前置准备

1\. Faucet领取测试币：

[https://www.zetachain.com/docs/reference/faucet/](https://www.zetachain.com/docs/reference/faucet/)

[https://zetachain.faucetme.pro/](https://zetachain.faucetme.pro/)

![](https://av1ln7qpa6l.feishu.cn/space/api/box/stream/download/asynccode/?code=OTY1Yjc5MzVlMzlmYjRhODQ2Y2FjYmE3YWE3M2QyYWFfcmdOdDg2dkI4bDljWHJqVjlDNVZsRnNQbHp1cHE3cktfVG9rZW46VVk3amJzQnEzb0R3MEJ4U0JDQmNiOEtjbmpoXzE3NjQwNjQ2ODQ6MTc2NDA2ODI4NF9WNA)

2.主网和测试网：

[https://www.zetachain.com/docs/developers/chains/list/](https://www.zetachain.com/docs/developers/chains/list/)

3.RPC 节点：

[https://www.zetachain.com/docs/reference/network/api](https://www.zetachain.com/docs/reference/network/api)

使用allthatnode:

[https://www.allthatnode.com/project.dsrv?seq=1c82ed14a14d215be82f31de6e1027359381cdbc](https://www.allthatnode.com/project.dsrv?seq=1c82ed14a14d215be82f31de6e1027359381cdbc)

![](https://av1ln7qpa6l.feishu.cn/space/api/box/stream/download/asynccode/?code=MzRlOTRmMTZkNDU3ZDI1NjkwN2RkZmMzMGZhMDY4MWFfbDA1RkZIang2R3VLc3ZubXR4S2JkbEt6YWdTdld1c2NfVG9rZW46RnZXeGJqQXJtb0trVVF4WHFwbmN6eTN5bjRkXzE3NjQwNjQ2ODQ6MTc2NDA2ODI4NF9WNA)

# 3.回顾一下RPC（**Remote Procedure Call**（远程过程调用））

RPC (Remote Procedure Call，远程过程调用)是一种进程间通信 (IPC)技术。

它允许一台计算机上的程序（客户端）调用另一台计算机（服务器）上的子程序或函数，而程序员无需显式编写远程交互的底层网络代码。

在区块链（特别是 ZetaChain 这种基于 Cosmos SDK 且兼容 EVM 的架构）的上下文中，RPC 的技术定义和作用如下：

### 1\. 技术定义：区块链节点的 API 层

区块链网络由分布式的**\*\*节点 (Nodes)\*\*** 组成。这些节点维护着账本的\*\*状态 (State)\*\*（如账户余额、合约代码、存储槽数据）。节点通常运行在一个隔离的环境中。

RPC 接口是节点软件暴露给外部世界的\*\***标准 API 端点**\*\*。它使得外部客户端（如您的 ZetaChain CLI、DApp 前端、索引器）能够与节点进行通信。

从架构上看，它遵循 **Client-Server 模型**：

-   **Client (Stub):** 您的开发环境。它将本地的方法调用（如 `query balances`）打包（序列化）成网络请求。
    
-   **Transport:** 数据包通过网络协议（通常是 HTTP 或 WebSocket）传输。
    
-   **Server (Node):** 区块链节点接收请求，解包，在本地状态机中执行查询或将交易注入内存池 (Mempool)，然后将结果序列化返回。
    

### 2\. ZetaChain 中的双重 RPC 架构（关键专业知识）

由于 ZetaChain 是基于 Cosmos SDK 构建并兼容 EVM（以太坊虚拟机）的，它的 RPC 架构比普通公链更复杂，通常包含两层：

A. JSON-RPC (EVM 层)

这是以太坊生态的标准协议。当您使用 `npm install -g zetachain` 安装的 JS CLI 开发智能合约时，主要交互的是这一层。

-   **协议标准：** JSON-RPC 2.0 (无状态、轻量级)。
    
-   **数据格式：** JSON。
    
-   **典型端口：** 8545。
    
-   **主要用途：**
    
    -   部署 Solidity 合约 (`eth_sendRawTransaction`)。
        
    -   调用合约方法 (`eth_call`)。
        
    -   获取 EVM 层的区块和交易信息。
        
-   **示例 Payload：**
    
    ```JSON
    {
      "jsonrpc": "2.0",
      "method": "eth_getBalance",
      "params": ["0xYourAddress", "latest"],
      "id": 1
    }
    ```
    

B. gRPC & REST (Cosmos SDK 层)

这是 ZetaChain 底层共识和跨链模块的通信协议。当您涉及质押 (Staking)、治理或底层跨链观察者 (Observer) 数据时，会用到这一层。

-   **gRPC:** 基于 HTTP/2，使用 Protocol Buffers (Protobuf) 进行二进制序列化。性能极高，延迟低。主要用于节点间通信或高性能客户端（如 `zetacored` Go CLI）。
    
    -   _典型端口：9090_
        
-   **REST (LCD):** 将 gRPC 封装为 HTTP 接口，方便网页端调用。
    
    -   _典型端口：1317_
        

### 3\. 开发中的关键概念

在专业开发中，理解 RPC 意味着你需要关注以下指标：

1.  **Endpoint (端点 URL):**
    

1.  这是 RPC 服务的入口地址。
    
    -   _Public RPC:_ 官方或社区提供的免费节点（如您在教程中自动连接的）。通常有\*\*速率限制 (Rate Limit)\*\*，比如每秒只能请求 10 次。
        
    -   _Private RPC:_ 使用 Infura、Alchemy 或 BlockPi 等基础设施服务商提供的专用节点，高并发、更稳定。
        

2.  **WebSockets (WSS) vs HTTP:**
    
    1.  **HTTP:** 它是“拉”模式 (Pull)。您的 CLI 必须不断询问“交易确认了吗？”
        
    2.  **WebSockets:** 它是“推”模式 (Push)。您可以建立长连接，订阅事件（如 `logs`），一旦链上有特定事件发生，节点会主动通过 RPC 推送消息给您的程序。
        
3.  **状态最终性 (Finality):**
    

1.  通过 RPC 查询到的数据取决于节点的同步状态。如果连接的 RPC 节点落后于网络（未同步），您获取的数据就是旧的。
    

### 总结

在您的开发流程中：

**RPC 是将您的业务逻辑（JavaScript/TypeScript 代码）与去中心化网络状态（ZetaChain 区块链数据）连接起来的通信协议和网关。**

当您执行 `zetachain query` 时，您实际上是在构造一个 **HTTP 请求**，发送给远程服务器上的 **JSON-RPC 接口**，服务器查询其本地的 **LevelDB/RocksDB 数据库**，然后将十六进制的结果返回给您并进行解码。

# 完成一次 Qwen API 的简单请求

看到群友“菜鸟Appler-R"的调用，重现了一下hhh

![](https://av1ln7qpa6l.feishu.cn/space/api/box/stream/download/asynccode/?code=OGU4YTRmNGNkMzVkMWJiZWYwMTQxNTg1ZTIyZGM3MGJfQVVnajhMUTdtejF0RklUVDZyeHdEQWlZbTJMN0R6R2lfVG9rZW46Tm5wTmJNNnJLb2V4d014UlV5VmNKNTRObkJjXzE3NjQwNjQ2ODQ6MTc2NDA2ODI4NF9WNA)
<!-- DAILY_CHECKIN_2025-11-25_END -->

# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->

# DAY1

**学习资料**

-   ZetaChain 总文档
    
-   [https://www.zetachain.com/docs/](https://www.zetachain.com/docs/)
    
-   ZetaChain Developers（入口总览）
    
-   [https://www.zetachain.com/docs/developers](https://www.zetachain.com/docs/developers)
    
-   Qwen 总文档（Quickstart / Key Concepts）
    
-   [https://qwen.readthedocs.io/zh-cn/latest/](https://qwen.readthedocs.io/zh-cn/latest/)
    

# 什么是ZetaChain

目标：不同链之间互联，能够原生访问任何区块链，让加密货币变得像互联网一样易于访问、多样化和互联

ZetaChain 是一个赋能开发者创建通用，能够无缝交互任何区块链的应用。

官网的developer界面

![](https://av1ln7qpa6l.feishu.cn/space/api/box/stream/download/asynccode/?code=ODYzZjU5M2FjMDgyOGIzZTFmMWU5MDMwYzYyZjZmZTlfNFZydGwwZDF0SEIxSzA0VEpPOWJJOTFxWVR2VnQ3MjNfVG9rZW46WFU2ZmJoQ0xmb05lcUd4OGZoWmN5ano1blFlXzE3NjM5Njk2MzM6MTc2Mzk3MzIzM19WNA)

# 环境搭建

## 先决条件

-   [**Node.js**](https://nodejs.org/en)**（推荐v21或更晚版本）：**必须 运行 ZetaChain CLI 并管理 JavaScript 依赖。(node -v)
    
-   **Yarn或者NPM：**用于安装和 更新项目库。两种方法都可以，随你喜欢。(npm version)
    
-   [**Git**](https://git-scm.com/)**:**管理项目资源必不可少 编程和与他人协作。
    
-   [**JQ**](https://jqlang.org/)**:**一个轻量级命令行JSON处理器， 对于解析Localnet输出和编写shell脚本非常有用。(win bash:winget install jqlang.jq)
    
-   [**Foundry**](https://getfoundry.sh/)**:**一个快速、模块化的以太坊工具包 发展。你会用它来编译契约、管理依赖和运行 Localnet。
    

### Windows

在 Windows 上安装 Foundry 需要一些额外的步骤，因为`foundryup` 目前不支持 PowerShell 或命令提示符 (Cmd)。您需要使用 Windows Subsystem for Linux (WSL) 或 Git BASH 来进行安装。\[[1](https://www.google.com/url?sa=E&q=https%3A%2F%2Fvertexaisearch.cloud.google.com%2Fgrounding-api-redirect%2FAUZIYQF7zCQXvNYyf1lIuwj_SykCNnDx-Fs34VfoYyf3ctjVjTHBXDt9T0oqAn542wsnl088smS_Lj9n5l0cI11E24eFj4qehO9A6AVp_pYN5L5ge9jDRaDvVX27gbPWQ6fqk1C7PraRa8LPv4_aAiap)\]\[[2](https://www.google.com/url?sa=E&q=https%3A%2F%2Fvertexaisearch.cloud.google.com%2Fgrounding-api-redirect%2FAUZIYQGzBjoCSkl_rKeTK2BbapcE-MR8_4zguUZ9YJcyYxxAba1j2J8NNYf7Ngy3woDdVyZklosYbRjydKx1rmO2L3EchMCOQmvlb60R0ca6L4t2ptSATdjLG3pCcg9-kkO_oWYGTzb3fsmBgw9C8qVaXox6pr0W8S2782AXTvGgkg7KxFeIBh6SWdN_l4YBnA%3D%3D)\]

**步骤 1：安装 Windows Subsystem for Linux (WSL)**

1.  打开 PowerShell 或 Windows 命令提示符，并以管理员身份运行。
    
2.  输入以下命令来安装 WSL：
    
3.  codeBash
    

```Plain
wsl --install
```

**步骤 2：在 WSL 中安装 Foundry**

1.  打开您的 WSL 终端 (例如 Ubuntu)。
    
2.  运行与 macOS 和 Linux 相同的 `curl` 命令来安装 `foundryup`：
    

```Plain
curl -L https://foundry.paradigm.xyz | bash
```

1.  按照屏幕上的指示完成安装，然后运行 `foundryup` 来安装 Foundry 工具链：
    

```Plain
foundryup
```

## 环境建设

Install the ZetaChain CLI:

```Shell
npm install -g zetachain
```

Run:

```Shell
zetachain query chains list
```

这个命令可以打印所有当前连接在ZetaChain上的链条

对于本地开发，推荐运行Localnet，一个自给自足的平台。该环境包括ZetaChain、EVM、Solana、Sui和TON。Localnet 是构建和测试通用应用最快的方法，无需依赖公共测试网。

注意：必须要有Foundry才可以运行Localnet

# qwen账号注册和进入控制台

1.进入阿里云百炼，注册，创建API key即可

[https://bailian.console.aliyun.com/?tab=model#/model-market/detail/qwen3-max](https://bailian.console.aliyun.com/?tab=model#/model-market/detail/qwen3-max)
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->
