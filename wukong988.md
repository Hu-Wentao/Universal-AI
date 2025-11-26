---
timezone: UTC+8
---

# sue

**GitHub ID:** wukong988

**Telegram:** @Sue_muyu

## Self-introduction

web3独立开发者，曾编写过solana合约、套利等

## Notes

<!-- Content_START -->
# 2025-11-26
<!-- DAILY_CHECKIN_2025-11-26_START -->
# Swap 合约系统性分析

解决的核心问题

1\. 跨链流动性碎片化

传统 DeFi 中,不同链上的资产无法直接交换,用户需要:

\- 使用多个桥接协议

\- 在不同链上分别操作 DEX

\- 承担高额手续费和时间成本

2\. 复杂的跨链 gas 费管理

跨链操作需要目标链的 gas token,这个合约智能地:

\- 自动从交换数额中预留 gas 费用

\- 支持不同 gas token 的自动兑换

\- 确保交易能够在目标链成功执行

跨链交易失败处理

当目标地址无法接收 token 时(如合约地址),提供了 onRevert 机制自动退款。
<!-- DAILY_CHECKIN_2025-11-26_END -->

# 2025-11-25
<!-- DAILY_CHECKIN_2025-11-25_START -->

```
┌─────────────────────────────────────────────────────────────────┐
│                 从 Ethereum 到 BSC 的跨链调用                      │
└─────────────────────────────────────────────────────────────────┘

[用户钱包 - Ethereum]
     │ 调用: depositAndCall(
     │   receiver: 0xUniversalOnZetaChain,  ← 地址1
     │   message: encode(56, 0xConnectedOnBSC, "Hello")  ← 包含地址2
     │ )
     ▼
┌─────────────────────┐
│  Ethereum Chain     │
│  Connected 合约     │
└──────────┬──────────┘
           │ gateway.depositAndCall(...)
           ▼
     [Ethereum Gateway]
           │ 发出跨链事件
           │
    ┌──────┴──────┐
    │ ZetaChain   │
    │ 观察者网络   │
    └──────┬──────┘
           │ 共识验证
           ▼
┌─────────────────────┐
│  ZetaChain          │
│  Universal 合约     │ ← onCall() 被触发
└──────────┬──────────┘
           │ 1️⃣ decode(message)
           │    → targetChainId = 56
           │    → targetContract = 0xConnectedOnBSC
           │    → targetData = "Hello"
           │
           │ 2️⃣ gateway.withdrawAndCall(
           │       0xConnectedOnBSC,  ← 使用解析出的地址2
           │       ...
           │    )
           ▼
   [ZetaChain Gateway]
           │ 发出提取指令
           │
    ┌──────┴──────┐
    │ ZetaChain   │
    │ 观察者网络   │
    └──────┬──────┘
           │ 监控并执行
           ▼
     [BSC Gateway]
           │ executeRevert() 或 execute()
           ▼
┌─────────────────────┐
│  BSC Chain          │
│  Connected 合约     │ ← onCall() 接收消息
└──────────┬──────────┘
           │ 执行业务逻辑
           ▼
    [目标应用/用户]
```
<!-- DAILY_CHECKIN_2025-11-25_END -->

# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->


# ERC20和ZRC20：

## **ERC20：**

**ERC20** 是以太坊区块链上的一个**技术标准**。你可以把它理解为一种“代币制作规范”或“接口协议”。

在 ERC20 出现之前，每个人都可以在以太坊上发行代币，但彼此之间无法兼容。就像一个城市里，每家手机充电器接口都不同，非常混乱。ERC20 的出现，统一了所有代币的“接口”，使得所有代币都能在同一个生态系统（如钱包、交易所、DApp）中无缝使用。

**ERC = Ethereum Request for Comments**（以太坊意见征求稿），20 是提案编号。

## **ZRC20：**

**ZRC20** 是 **ZetaChain** 区块链上的一个代币标准。ZetaChain 是一个公共的、去中心化的 L1 区块链，其核心使命是成为**不同区块链之间的桥梁**。

ZRC20 标准**扩展并兼容了 ERC20**，并为其增加了强大的**原生跨链功能**。

2\. 主要功能和核心创新

ZRC20 代币继承了 ERC20 的所有功能（如 `transfer`, `balanceOf` 等），但最关键的是，它增加了**跨链存款和取款**的能力。

想象一下，一个 ZRC20 代币（比如 `ZRC20-USDT`）就像是 USDT 的一个“万能版本”，它可以在多条链上流通。

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/wukong988/images/2025-11-24-1763990533632-image.png)
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->
