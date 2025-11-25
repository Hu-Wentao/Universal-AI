---
timezone: UTC+8
---

# diandian

**GitHub ID:** diandian42

**Telegram:** @diandian

## Self-introduction

学习AI和web3的新人

## Notes

<!-- Content_START -->
# 2025-11-25
<!-- DAILY_CHECKIN_2025-11-25_START -->
# **ZetaChain 跨链调用项目 - 使用分析报告**

## **📋 项目简介**

这是一个 ZetaChain 跨链调用示例项目，演示了如何在 EVM 链、Solana 和 Sui 之间进行跨链操作，包括跨链调用、资产转移和错误处理。

## **🏗️ 项目结构**

```
call/
├── contracts/          # Solidity 智能合约
│   ├── Connected.sol   # 外部链合约（EVM）
│   └── Universal.sol   # ZetaChain 中心合约
├── commands/           # CLI 命令行工具
│   ├── connected/      # Connected 合约操作
│   ├── universal/      # Universal 合约操作
│   └── deploy.ts       # 部署脚本
├── solana/             # Solana 链代码
├── sui/                # Sui 链代码
└── test/               # 测试用例
```

## **🚀 快速开始**

### **1\. 环境准备**

```
# 安装依赖
yarn install
​
# 编译合约
npx hardhat compile
```

### **2\. 部署合约**

**部署 Universal 合约（ZetaChain）**

```
npx tsx commands/index.ts deploy \
  --name Universal \
  --rpc https://zetachain-athens-evm.blockpi.network/v1/rpc/public \
  --private-key YOUR_PRIVATE_KEY \
  --gateway 0x6c533f7fe93fae114d0954697069df33c9b74fd7
```

**部署 Connected 合约（外部 EVM 链）**

```
npx tsx commands/index.ts deploy \
  --name Connected \
  --rpc YOUR_EVM_RPC_URL \
  --private-key YOUR_PRIVATE_KEY \
  --gateway GATEWAY_ADDRESS
```

## **💡 核心功能使用**

### **一、Connected 合约操作（外部链 → ZetaChain）**

**1\. 跨链调用（Call）**

从外部 EVM 链调用 ZetaChain 上的 Universal 合约：

```
npx tsx commands/index.ts connected call \
  --contract CONNECTED_CONTRACT_ADDRESS \
  --receiver UNIVERSAL_CONTRACT_ADDRESS \
  --types '["string"]' \
  --values '["Hello ZetaChain"]' \
  --rpc YOUR_EVM_RPC_URL \
  --private-key YOUR_PRIVATE_KEY
```

**功能说明：**

-   从外部链发起跨链调用
    
-   调用 ZetaChain 上的 Universal 合约的 `onCall()` 函数
    
-   不涉及资产转移，仅传递消息
    

**2\. 存款（Deposit）**

将原生代币（如 ETH）存入 ZetaChain：

```
npx tsx commands/index.ts connected deposit \
  --contract CONNECTED_CONTRACT_ADDRESS \
  --receiver UNIVERSAL_CONTRACT_ADDRESS \
  --amount 0.1 \
  --rpc YOUR_EVM_RPC_URL \
  --private-key YOUR_PRIVATE_KEY
```

**功能说明：**

-   将原生代币转换为 ZRC20 代币
    
-   代币会出现在 ZetaChain 上的 Universal 合约地址
    
-   支持原生代币和 ERC20 代币
    

**3\. 存款并调用（Deposit and Call）**

存款的同时执行跨链调用：

```
npx tsx commands/index.ts connected deposit-and-call \
  --contract CONNECTED_CONTRACT_ADDRESS \
  --receiver UNIVERSAL_CONTRACT_ADDRESS \
  --amount 0.1 \
  --types '["string"]' \
  --values '["Hello"]' \
  --rpc YOUR_EVM_RPC_URL \
  --private-key YOUR_PRIVATE_KEY
```

**功能说明：**

-   一次性完成存款和调用操作
    
-   适合需要同时转移资产和执行逻辑的场景
    

### **二、Universal 合约操作（ZetaChain → 外部链）**

**1\. 跨链调用（Call）**

从 ZetaChain 调用外部链上的 Connected 合约：

