---
timezone: UTC+8
---

# Kong Weiyi

**GitHub ID:** Kongweiyi928

**Telegram:** @KLucifer928

## Self-introduction

From SEU BA

## Notes

<!-- Content_START -->
# 2025-11-25
<!-- DAILY_CHECKIN_2025-11-25_START -->
# **1.安装ZetaChain CLI**

## **ZetaChain CLI**

ZetaChain CLI 是一个功能强大的命令行工具，专门用于与 ZetaChain 区块链网络进行交互。它既是开发者的构建工具，也是节点运营者和高级用户的管理控制台。

### **核心架构**

### **二进制组件**

-   **主要组件**: `zetacored` - ZetaChain 的核心二进制文件
    
-   **集成功能**: 节点运行 + 客户端交互一体化
    
-   **技术基础**: 基于 Cosmos SDK 构建，遵循 Cosmos 生态标准
    

### **主要功能模块**

### **1\. 钱包与密钥管理**

```
# 创建新钱包
zetacored keys add my-wallet

# 恢复钱包（通过助记词）
zetacored keys add recovered-wallet --recover

# 列出所有钱包
zetacored keys list

# 查看钱包详情
zetacored keys show my-wallet

# 删除钱包
zetacored keys delete my-wallet
```

### **2\. 网络查询功能**

```
# 查询账户余额
zetacored query bank balances zeta1...

# 查询交易状态
zetacored query tx <交易哈希>

# 获取区块信息
zetacored query block

# 查询验证者列表
zetacored query staking validators

# 跨链状态查询（ZetaChain 特有）
zetacored query observer chain-state
```

### **3\. 交易操作**

```
# ZETA 代币转账
zetacored tx bank send <发送者> <接收者> 1000000azeta --chain-id zetachain_7000-1

# 质押操作
zetacored tx staking delegate <验证者地址> 1000000azeta

# 治理投票
zetacored tx gov vote <提案ID> yes

# 跨链交易（核心功能）
zetacored tx crosschain send ...
```

### **4\. 节点运营管理**

```
# 初始化节点
zetacored init my-node --chain-id zetachain_7000-1

# 启动节点
zetacored start

# 检查节点状态
zetacored status

# 重置节点（测试环境）
zetacored unsafe-reset-all
```

## **安装与配置**

### **环境要求**

-   **Node.js**: ≥ 18.x
    
-   **Git**: 用于克隆项目模板
    
-   **Docker**: ≥ 24.x（用于本地网络）
    

### **安装方式**

**方法一：本地临时使用**

```
npx zetachain@next new
```

**方法二：全局安装**

```
npm install -g zetachain@latest
```

**方法三：从源码构建**

```
git clone https://github.com/zeta-chain/zetacored
cd zetacored
make install
```

### **环境验证**

```
# 验证安装
zetachain version

# 测试网络连接
zetachain query chains list

# 检查配置
zetachain config list
```

## **实际应用场景**

### **开发工作流**

```
# 1. 创建新项目
zetachain new my-crosschain-dapp

# 2. 启动本地开发网络
zetachain localnet start

# 3. 编译合约
cd my-crosschain-dapp
npm run compile

# 4. 部署合约
npm run deploy

# 5. 测试交互
zetachain query contract-state <合约地址>
```

### **钱包管理流程**

```
# 创建开发钱包
npx zetachain accounts create --name dev-wallet

# 导出私钥（谨慎操作）
npx zetachain accounts export dev-wallet

# 查询测试币余额
zetachain query balances --evm $(zetachain accounts list)

# 从水龙头获取测试币
curl -X POST https://faucet.zetachain.com/request -H "Content-Type: application/json" -d '{"address":"你的地址"}'
```

### **跨链操作示例**

```
# 查询支持的链列表
zetachain query chains list

# 跨链余额查询
zetachain query balances --evm 0x... --chain eth

# 发送跨链交易
zetachain tx crosschain send \
  --from my-wallet \
  --chain eth \
  --recipient 0x... \
  --amount 1000000
```

## **高级功能**

### **配置管理**

```
# 查看当前配置
zetachain config list

# 设置默认网络
zetachain config set network testnet

# 配置自定义 RPC 端点
zetachain config set rpc.endpoint https://your-custom-rpc.com

# 设置 Gas 价格
zetachain config set gas.price 1000000000azeta
```

### **脚本自动化**

