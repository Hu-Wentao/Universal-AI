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
