---
timezone: UTC+8
---

# Louis

**GitHub ID:** LouisCanBe

**Telegram:** @louiscanbe

## Self-introduction

掌握前端nextjs，ts等开发，熟练应用ai辅助开发，有web项目上线能力；常用过claudecode、warp、cursor、aistudio等coding工具。了解过区块链基础内容，从上次黑客松关注到残酷共学。研究方向某垂直方向agentic system应用开发，目前AI产品实习中。

## Notes

<!-- Content_START -->
# 2025-11-26
<!-- DAILY_CHECKIN_2025-11-26_START -->
## 1\. 理解 “通用区块链 / Universal EVM / Universal App / Omnichain Smart Contract” 的基本含义。

**通用区块链 (Universal Blockchain) / ZetaChain** ZetaChain 是一个建立在 Cosmos SDK 和 Comet BFT 共识引擎之上的 **PoS 区块链**。ZetaChain 的核心目标是提供基础设施，使开发者能够创建可与**任何区块链**（包括像 Bitcoin 这样的非智能合约区块链、以及 Ethereum、Solana、TON 等）**无缝交互**的通用应用程序。ZetaChain 通过内置的全链互操作性功能，将多样化的区块链生态系统统一在一个单一的开发框架之下。

**Universal EVM (通用 EVM)** Universal EVM (通用 EVM) 是 ZetaChain 上的一个 **智能合约平台**，它内置了**全链互操作性功能**，从而能够开发通用应用。它也被称为通用以太坊虚拟机 (UEVM)。它扩展了标准的 EVM，使其具备全链功能，并且与 Ethereum 的 EVM 完全兼容，允许开发者使用 Solidity 或其他 EVM 兼容语言编写智能合约。此外，ZetaChain 提供了**无 Gas 的 EVM 执行环境**，这意味着当通用应用被连接链上的用户调用时，只需在连接链上支付 Gas，而在 ZetaChain 上的执行不会产生额外费用。

**Universal App (通用应用) / Omnichain Smart Contract (全链智能合约)** 通用应用是部署在 ZetaChain 上的一个**智能合约**，它**原生连接**到其他区块链，例如 Ethereum、BNB 和 Bitcoin。

**特点：**

-   它可以接收来自**任何连接链**的合约调用、消息和代币转移。
    
-   它可以触发对连接链的合约调用和代币转移。
    
-   通用应用能够**协调**跨越多链的复杂多步骤交易和价值转移，只需用户签署一次交易即可触发。
    
-   一旦部署在 ZetaChain 上，它会自动连接到 ZetaChain 生态系统中的所有网络，并且随着新区块链的加入，它会自动获得兼容性，无需修改合约源代码（**前向兼容性**）。
    
-   它能够通过**原生代币**（而非包装或合成版本）在所有连接链之间转移价值。
    

## 2\. 实践 / 作业：用自己的话写出定义

**○ Universal App 是什么？通用应用**是部署在 ZetaChain 的 **Universal EVM** 上的智能合约。它具有**全链互操作性**，这意味着它能直接接收来自任何外部连接的区块链（包括 EVM 链、Solana、Bitcoin 等）的消息、代币和合约调用。通用应用不仅能接收信息，还能向这些连接链发起调用或转移代币，从而实现从一个合约协调跨越多个区块链的复杂交易。

**○ Gateway 大概做什么？Gateway (网关)** 是用户或合约与 ZetaChain 上的通用应用进行交互的**单一入口点**。每个连接链上都会部署一个 Gateway 合约。它的主要功能包括：

1.  **接收存款和调用：** Gateway 合约暴露了方法，允许用户将代币存入通用应用并调用它们。例如，以太坊用户通过 Gateway 发送 ETH 和消息到通用应用。Bitcoin 用户只需将 BTC 和数据发送到 **Gateway 地址**即可调用通用应用。
    
2.  **代币和调用流出：** Gateway 也用于通用应用向连接链**提取代币**和**发起合约调用**。
    

## 3\. 画一张简单的架构图

**ZetaChain 架构简图描述：ZetaChain 中心 + 多条公链 + Gateway**

在 ZetaChain 的架构中，**ZetaChain 协议**位于中心，扮演着协调者的角色，并运行 **Universal EVM**。

1.  **中心 (ZetaChain Core):**
    

-   **ZetaChain (PoS 区块链):** 运行 Universal EVM 和 通用应用 (Universal Apps)。
    
-   **ZetaChain 验证者 (Validators):** 包含 ZetaCore 和 ZetaClient。**观察者-签名者 (Observer-Signer Validators)** 是一组关键的参与者，他们持续观察连接链上的相关事件/状态，并集体持有密钥，以便代表 ZetaChain 对连接链进行认证交互（签名出站交易）。
    

2.  **连接者 (Gateway Contracts / Addresses):**
    

-   在每一条连接的外部公链上，都部署了 **Gateway 合约**（或提供 Gateway 地址，如在 Bitcoin 网络上）。Gateway 是用户与 ZetaChain 上的通用应用交互的**入口点**。
    

3.  **外围链 (Connected Chains):**
    

这些是 ZetaChain 互操作的目标链，包括：

-   **EVM 兼容链:** Ethereum、BNB、Polygon、Base 等。
    
-   **非 EVM 链:** Solana、TON、Sui。
    
-   **非智能合约链:** Bitcoin。
    

**数据/调用流向描述：**

-   **入站流 (Connected Chain -> ZetaChain):** 外部链上的用户通过与该链上的 **Gateway 合约**交互，发起代币存入和通用应用调用。这些事件随后被 ZetaChain 的**观察者**捕获，并在 ZetaChain 上触发通用应用的执行。
    
-   **出站流 (ZetaChain -> Connected Chain):** 通用应用通过调用 ZetaChain 上的协议合约，指示 ZetaChain 的**观察者-签名者**，代表 ZetaChain 签署一笔交易，对目标连接链（如 Ethereum 或 BNB Chain）发起合约调用或代币提取。
    

![screenshot-20251126-235044.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/LouisCanBe/images/2025-11-26-1764172264865-screenshot-20251126-235044.png)![screenshot-20251126-235459.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/LouisCanBe/images/2025-11-26-1764172513162-screenshot-20251126-235459.png)
<!-- DAILY_CHECKIN_2025-11-26_END -->

# 2025-11-25
<!-- DAILY_CHECKIN_2025-11-25_START -->


了解了qwen，zetachain的部署使用，llm api调用没问题，链相关的内容还没太搞懂
<!-- DAILY_CHECKIN_2025-11-25_END -->

# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->



已加入社区，能正常访问页面。

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/LouisCanBe/images/2025-11-23-1763921560977-image.png)
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->