```
npx tsx commands/index.ts universal call \
  --contract UNIVERSAL_CONTRACT_ADDRESS \
  --receiver CONNECTED_CONTRACT_ADDRESS \
  --zrc20 ZRC20_TOKEN_ADDRESS \
  --types '["string"]' \
  --values '["Hello EVM"]' \
  --function "hello(string)" \
  --call-options-gas-limit 500000 \
  --rpc ZETACHAIN_RPC_URL \
  --private-key YOUR_PRIVATE_KEY
```

**参数说明：**

-   `--zrc20`: 用于支付 gas 费的 ZRC20 代币地址
    
-   `--function`: 可选，指定要调用的函数（任意调用模式）
    
-   `--call-options-is-arbitrary-call`: 启用任意函数调用
    

**2\. 提款（Withdraw）**

从 ZetaChain 提款到外部链：

```
npx tsx commands/index.ts universal withdraw \
  --contract UNIVERSAL_CONTRACT_ADDRESS \
  --receiver CONNECTED_CONTRACT_ADDRESS \
  --amount 0.1 \
  --zrc20 ZRC20_TOKEN_ADDRESS \
  --rpc ZETACHAIN_RPC_URL \
  --private-key YOUR_PRIVATE_KEY
```

**功能说明：**

-   将 ZRC20 代币转换回原生代币
    
-   代币会发送到目标链上的指定地址
    
-   自动处理 gas 费（可能使用不同的代币）
    

**3\. 提款并调用（Withdraw and Call）**

提款的同时执行跨链调用：

```
npx tsx commands/index.ts universal withdraw-and-call \
  --contract UNIVERSAL_CONTRACT_ADDRESS \
  --receiver CONNECTED_CONTRACT_ADDRESS \
  --amount 0.1 \
  --zrc20 ZRC20_TOKEN_ADDRESS \
  --types '["string"]' \
  --values '["Hello"]' \
  --call-options-gas-limit 500000 \
  --rpc ZETACHAIN_RPC_URL \
  --private-key YOUR_PRIVATE_KEY
```

## **⚙️ 高级选项**

### **错误处理配置**

所有命令都支持错误处理选项：

```
--call-on-revert              # 是否在回滚时调用 onRevert
--revert-address ADDRESS      # 回滚处理合约地址
--abort-address ADDRESS       # 中止处理合约地址
--revert-message "message"    # 自定义回滚消息
--on-revert-gas-limit 500000  # 回滚调用的 gas 限制
```

### **示例：带错误处理的调用**

```
npx tsx commands/index.ts connected call \
  --contract CONNECTED_ADDRESS \
  --receiver UNIVERSAL_ADDRESS \
  --types '["string"]' \
  --values '["Test"]' \
  --call-on-revert \
  --revert-address CONNECTED_ADDRESS \
  --revert-message "Custom error message" \
  --rpc RPC_URL \
  --private-key PRIVATE_KEY
```

## **🔄 典型使用流程**

### **场景 1：跨链消息传递**

```
1. 部署 Connected 合约到外部链（如 Ethereum）
2. 部署 Universal 合约到 ZetaChain
3. 从外部链调用：connected call → Universal.onCall()
4. 从 ZetaChain 调用：universal call → Connected.onCall()
```

### **场景 2：跨链资产转移**

```
1. 存款：connected deposit → 资产转换为 ZRC20
2. 在 ZetaChain 上使用资产
3. 提款：universal withdraw → ZRC20 转换回原生代币
```

### **场景 3：跨链 DeFi 操作**

```
1. 存款并调用：connected deposit-and-call
   → 资产转移到 ZetaChain + 执行 DeFi 操作
2. 提款并调用：universal withdraw-and-call
   → 资产转回外部链 + 执行最终操作
```

## **🧪 运行测试**

```
# 使用 Foundry 运行测试
forge test --match-path "test/CallTest.t.sol" -vvv

# 测试覆盖的功能：
# - EVM ↔ ZetaChain 双向调用
# - 原生代币和 ERC20 存款
# - 提款功能
# - 错误处理和回滚
```

## **📝 注意事项**

NaN.  **Gas 费处理**
      
      -   Universal 合约操作需要 ZRC20 代币支付 gas 费
          
      -   系统会自动计算并处理 gas 费
          
NaN.  **地址格式**
      
      -   EVM 链：使用 0x 开头的地址
          
      -   Solana：使用 base58 编码的地址
          
      -   Sui：使用 0x 开头的地址（Move 格式）
          
NaN.  **消息编码**
      
      -   使用 ABI 编码传递参数
          
      -   支持任意函数调用（通过 `--function` 参数）
          
