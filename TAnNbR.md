---
timezone: UTC+8
---

# Tam

**GitHub ID:** TAnNbR

**Telegram:** @Tam_069

## Self-introduction

研三、dapp开发

## Notes

<!-- Content_START -->
# 2025-11-26
<!-- DAILY_CHECKIN_2025-11-26_START -->
# \# ZetaChain — Universal App 与 Gateway 说明

## \## 1. Universal App 是什么

\- **Universal App** 是部署在 ZetaChain 上的一种智能合约，它运行在 ZetaChain 的 **Universal EVM**。

\- 与普通合约不同，Universal App **可以接受来自任意连接链（如 Ethereum、Bitcoin、Solana 等）的合约调用、消息和代币转移**。

\- 同样，它也可以从 ZetaChain 向连接链发起合约调用或代币转账。

\- 通过这个机制，一个用户签名交易就能触发跨链多步操作。例如：比特币用户发送 BTC → ZetaChain 上的 Universal App 收到 → 转换 / 处理 → 再将资产发到 Ethereum 或 BNB 链。

\- Universal App 支持 “Gas 抽象”（gas abstraction）：

\- 来自连接链（source chain）的调用／转账时，只需要支付源链的 gas。

\- 如果 Universal App 要发起跨链调用或 withdraw，它需要 ZRC-20 gas 代币来支付目标链的 gas。

\- 因为 ZetaChain 的 Universal EVM 与标准 EVM 兼容，开发者可以继续用 Solidity + 现有工具（Hardhat、Foundry 等）开发，只需稍作修改即可获得跨链能力。

\- 总之，Universal App 是 ZetaChain 提供的一种 **跨链智能合约**，可以作为 “中心枢纽（hub）” 来协调多个链之间的资产和调用。

\---

## \## 2. Gateway 大概做什么

\- **Gateway** 是连接 ZetaChain 与各连接链（connected chains）之间的统一 “入口 / 桥” 接口。

\- 每条连接链（例如 Ethereum、Solana、Bitcoin）都有自己的 Gateway：

\- 对于 EVM 链，是一个智能合约。

\- 对于非 EVM 链（如 Bitcoin），是对应的 Gateway 程序 / 地址，由 ZetaChain 的 observer-signer validators 管理。

\- Gateway 的功能包括：

\- **接收（deposit）来自连接链的代币或 native gas**，然后发起调用到 Universal App。

\- **允许连接链用户调用 Universal App**，即使他们只在自己的链上操作，也能触发 ZetaChain 上的逻辑。

\- 在 ZetaChain 一端（Universal EVM 侧），Gateway 还负责：

\- 将 ZRC-20 代币 “withdraw” 回连接链（变回原生资产或 ERC-20）。

\- 发起对连接链的跨链合约调用`withdrawAndCall`）——也就是 Universal App 在 ZetaChain 上可以发起对目标链合同的调用并附带资金。

\- **错误／回退处理（revert）**：如果跨链调用失败（目标链上的调用发生 revert），Gateway 支持灵活的退款机制 — 可以把资产退回到用户地址或调用某个指定合约。

\- Gateway 本质上简化了开发者和最终用户在跨链场景下的交互逻辑：

\- 开发者只需要通过 Gateway 统一 API 与 Universal App 交互，不必为每条链写不同逻辑。

\- 用户从自己熟悉的链（钱包所在链）出发，就能无缝调用跨链应用，无需频繁切换网络。

\---

## \## 3. ZetaChain 架构与设计背景（简要）

\- ZetaChain 采用 **hub-and-spoke 模型**：

\- **Hub** 是 ZetaChain 本身，负责跨链协调和资产中转。

\- **Spokes** 是外部连接链（Ethereum、Solana、Bitcoin 等）。

\- 验证者（Validators）分为两类：

\- **Core Validators**：负责 ZetaChain 区块生产与共识。

\- **Observer-Signer Validators**：负责观察链上外部事件（如用户 deposit）并签名跨链交易。

\- ZetaChain 提供模块化架构（Cosmos SDK 模式），包括 CrossChain 模块、Fungible（ZRC-20）模块等。

\- 跨链交易的生命周期由 CrossChain 模块管理，从接收、验证、签名到最终执行或回退。

\---

## \## 4. 结论

\- **Universal App** 是 ZetaChain 提供的 “跨链兼容合约” 模式：一个合约可以同时服务多个链，处理跨链资产与调用。

\- **Gateway** 是连接各个链与 Universal App 的桥：它负责代币转入 (deposit)、跨链 call、Withdraw，以及错误回退处理。

\- 结合 ZetaChain 的 hub-and-spoke 架构与验证者系统，这套设计使构建跨链应用变得更简单、安全、可扩展。

\---
<!-- DAILY_CHECKIN_2025-11-26_END -->

# 2025-11-25
<!-- DAILY_CHECKIN_2025-11-25_START -->

# ZetaChain 开发精要文档

整理内容来自：

\- ZRC-20 标准

\- Universal Token / NFT

\- 跨链 Swap 教程

\- example-contracts 示例仓库

目标：

1\. 了解 ZRC-20 / Universal Token / Universal NFT

2\. 理解跨链 Swap / DeFi 基础流程

3\. 跑通官方 Demo

\---

## 1\. 核心资产标准

### 1.1 ZRC-20

ZetaChain 上的 ERC-20 增强版，支持跨链资产交互。

**特性：**

\- ERC-20 完全兼容

\- 支持跨链消息 & 跨链转账

\- 内置跨链 Gas 支付（gasToken）

\- 用于构建跨链 DeFi / Swap

\> 简单理解：跨链能力的 ERC-20。

\---

### 1.2 Universal Token

外链真实资产在 ZetaChain 上的统一表示。

**特点：**

\- 与 ERC-20 类似

\- 一个 Token 可被多个链共享

\- 用于跨链支付 / DeFi / 统一资产管理

\---

### 1.3 Universal NFT

一个 NFT 的跨链镜像。

\- 一次 mint，多链使用

\- 用于跨链游戏、身份、资产流通

\---

## 2\. 跨链 Swap / DeFi 的基本原理

跨链交互核心流程：

1\. 用户在链 A 调用 swap

2\. A 链合约通过 `zetaSend()` 发送跨链指令

3\. ZetaChain 中继器转发消息

4\. 链 B 合约收到 `onZetaMessage()` 回调

5\. 链 B 执行 swap / 转账

6\. 用户在链 B 收到资产

**关键函数：**

\- `zetaSend()`：发跨链消息

\- `onZetaMessage()`：链 B 回调

\- `zetaRevert()`：跨链失败回滚

\> 所有跨链 Swap 示例均基于这套机制。

\---

## 3\. 官方 Demo 实操指南（最短路径）

所有示例均来自 `example-contracts` 仓库。

\---

### 3.1 克隆仓库

```
git clone https://github.com/zeta-chain/example-contracts
```

```
cd example-contracts
```

```
npm install
```
<!-- DAILY_CHECKIN_2025-11-25_END -->
<!-- Content_END -->
