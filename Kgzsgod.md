---
timezone: UTC+8
---

# K9z4g0d

**GitHub ID:** Kgzsgod

**Telegram:** @kgzsgod

## Self-introduction

大四计算机在读，熟悉区块链基础概论，以及DeFi等区块链扩展应用，希望可以在此次共学中学到知识

## Notes

<!-- Content_START -->
# 2025-11-25
<!-- DAILY_CHECKIN_2025-11-25_START -->
## 部署在本地的universal合约

```Solidity
npx zetachain localnet start
```

使用如上终端命令，打开zetachain的anvil本地测试环境

在命令行中输入`forge build`编译foundry项目中的Universal合约

在输入如下命令将Universal合约部署上链

```Shell
forge create Universal \
  --rpc-url http://127.0.0.1:8545 \
  --private-key $PRIVATE_KEY \
  --broadcast
[⠊] Compiling...
No files changed, compilation skipped
Deployer: 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
Deployed to: 0x5bf5b11053e734690269C6B9D438F8C9d48F528A
Transaction hash: 0x57d6b6f7efdec82004cc021f837e2d7bee84a92e477d5c6f3e6a0817033f68c2
```

可以看到已经完成部署上链，发送方和接收方的地址以及交易的哈希

Universal合约就是实现了当其他链通过zetachain跨链调用这个合约时，他会解码传入的内容，并触发打印名字的事件（并没有实际资产转移，只单纯输出消息）

## 部署在测试网的Universal合约

首先先将zetachain testnet添加到metamask中

![](https://xvadt6dwbiv.feishu.cn/space/api/box/stream/download/asynccode/?code=M2Q2ODI3NWIxN2FjYjc3MGQ5OWQ0OGFhYTJlYjRlMzhfeDdQdThONkRuSXd3a2RUNVhKZkRjYkE2R0FhTXZTV3BfVG9rZW46TjJmSWJ0WVJub2ZReWl4Zkh0bmN0OEJCbkZKXzE3NjQwNzU5OTU6MTc2NDA3OTU5NV9WNA)

[https://zetachain.faucetme.pro/](https://zetachain.faucetme.pro/)

通过官方水龙头获取zeta代币，然后将私钥改成测试网地址的私钥，在输入如下命令即可将Universal合约部署在测试网上

```Shell
forge create Universal \
  --rpc-url https://zetachain-athens-evm.blockpi.network/v1/rpc/public \
  --private-key $PRIVATE_KEY \
  --broadcast \
  --json

{
  "deployer": "0xAa79ED23Adf4A21fE58736d60fEEcec17BD9E33B",
  "deployedTo": "0x525087bA0FF1f84c8E93846f1D0fC7D5709D37Af",
  "transactionHash": "0x64680383161a811a369e60adaaf34f0b7bcdbba1f725642ea3cee212e66c83d0"
}
```

得到的交易哈希可以从区块链浏览器中查到[https://testnet.zetascan.com/](https://testnet.zetascan.com/)

![](https://xvadt6dwbiv.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTY3YTZlYjg5N2NjYWRjNTFhNTZiZjA5ZThjYzljNzlfdk56TEVadk9JdFQ4NHNvVTQ4STBlS1h6UjlrRW44SnhfVG9rZW46WTFWdWJRTmttbzVrR0N4b0xXbGN1dVhUbmplXzE3NjQwNzU5OTU6MTc2NDA3OTU5NV9WNA)
<!-- DAILY_CHECKIN_2025-11-25_END -->

# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->

搭建了zetachain的cli环境

阅读了zetachain的官方文档并搜索了相关资料，理清了他的逻辑

zetachian并不是传统意义上的桥接跨链，而是通过在zetachain上部署智能合约，实现从一个链到另一个链的操作

比如现在我想要从比特币链上转账btc到以太坊链上，我只需要在zetachain上部署执行转账合约，此时中间的过程：

1.  比特币链触发转账操作
    
2.  zetachain链监听到该交易
    
3.  zetachain链节点达成共识
    
4.  执行跨链转账合约逻辑
    
5.  生成转账交易
    

对比传统跨链来说确实有优势，速度快延迟短，也不需要考虑各种跨链fee
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->