NaN.  **错误处理**
      
      -   配置 `onRevert` 处理调用失败
          
      -   配置 `onAbort` 处理中止场景
          
      -   支持自定义回滚消息
          

## **🔗 相关资源**

-   [ZetaChain 官方文档](https://www.zetachain.com/docs)
    
-   [教程链接](https://www.zetachain.com/docs/developers/tutorials/call)
    
-   协议合约：`@zetachain/protocol-contracts`
    

## **📊 命令总结**

| 操作 | 命令 | 方向 | 说明 |
| --- | --- | --- | --- |
| 调用 | connected call | 外部链 → ZetaChain | 纯消息传递 |
| 存款 | connected deposit | 外部链 → ZetaChain | 资产转移 |
| 存款+调用 | connected deposit-and-call | 外部链 → ZetaChain | 资产+消息 |
| 调用 | universal call | ZetaChain → 外部链 | 纯消息传递 |
| 提款 | universal withdraw | ZetaChain → 外部链 | 资产转移 |
| 提款+调用 | universal withdraw-and-call | ZetaChain → 外部链 | 资产+消息 |

* * *

**提示：** 使用前请确保已正确配置 RPC 节点和私钥，并在测试网络上进行充分测试。
<!-- DAILY_CHECKIN_2025-11-25_END -->

# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->

# **ZetaChain EVM 核心工具速查表**

| 工具 / 组件名称 | 核心用途 | 调用 / 使用方式 |
| --- | --- | --- |
| Cosmos SDK + CometBFT + Cosmos EVM | 底层技术栈，提供模块化架构、快速最终性（~4 秒）、全 EVM 兼容性 | 无需手动调用，开发时直接受益（合约无需修改即可部署） |
| ZetaChain CLI | 本地环境搭建、合约部署、跨链交易调用、测试网账号管理 | 终端执行命令（如 npx hardhat localnet npx hardhat account） |
| Localnet | 本地多链模拟环境，测试跨链合约 / 交易（支持 EVM、Solana、Sui 等链） | 通过 CLI 启动（npx hardhat localnet），本地调试无需依赖公网测试网 |
| Gateway 合约 | 跨链交互统一入口（入链 / 出链）：处理存款、跨链调用、资产 mint/burn | 合约调用（如 EVM 链调用 GatewayEVM，ZetaChain 侧调用 GatewayZEVM） |
| ZRC-20 标准 | 跨链代币标准，映射多链资产（如 BTC、SOL），兼容 ERC-20 接口 | 合约开发时遵循标准，通过 Fungible 模块部署或调用已有 ZRC-20 合约 |
| ContractRegistry | 存储协议合约（网关、ZRC-20）元数据和地址，避免调用错误 | 链上查询（通过 RPC 或 Explorer），开发时直接引用注册的合约地址 |
| CrossChain 模块 | 管理跨链交易（CCTX）生命周期，跟踪交易状态（待入链 / 待出链 / 已完成） | 无需手动调用，跨链交易时自动触发，可通过 API/Explorer 查询交易状态 |
| Fungible 模块 | 部署 ZRC-20 代币、管理跨链资产存款和流动性 | 合约调用（如存款、 mint 代币），或通过 CLI 间接触发 |
| Observer 模块 | 协调验证者完成跨链事件观测、投票，保障交易安全性 | 底层自动运行，开发者无需干预，仅需关注交易是否通过验证 |
| RPC 节点 | 连接测试网 / 主网，发送交易、查询链上数据（如账户余额、交易记录） | 通过 API 调用（如 Postman、代码中集成），需记录官方 RPC 入口 |
| Faucet 工具 | 领取测试网 ZETA 代币，用于支付跨链交易 Gas 费 | 访问官方 Faucet 页面或通过 CLI 命令（npx hardhat faucet）领取 |
| Explorer 浏览器 | 查询跨链交易状态、合约部署记录、账户明细，用于调试和验证 | 访问官方 Explorer 页面，输入交易哈希 / 合约地址查询 |
| Threshold Signature Scheme（TSS） | 验证者协同签名跨链交易，避免私钥单点风险 | 底层自动执行，开发者无需操作，仅需确保交易通过 TSS 签名验证 |

  
今天刚刚看ZetaChain的文档有点懵，所以想先把涉及到的工具整理一份出来。
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->
