---
timezone: UTC+8
---

# 黄文晔

**GitHub ID:** Eeeeye

**Telegram:** @Eeeeye

## Self-introduction

大三

## Notes

<!-- Content_START -->
# 2025-11-26
<!-- DAILY_CHECKIN_2025-11-26_START -->
## **今天的关键概念**

**通用区块链（Universal Blockchain）** 像 ZetaChain 这样的 L1，它自己就是一条链，但天生可以直接连很多其他链（Bitcoin / Ethereum / Solana 等），从一个中心统一管理不同链上的资产和调用。

直观理解：

-   一条专门用来“打通所有链”的 L1 公链，你可以把它想成“多链世界的操作系统”或“总控制台”。
    
-   它本身是一个 PoS L1（基于 Cosmos SDK），但内嵌了跨链能力，可以原生连接 Ethereum、Bitcoin、Solana 等各种链，包括没有智能合约的链（如 BTC）。\[
    

在实际应用中的作用：

-   对用户：只和 ZetaChain 打交道，却能在背后同时操作多条链上的资产和合约——不用频繁切网络、桥资产。
    
-   对开发者：只在一个地方（ZetaChain）写逻辑，就能控制多链资产/合约，相当于“只写一次，多链生效”。
    

**Universal EVM（通用 EVM）** ZetaChain 上的 EVM 版本。对开发者看起来像普通 EVM（Solidity、工具都能用），但它内置跨链能力：合约可以直接收、发来自其他链的消息和资产。

在实际应用中的作用：

-   开发者仍然写 Solidity，但多了“跨链能力”，比如：
    
    -   在一个合约函数里，同时读取 Ethereum 上某个池子的状态 + 操作 Bitcoin 资产 + 最终把结果发到 Solana 上。
        
    -   它是“通用应用 / Universal Apps”真正跑的执行环境。
        

**Omnichain Smart Contract（全链智能合约）**

部署在 ZetaChain 的合约，但可以操作“任意已连接链上的资产和数据”，所以叫 Omnichain。\[

与普通合约的对比：

-   普通合约：
    
    -   部署在哪条链，只能管理这条链上的状态和资产。
        
-   Omnichain 合约：
    
    -   部署在 ZetaChain 上，却能：
        
        -   管理 Ethereum、Bitcoin 等链上的资金金库；
            
        -   对这些链发交易（如调用 Uniswap、借贷协议等）；
            
        -   统一编排多链操作流程。
            

在实际应用中的作用：

-   大幅减少开发复杂度：
    
    -   过去：每条链部署一份合约 + 自己写消息传递/安全逻辑；
        
    -   现在：只要在 ZetaChain 部署一份 Omnichain 合约，由 ZetaChain 处理跨链消息与安全。
        
-   应用场景：跨链 DEX、跨链借贷、用 BTC 参与 DeFi 等。
    

**Universal App（通用应用）**

官方/代码层面的定义：

-   “Universal App 是部署在 ZetaChain 上、并且原生连接到其他区块链（Ethereum、BNB、Bitcoin 等）的智能合约（App）。”
    
-   这些应用通过 Gateway 接受来自各条链的调用和资产，统一在 ZetaChain 内部处理，再可以向外发起跨链操作。
    

具体例子（帮助理解应用价值）：

1）跨链支付 / 汇款

-   用户：只在 Bitcoin 钱包里签一笔交易，给某个 Universal App。
    
-   App：
    
    -   接收 BTC；
        
    -   在 ZetaChain 上把 BTC 换成 ZRC-20 USDC；
        
    -   再通过 Gateway 把 USDC 以原生 USDC 形式发到 Ethereum 的某个地址。
        

2）跨链 DEX / 聚合器

-   用户：在一个页面上输入“用 SOL 换成 Base 上的 ETH”；
    
-   Universal App：
    
    -   从 Solana 接收 SOL；
        
    -   中间可能经过多条链/多次 swap；
        
    -   最终在 Base 上把 ETH 打给用户；
        
    -   用户眼里只是一键 swap。
        

3）跨链借贷 / 做多

-   用 BTC 作为抵押，在多个 EVM 链上借出稳定币，再去做策略、挖矿，最后统一结算。
    

**Gateway** Gateway 是「入口 + 出口」：

-   在每一条外部链上（例如 Ethereum / Solana / Bitcoin），都有一个对应的 Gateway：
    
    -   EVM 链上是一个 Gateway 合约；
        
    -   Solana 上是一个 Gateway program；
        
    -   Bitcoin 上是一个由验证者共同管理的多签地址。 这些 Gateway 负责接收用户的交易，把“我要调用哪个 Universal App、要带多少代币、要执行什么操作”等信息传入 ZetaChain。
        
-   在 ZetaChain 链上也有一个 Gateway 合约：
    
    -   它负责把 Universal App 的指令执行到外部链上，比如：从 ZetaChain 把 ZRC-20 代币提到 Ethereum 变成原生 ETH，并且顺便在 Ethereum 上调用一个合约函数。
        

**各个概念之前的关系**

外围链用户/合约 → 各自链的 Gateway → ZetaChain（Universal Blockchain） → Universal EVM → Omnichain 合约 → Universal App → 再通过 Gateway 操作各外链资产和合约。

## **架构图**

```
                 [Bitcoin 链]
                      |
                 [Gateway-BTC]
                      |
[Solana 链] -- [Gateway-Solana]   [Ethereum 链] -- [Gateway-ETH]
                      \            /
                       \          /
                        \        /
                      [   ZetaChain   ]
                      [ Universal EVM ]
                      [ Universal Apps ]
                        /        \
                       /          \
          [Gateway-Zeta → 其它链调用/提币 ...]
​
```

## **拓展资料学习**

**1\. 为什么在 ZetaChain 上开发** 在我看来，在 ZetaChain 上开发的意义在于，它把多条区块链整合成一个统一的应用平台。我只需要在 ZetaChain 的 Universal EVM 上写一份合约，就可以同时调度 Bitcoin、Ethereum、Solana 等不同链上的资产和状态，而不用在每条链上分别部署合约、维护多套跨链桥逻辑，这大大降低了开发和安全成本。对用户而言，只需在自己熟悉的钱包和链上发起操作，后台由 ZetaChain 自动完成跨链路由和结算，使多链使用体验尽量接近“用一个应用、面对一个界面”的单链体验。

**2\. ZetaChain 架构设计概览** 我理解的 ZetaChain 架构是：以一条 PoS 公链为中心，在链上运行 Universal EVM 和 omnichain 合约，由验证人网络去观察外部区块链的事件，并通过各链上的 Gateway 完成资产和消息的跨链转发。外部资产会在 ZetaChain 上被映射成统一标准的代币，这样合约可以像操作本地资产一样统一管理多链资金。整体上它采用“中心 Hub + 多条辐射链”的模式，把复杂的多对多跨链关系简化为一条主链与多条外链的连接，为上层的 Universal App 提供一个简单而统一的多链基础设施。
<!-- DAILY_CHECKIN_2025-11-26_END -->

# 2025-11-25
<!-- DAILY_CHECKIN_2025-11-25_START -->

## **Getting start（CLI）**

测试官网的运行指令（在本地跑起3条链）：

```
 zetachain localnet start                                                                                                        ✔  21:32:50 
[LOCALNET] Starting anvil on port 8545 with args: -q
[LOCALNET] Skipping Ton...
[LOCALNET] Skipping Solana...
[LOCALNET] Skipping Sui...
[LOCALNET] EVM default wallet address: 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
[LOCALNET] EVM default wallet private key: 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80
[LOCALNET] Default wallet mnemonic: test test test test test test test test test test test junk
​
Ethereum (11155112)
┌───────────────┬────────────────────────────────────────────┐
│ Contract      │ Address                                    │
├───────────────┼────────────────────────────────────────────┤
│ erc20Custody  │ 0xa85233C63b9Ee964Add6F2cffe00Fd84eb32338f │
├───────────────┼────────────────────────────────────────────┤
│ gateway       │ 0x09635F643e140090A9A8Dcd712eD6285858ceBef │
├───────────────┼────────────────────────────────────────────┤
│ zetaConnector │ 0x67d269191c92Caf3cD7723F116c85e6E9bf55933 │
├───────────────┼────────────────────────────────────────────┤
│ zetaToken     │ 0x7a2088a1bFc9d81c55368AE168C2C02570cB814F │
├───────────────┼────────────────────────────────────────────┤
│ USDC.ETH      │ 0x1fA02b2d6A771842690194Cf62D91bdd92BfE28d │
└───────────────┴────────────────────────────────────────────┘
​
​
ZetaChain (31337)
┌───────────────────┬────────────────────────────────────────────┐
│ Contract          │ Address                                    │
├───────────────────┼────────────────────────────────────────────┤
│ gateway           │ 0xB7f8BC63BbcaD18155201308C8f3540b07f84F5e │
├───────────────────┼────────────────────────────────────────────┤
│ uniswapV2Factory  │ 0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512 │
├───────────────────┼────────────────────────────────────────────┤
│ uniswapV2Router02 │ 0x9fE46736679d2D9a65F0992F2272dE9f3c7fa6e0 │
├───────────────────┼────────────────────────────────────────────┤
│ uniswapV3Factory  │ 0xCf7Ed3AccA5a467e9e704C703E8D87F634fB0Fc9 │
├───────────────────┼────────────────────────────────────────────┤
│ uniswapV3Router   │ 0xa513E6E4b8f2a923D98304ec87F64353C4D5C853 │
├───────────────────┼────────────────────────────────────────────┤
│ zetaToken         │ 0x5FbDB2315678afecb367f032d93F642f64180aa3 │
├───────────────────┼────────────────────────────────────────────┤
│ ZRC-20 ETH.ETH    │ 0x2ca7d64A7EFE2D62A725E2B35Cf7230D6677FfEe │
├───────────────────┼────────────────────────────────────────────┤
│ ZRC-20 USDC.ETH   │ 0xd97B1de3619ed2c6BEb3860147E30cA8A7dC9891 │
├───────────────────┼────────────────────────────────────────────┤
│ ZRC-20 BNB.BNB    │ 0x65a45c57636f9BcCeD4fe193A602008578BcA90b │
├───────────────────┼────────────────────────────────────────────┤
│ ZRC-20 USDC.BNB   │ 0x05BA149A7bd6dC1F937fA9046A9e05C05f3b18b0 │
└───────────────────┴────────────────────────────────────────────┘
​
​
BNB (98)
┌───────────────┬────────────────────────────────────────────┐
│ Contract      │ Address                                    │
├───────────────┼────────────────────────────────────────────┤
│ erc20Custody  │ 0x70e0bA845a1A0F2DA3359C97E0285013525FFC49 │
├───────────────┼────────────────────────────────────────────┤
│ gateway       │ 0x0E801D84Fa97b50751Dbf25036d067dCf18858bF │
├───────────────┼────────────────────────────────────────────┤
│ zetaConnector │ 0x9d4454B023096f34B160D6B654540c56A1F81688 │
├───────────────┼────────────────────────────────────────────┤
│ zetaToken     │ 0x99bbA657f2BbC93c02D617f8bA121cB8Fc104Acf │
├───────────────┼────────────────────────────────────────────┤
│ USDC.BNB      │ 0xf953b3A269d80e3eB0F2947630Da976B896A8C5b │
└───────────────┴────────────────────────────────────────────┘
​
```

在shell中创建自己的钱包

```
npx zetachain accounts create --name mywallet                                                                            
Creating accounts for all supported types...
EVM account created successfully!
Key saved to: /home/eeeeye/.zetachain/keys/evm/mywallet.json
Address: 0x784f02F6a80c0D2Dc8485b9F05Ce2A549EDa60A3
SOLANA account created successfully!
Key saved to: /home/eeeeye/.zetachain/keys/solana/mywallet.json
Address: GNPPUzwT1jn4VroozW7BoPr2XdvMBXtgXD1aFLTUDZiG
SUI account created successfully!
Key saved to: /home/eeeeye/.zetachain/keys/sui/mywallet.json
Address: 0x98aec9ebf7d1797313c7e863e4ef4e7f89c7e87286f1e7375ca24934180e98ba
BITCOIN account created successfully!
Key saved to: /home/eeeeye/.zetachain/keys/bitcoin/mywallet.json
Address: bc1qy3tafmggfkgp5fappxf5cqsswg2zms7haru0r9
TON account created successfully!
Key saved to: /home/eeeeye/.zetachain/keys/ton/mywallet.json
Address: 0QCvck3o6tKGPvzkairgUWnWO0-vCKE0RvQdHZalpD1ak3p8
```

在shell中创建自己的钱包

```
npx zetachain accounts create --name mywallet                                                                            
Creating accounts for all supported types...
EVM account created successfully!
Key saved to: /home/eeeeye/.zetachain/keys/evm/mywallet.json
Address: 0x784f02F6a80c0D2Dc8485b9F05Ce2A549EDa60A3
SOLANA account created successfully!
Key saved to: /home/eeeeye/.zetachain/keys/solana/mywallet.json
Address: GNPPUzwT1jn4VroozW7BoPr2XdvMBXtgXD1aFLTUDZiG
SUI account created successfully!
Key saved to: /home/eeeeye/.zetachain/keys/sui/mywallet.json
Address: 0x98aec9ebf7d1797313c7e863e4ef4e7f89c7e87286f1e7375ca24934180e98ba
BITCOIN account created successfully!
Key saved to: /home/eeeeye/.zetachain/keys/bitcoin/mywallet.json
Address: bc1qy3tafmggfkgp5fappxf5cqsswg2zms7haru0r9
TON account created successfully!
Key saved to: /home/eeeeye/.zetachain/keys/ton/mywallet.json
Address: 0QCvck3o6tKGPvzkairgUWnWO0-vCKE0RvQdHZalpD1ak3p8
​
```

## **Faucet**

**将metamask的Ethereum钱包地址放入**[**https://zetachain.faucetme.pro/**](https://zetachain.faucetme.pro/)

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/Eeeeye/images/2025-11-25-1764085622471-image.png)

在钱包中检查是否收到测试代币：

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/Eeeeye/images/2025-11-25-1764085733607-image.png)

## **Explorer**

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/Eeeeye/images/2025-11-25-1764076859772-image.png)