```
#!/bin/bash
# 自动化部署脚本示例

# 设置环境变量
export PRIVATE_KEY="你的私钥"
export NETWORK="zeta_testnet"

# 编译合约
echo "编译合约..."
npx hardhat compile

# 部署合约
echo "部署合约..."
npx hardhat deploy --network $NETWORK

# 验证合约
echo "验证合约..."
npx hardhat verify --network $NETWORK <合约地址>
```

### **监控与调试**

```
# 实时日志监控
zetacored logs --follow

# 交易调试
zetachain tx debug <交易哈希>

# 性能监控
zetachain query tendermint validator-set
```

## **故障排除**

### **常见问题解决**

```
# 清除缓存
zetachain cache clean

# 重置配置
zetachain config reset

# 更新工具版本
npm update -g zetachain

# 检查网络连接
zetachain query status
```

### **日志分析**

```
# 查看详细日志
zetacored logs --level debug

# 过滤特定模块日志
zetacored logs --module bank

# 导出日志文件
zetacored logs > zetacored.log
```

![](https://camo.githubusercontent.com/10bf7a23c219fa1f242bb1e763e7df911448b9d7b6c2365f4db2928eb4f34a0f/68747470733a2f2f6176316c6e37717061366c2e6665697368752e636e2f73706163652f6170692f626f782f73747265616d2f646f776e6c6f61642f6173796e63636f64652f3f636f64653d596d45774f574e6d4f4467304d4751354e474a6c4e4745334e4455784e6a42685a4441325a6d5a6b596a4e6652304d334f5768305a6b4a5453317071526b5a5a535452794d4468546447356f56553544636e6835647a4e66564739725a57343656557835566d4a7665576c6c62334d354e587034536c597762574e754d303949626d4e6f587a45334e6a51774e6a51324f4451364d5463324e4441324f4449344e4639574e41)

# **2.ZetaChain Faucet**

## **什么是 Faucet？**

**Faucet**（水龙头）是区块链测试网络中免费分发测试代币的服务。它允许开发者在无需真实资金的情况下获取测试网代币，用于开发和测试智能合约、DApps 和跨链功能。

## **ZetaChain Faucet 的作用**

### **主要用途**

-   **开发测试**: 获取测试网 ZETA 代币部署和测试智能合约
    
-   **交易燃料**: 支付交易手续费（Gas Fee）
    
-   **跨链测试**: 测试跨链交易和消息传递功能
    
-   **教育学习**: 供学习者体验 ZetaChain 功能
    

## **官方 Faucet 渠道**

### **1\. 主 Faucet 网站**

```
https://www.zetachain.com/docs/reference/faucet/
```

### **2\. 社区 Faucet**

```
https://zetachain.faucetme.pro/
```

### **3\. Discord 水龙头**

-   加入 ZetaChain 官方 Discord
    
-   在特定频道使用命令获取测试币
    

## **使用流程**

### **基本步骤**

```
# 1. 首先创建或获取你的测试网地址
npx zetachain accounts create --name test-account

# 2. 获取生成的地址
zetachain accounts list

# 3. 访问 Faucet 网站并输入地址
# 或者使用 API 方式
```

### **API 请求示例**

```
curl -X POST https://faucet.zetachain.com/request \
  -H "Content-Type: application/json" \
  -d '{"address":"你的zeta地址或0x格式地址"}'
```

![](https://camo.githubusercontent.com/06158d84aa2aae98eb38d43d5f2a878272e17bf5efd049494a353a74510a5992/68747470733a2f2f6176316c6e37717061366c2e6665697368752e636e2f73706163652f6170692f626f782f73747265616d2f646f776e6c6f61642f6173796e63636f64652f3f636f64653d4f545931596a63354d7a566c4d7a6c6d596a52684f4451325932466a596d4533595745334d32517959574666636d644f64446732646b493462446c6a57484a71566a6c444e565a73526e4e516248703163484533636b7466564739725a57343656566b33616d4a7a516e457a623052334d454a3455304a44516d4e694f45746a626d706f587a45334e6a51774e6a51324f4451364d5463324e4441324f4449344e4639574e41)

# **3.ZetaChain 主网与测试网**

## **主网 (Mainnet)**

### **定义与特点**

**主网**是 ZetaChain 的正式生产环境，处理真实价值的资产和交易。

### **关键特性**

-   **真实经济价值**: 所有交易使用真实 ZETA 代币
    
-   **不可逆性**: 交易一旦确认不可撤销
    
-   **生产级安全**: 最高级别的网络安全措施
    
-   **真实用户资产**: 承载真实的用户资金和商业应用
    

### **技术参数**

```
# 主网 Chain ID
Chain ID (EVM): 7000
Chain ID (Cosmos): zetachain_7000-1

# 主网 RPC 端点
https://zetachain-evm.blockpi.network/v1/rpc/public
https://zetachain-mainnet.rpc.thirdweb.com

# 主网区块浏览器
https://zetascan.com
https://explorer.zetachain.com
```

## **测试网 (Testnet)**

### **定义与目的**

**测试网**是 ZetaChain 的测试环境，用于开发和测试，不涉及真实价值。

### **主要用途**

-   **智能合约开发**: 安全地测试和调试合约
    
-   **DApp 测试**: 验证应用程序功能
    
-   **协议升级测试**: 在新功能上线主网前进行测试
    
-   **开发者教育**: 学习 ZetaChain 功能的最佳环境
    

### **当前测试网: Maimet Beta**

**技术参数**

```
# 测试网 Chain ID
Chain ID (EVM): 7001
Chain ID (Cosmos): zetachain_7001-1

# 代币信息
Denom: azeta
Symbol: testZETA (或 tZETA)
Decimals: 18

# 测试网 RPC 端点
https://zetachain-testnet.rpc.thirdweb.com
https://zetachain-evm.testnet.lava.build

# 测试网区块浏览器
https://athens.explorer.zetachain.com
https://zetachain-testnet.blockexplorer.ai
```

# **4.ZetaChain RPC**

## **什么是 RPC？**

RPC（远程过程调用）是区块链与外部世界通信的桥梁。在 ZetaChain 的语境中，RPC 是**节点暴露的 API 端点**，允许开发者查询区块链数据、提交交易、与智能合约交互。

## **ZetaChain 的双重 RPC 架构**

ZetaChain 的独特之处在于它同时支持两种 RPC 协议：

### **1\. JSON-RPC (EVM 兼容层)**

**特点**

-   **协议**: JSON-RPC 2.0
    
-   **数据格式**: JSON
    
-   **端口**: 通常 8545、8546
    
-   **兼容性**: 完全兼容以太坊生态工具
    

**主要方法**

```
// 基础查询
eth_blockNumber        // 获取最新区块号
eth_getBalance         // 查询地址余额
eth_getTransactionReceipt // 获取交易回执

// 智能合约交互
eth_call              // 读取合约状态
eth_sendRawTransaction // 发送签名交易

// 事件监听
eth_getLogs           // 查询事件日志
```

**使用示例**

```
// 使用 Web3.js 连接 ZetaChain RPC
const Web3 = require('web3');
const web3 = new Web3('https://zetachain-evm.blockpi.network/v1/rpc/public');

// 查询余额
const balance = await web3.eth.getBalance('0x...');
console.log(`余额: ${web3.utils.fromWei(balance, 'ether')} ZETA`);

// 发送交易
const tx = {
  from: '0x...',
  to: '0x...',
  value: web3.utils.toWei('0.1', 'ether'),
  gas: 21000
};
const receipt = await web3.eth.sendTransaction(tx);
```

### **2\. gRPC & REST (Cosmos SDK 层)**

**特点**

-   **协议**: gRPC (HTTP/2 + Protobuf) 和 REST/HTTP
    
-   **数据格式**: 二进制 (gRPC) 或 JSON (REST)
    
-   **端口**: 9090 (gRPC), 1317 (REST)
    
-   **功能**: 访问 Cosmos 原生功能
    

**端点示例**

```
# REST 端点示例
# 查询账户信息
curl http://localhost:1317/cosmos/auth/v1beta1/accounts/zeta1...

# 查询链状态
curl http://localhost:1317/cosmos/base/tendermint/v1beta1/node_info

# 查询跨链观察者状态
curl http://localhost:1317/zeta-chain/observer/chain_params
```

## **RPC 端点类型**

### **公共端点 (Public RPC)**

```
// 主网公共端点
const mainnetRPC = {
  evm: "https://zetachain-evm.blockpi.network/v1/rpc/public",
  cosmos: "https://zetachain-rest.core.chainstack.com"
};

// 测试网公共端点  
const testnetRPC = {
  evm: "https://zetachain-testnet.rpc.thirdweb.com",
  cosmos: "https://zetachain-testnet.rest.core.chainstack.com"
};
```

**特点**:

-   免费使用
    
-   有速率限制
    
-   适合开发和测试
    
-   可能存在性能瓶颈
    

### **专用端点 (Dedicated RPC)**

```
// 基础设施服务商
const dedicatedRPC = {
  // Chainstack
  chainstack: "https://zetachain-mainnet.rpc.chainstack.com",
  
  // BlockPI
  blockpi: "https://zetachain.blockpi.network/v1/rpc/public",
  
  // Lava Network
  lava: "https://zetachain.rpc.lava.build"
};
```

**特点**:

-   更高的速率限制
    
-   更好的性能
    
-   可能需要注册或付费
    
-   生产环境推荐
    

### **本地端点 (Local RPC)**

```
# 启动本地节点
zetacored start

# 本地 RPC 端点
EVM: http://localhost:8545
REST: http://localhost:1317
gRPC: http://localhost:9090
```

## **实际配置示例**

### **1\. Hardhat 配置**

```
// hardhat.config.js
require('@nomiclabs/hardhat-ethers');

module.exports = {
  networks: {
    zeta_mainnet: {
      url: "https://zetachain-evm.blockpi.network/v1/rpc/public",
      chainId: 7000,
      accounts: [process.env.MAINNET_PRIVATE_KEY],
      gasPrice: 20000000000, // 20 Gwei
      timeout: 60000
    },
    zeta_testnet: {
      url: "https://zetachain-testnet.rpc.thirdweb.com", 
      chainId: 7001,
      accounts: [process.env.TESTNET_PRIVATE_KEY],
      gasPrice: 10000000000, // 10 Gwei
      timeout: 60000
    },
    zeta_local: {
      url: "http://localhost:8545",
      chainId: 70000,
      accounts: [process.env.LOCAL_PRIVATE_KEY]
    }
  },
  solidity: {
    version: "0.8.19",
    settings: {
      optimizer: {
        enabled: true,
        runs: 200
      }
    }
  }
};
```

### **2\. 前端 DApp 配置**

```
// web3配置
import { ethers } from 'ethers';

const ZETACHAIN_RPC = {
  mainnet: 'https://zetachain-evm.blockpi.network/v1/rpc/public',
  testnet: 'https://zetachain-testnet.rpc.thirdweb.com'
};

class ZetaChainClient {
  constructor(network = 'testnet') {
    this.provider = new ethers.providers.JsonRpcProvider(
      ZETACHAIN_RPC[network]
    );
    this.signer = null;
  }
  
  // 连接钱包
  async connectWallet() {
    if (window.ethereum) {
      await window.ethereum.request({ method: 'eth_requestAccounts' });
      this.signer = new ethers.providers.Web3Provider(window.ethereum).getSigner();
    }
  }
  
  // 查询跨链余额
  async getCrossChainBalance(address, chain) {
    const balance = await this.provider.getBalance(address);
    return ethers.utils.formatEther(balance);
  }
}
```

### **3\. 命令行工具使用**

```
# 使用 CLI 查询不同 RPC 端点
zetachain query balances --rpc https://zetachain-evm.blockpi.network/v1/rpc/public

# 设置默认 RPC 端点
zetachain config set rpc.evm https://zetachain-evm.blockpi.network/v1/rpc/public
zetachain config set rpc.cosmos https://zetachain-rest.core.chainstack.com
```

# **5.ZetaChain开发工作流程**

### **1\. 环境设置**

```
# 1. 安装 CLI
npm install -g zetachain@latest

# 2. 创建项目
zetachain new my-crosschain-app

# 3. 安装依赖
cd my-crosschain-app && npm install

# 4. 配置环境变量
cp .env.example .env
# 编辑 .env 文件添加私钥和 RPC URL
```

### **2\. 本地开发测试**

```
# 启动本地网络
zetachain localnet start

# 编译合约
npx hardhat compile

# 运行测试
npx hardhat test

# 部署到本地网络
npx hardhat deploy --network localnet
```

### **3\. 测试网部署**

```
# 获取测试币
npx zetachain faucet --address <你的地址>

# 部署到测试网
npx hardhat deploy --network zeta_testnet

# 验证合约
npx hardhat verify --network zeta_testnet <合约地址>
```

# **6.Qwen API**

## **1\. 终端使用 cURL 请求**

### **基本请求格式**

```
curl -X POST "https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen-turbo",
    "input": {
      "messages": [
        {
          "role": "user",
          "content": "请介绍一下你自己"
        }
      ]
    },
    "parameters": {
      "result_format": "message"
    }
  }'
```

### **简化版本**

```
curl -X POST "https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen-turbo",
    "input": {
      "messages": [
        {"role": "user", "content": "你好"}
      ]
    }
  }' > response.json
```

## **2\. Postman 请求配置**

### **步骤 1：创建新请求**

-   **方法**: POST
    
-   **URL**: `https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation`
    

### **步骤 2：设置 Headers**

| Key | Value |
| --- | --- |
| Authorization | Bearer YOUR_API_KEY |
| Content-Type | application/json |
| X-DashScope-SSE | disable (如需关闭流式输出) |

### **步骤 3：设置 Body**

选择 **raw** 和 **JSON** 格式，输入以下内容：

```
{
  "model": "qwen-turbo",
  "input": {
    "messages": [
      {
        "role": "user",
        "content": "请用一句话介绍量子计算"
      }
    ]
  },
  "parameters": {
    "result_format": "message",
    "max_tokens": 1500,
    "temperature": 0.7
  }
}
```

## **3\. 不同模型的请求示例**

### **Qwen-Turbo**

```
curl -X POST "https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen-turbo",
    "input": {
      "messages": [
        {"role": "user", "content": "写一首关于春天的短诗"}
      ]
    }
  }'
```

### **Qwen-Max**

```
curl -X POST "https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen-max",
    "input": {
      "messages": [
        {"role": "user", "content": "解释深度学习的基本原理"}
      ]
    },
    "parameters": {
      "result_format": "message"
    }
  }'
```

### **Qwen-Plus**

```
curl -X POST "https://dashscope.aliyuncs.com/api/v1/services/aigc/text-generation/generation" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen-plus",
    "input": {
      "messages": [
        {"role": "user", "content": "用Python写一个计算斐波那契数列的函数"}
      ]
    }
  }'
```
<!-- DAILY_CHECKIN_2025-11-25_END -->

# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->

# **ZetaChain**

目前，区块链世界在享受多链带来的多样性和特定优势的同时，也深刻受困于由此产生的“孤岛效应”。

1.  **流动的碎片化：资本被分散在数十条公链和 Layer 2 网络上。这不仅降低了资金的整体利用效率，还导致用户在跨链转移资产时面临高昂的手续费、显著的交易滑点以及漫长的等待时间。**
    
2.  **技术复杂性与安全风险**：传统的跨链方案，如资产桥，通常需要引入“包装资产”和额外的信任假设。这不仅增加了用户的操作步骤和理解门槛，更引入了**新的单点故障风险**，桥接合约已成为黑客攻击的重灾区。此外，不同区块链在协议、共识机制和数据结构上的技术差异，使得实现无缝互操作在工程上极为困难。
    
3.  **开发者体验与创新受阻**：开发者若想构建覆盖多链用户的应用，不得不为每条链单独部署和维护智能合约，并处理复杂的跨链逻辑。这种高昂的开发成本和复杂性严重**抑制了创新，限制了应用的可访问性**。
    

面对上述问题，市场迫切需要一种更底层、更统一的基础设施。ZetaChain 作为一个“通用区块链”，其设计理念和技术架构直指这些核心问题。

1.  **实现真正的原生互操作性**：ZetaChain 最核心的突破在于，它允许开发者**通过一个全链智能合约，直接管理和操作不同链上的原生资产**，甚至是比特币。用户无需再与包装资产打交道，从而消除了与之相关的信用风险和摩擦。
    
2.  **统一流动性层**：ZetaChain 的愿景是成为一个**统一的流动性层和业务逻辑执行层**。它通过其通用EVM（zEVM）和跨链消息传递机制，抽象了底层链的复杂性。这使得开发者可以像调用单个链上的合约一样，构建跨链的DeFi应用、NFT平台等，从而**释放被割裂的流动性价值**。
    
3.  **提升开发者效率与用户体验**：开发者得以从多链部署和维护的繁重工作中解放出来，**一次开发，即可覆盖所有主流区块链的用户**。对用户而言，复杂的跨链操作被封装在简洁的应用界面之后，交互体验无限接近于单链应用，这极大地**降低了Web3的进入门槛**。
    

# **Qwen**

当前，AI Agent在实际应用中暴露出关键问题。在推理能力方面，大多数模型难以维持复杂的逻辑链条，当任务复杂度增加时，很容易出现"推理迷失"现象。具体表现为：

1.  **在处理多步骤任务时，模型会逐渐偏离核心目标。**
    
2.  **在需要长期规划的任务中，无法保持战略方向的一致性。**
    
3.  **面对突发情况时，缺乏灵活的应变能力。**
    

面对这些挑战，Qwen模型从底层架构开始就进行了针对性的设计和优化。在推理能力方面，Qwen通过创新的训练方法和模型结构，显著提升了逻辑推理和数学推理能力。这不仅体现在基准测试的成绩上，更在实际的复杂任务处理中展现出明显的优势。模型能够更好地理解任务的内在逻辑，保持推理过程的一致性，并在遇到意外情况时展现出更强的应变能力。
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->
