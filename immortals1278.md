---
timezone: UTC+8
---

# 1mmortals

**GitHub ID:** immortals1278

**Telegram:** @gzh1219c137

## Self-introduction

tg写的微信号

## Notes

<!-- Content_START -->
# 2025-11-25
<!-- DAILY_CHECKIN_2025-11-25_START -->
RPC 让app连接到测试网：[https://zetachain-athens-evm.blockpi.network/v1/rpc/public](https://zetachain-athens-evm.blockpi.network/v1/rpc/public)

Faucet 领测试币：[https://zetachain.faucetme.pro/](https://zetachain.faucetme.pro/)

Explorer 用于查看链上信息：[https://zetachain-athens.blockpi.network/](https://zetachain-athens.blockpi.network/)

## gateway

部署在zetachain和与zetachain连接的链上的一系列智能合约，用于向zetachain中存款/收款。

存款：原生代币发到安全托管合约，zetachain铸造ZRC-20（若从没铸造过要先部署一个新的ZRC-20合约）并发送给特定地址，取款同理。

call：在源链上调用gateway的send函数->调用zetachain上通用合约的onCrossChainCall函数执行任意逻辑（如交换、质押、铸造NFT等）

## gas费

入站调用用原生代币支付，仅支付源链的原生 Gas 费

出站调用需用zrc20支付取款费用，出站时ZetaChain 的验证者需要动用他们自己持有的目标链原生代币（如 ETH、BNB）来为你支付目标链上的 Gas 费。这笔费用就是为了补偿他们。
<!-- DAILY_CHECKIN_2025-11-25_END -->

# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->




## zetachain

在ZetaChain上部署一次应用，就能自动连接到其生态中的所有区块链。未来当ZetaChain支持新的链时，应用自动获得与该新链交互的能力，无需修改或重新部署代码

ZetaChain的核心是通用以太坊虚拟机，完全兼容EVM。

zetachain本身的执行免gas费
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->