## **RPC & Contracts**

RPC 就是让你的电脑与区块链节点通信的入口，是区块链的 API 网关，所有读写都要通过它。

通读了官方文档中的以下部分

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/Eeeeye/images/2025-11-25-1764077681273-image.png)

学习了4 种智能合约类型：

| 合约 | 类比 | 用途 |
| --- | --- | --- |
| connector | 跨链大脑 | 验证跨链消息、路由消息 |
| erc20Custody | 银行保险柜 | 锁仓原链 ERC20，映射到 ZetaChain |
| gateway | 跨链 API | 用户和 dApp 调用的入口 |
| tss | 多签安全系统 | 验证 ZetaChain 节点签名，确保安全跨链 |

## Qwen

-   虚拟环境启动：
    

source .venv/bin/activate

-   添加如下代码到qwen\_test.py解决代理问题：
    

os.environ\["HTTP\_PROXY"\] = ""

os.environ\["HTTPS\_PROXY"\] = ""

os.environ\["ALL\_PROXY"\] = ""

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/Eeeeye/images/2025-11-25-1764086493033-image.png)
<!-- DAILY_CHECKIN_2025-11-25_END -->

# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->


## **Task1**

```
 npm install -g zetachain         
zetachain query chains list
```

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/Eeeeye/images/2025-11-24-1764000144501-image.png)

## **Task2**

![截图 2025-11-24 23-39-08.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/Eeeeye/images/2025-11-24-1764000078427-___2025-11-24_23-39-08.png)

generate the API key and use python visual environment to run [test.sh](http://test.sh)

here is the content of .sh(the "DASHSCOPE\_API\_KEY" has been set to my API\_KEY:

```
import os
from openai import OpenAI
​
client = OpenAI(
    # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",
)
completion = client.chat.completions.create(
    model="qwen3-max",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "你是谁？"},
    ],
    stream=True
)
for chunk in completion:
    print(chunk.choices[0].delta.content, end="", flush=True)
```

![截图 2025-11-24 23-53-41.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/Eeeeye/images/2025-11-24-1764000048047-___2025-11-24_23-53-41.png)

## **Task3**

Join the community in wechat

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/Eeeeye/images/2025-11-24-1764000110205-image.png)
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->
