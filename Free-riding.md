---
timezone: UTC+8
---

# lihua

**GitHub ID:** Free-riding

**Telegram:** @nowhere

## Self-introduction

Again and again ~

## Notes

<!-- Content_START -->
# 2025-11-25
<!-- DAILY_CHECKIN_2025-11-25_START -->
# ZetaChain和区块链一些基础

## ZetaChain

-   ZetaChain是 主链（Layer 1）
    
-   全链智能合约，开发者编写一次智能合约，即可在任意连接链上接收事件并执行逻辑
    
-   ZetaChain 的独特优势在于支持非智能合约链如：Bitcoin
    
-   通过协议层原生支持跨链消息与资产，无需桥或封装
    

## Layer 1 和Layer 2

### L1

-   Layer 1 是指底层的主区块链协议本身，它主要负责共识机制（如 PoW、PoS），数据存储（账本），原生代币（如 BTC、ETH）和基础安全性与去中心化
    
-   L1 的扩容通过**直接修改底层协议**实现
    
-   安全性高（直接由主链共识保障）
    
-   去中心化程度通常较高
    
-   无需依赖外部系统
    
-   升级困难（需全网共识，硬分叉风险）
    
-   扩容能力有限（如 Bitcoin TPS ≈ 7，Ethereum ≈ 15–30）
    
-   交易费用高、速度慢（尤其在高负载时）
    

### L2

-   **Layer 2 是构建在 Layer 1 之上的附加协议或网络**，目的是**提升交易吞吐量、降低费用，同时继承 L1 的安全性**。L2 本身不独立维护完整区块链，而是将大部分计算或存储“移出主链”，只在必要时与 L1 交互。
    
-   **高 TPS**：可达数千甚至上万笔/秒（如 zkSync 目标 2000+ TPS）
    
-   **低 Gas 费**：交易成本降低 10–100 倍
    
-   **快速确认**：部分操作秒级完成
    
-   **兼容 EVM**：多数 Rollup 支持以太坊智能合约无缝迁移
    
-   **复杂性高**：用户需理解“桥接”“提款延迟”等概念
    
-   **提款延迟**（Optimistic Rollup）：通常需 7 天挑战期
    
-   **中心化风险**（早期 L2）：排序器（Sequencer）可能由单一实体控制
    
-   **碎片化**：L2 之间互通困难（如 Arbitrum 和 Optimism 资产不能直接互转）
    

## ZetaChain的领水地址(需要登陆Discord)

[FAUCETME](https://zetachain.faucetme.pro/)

## 重新注册了Discord

## 重新注册了国内版的阿里云百炼（国外的需要用非内地手机号）

[阿里云百炼](https://bailian.console.aliyun.com/?tab=model#/efm/model_experience_center/text)

## 下载了PostMan

[PostMan](https://www.postman.com/downloads/)

需要注意处理器版本，看看是不是RAM版本

## 初始化ZetaChain环境

```
npx zetachain@latest new --project hello
cd hello
yarn
forge soldeer update
```

初始化成功后，会自动生成一个通用合约模板

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

// 引入 ZetaChain 协议合约中的 UniversalContract 接口
import "@zetachain/protocol-contracts/contracts/zevm/interfaces/UniversalContract.sol";

// 继承 UniversalContract，成为“全链合约”
contract Universal is UniversalContract {
    // 定义一个事件，用于日志输出
    event HelloEvent(string, string);

    // 重写 onCall 方法，处理跨链调用
    function onCall(
        MessageContext calldata context,   // 跨链消息的上下文信息
        address zrc20,                     // 发送的 ZRC-20 代币地址（如 zBTC, zETH）
        uint256 amount,                    // 发送的代币数量
        bytes calldata message             // 用户自定义的跨链消息数据
    ) external override onlyGateway {      // 仅允许 ZetaChain 网关调用
        // 从 message 中解码出一个字符串
        string memory name = abi.decode(message, (string));
        // 触发事件，打印 "Hello: [name]"
        emit HelloEvent("Hello: ", name);
    }
}
```

我当时报错说是编译器是0.8.30以上版本，在0.8.26前面加^就行了表示当前合约支持大于0.8.26,小于0.9.0的版本

### onCall()**是什么？**

![profile](https://assets.alicdn.com/g/qwenweb/qwen-webui-fe/0.0.248/static/qwen_icon_dark_84.png)

**Qwen3-Max22:58**

你提供的这段 Solidity 代码是 ZetaChain **全链智能合约（Universal Contract）** 的一个典型实现，其中重写了 `onCall` 方法。这是 ZetaChain 在其 **Zeta EVM（Zeta Chain 的兼容 EVM 的执行环境）** 中用于处理**跨链调用**的核心入口函数。

下面我们逐行解析这段代码，并重点讲解 `onCall` 方法的作用、参数含义、执行流程以及安全机制。

* * *

### **🔍 代码全貌解析**

**solidity**

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

// SPDX-License-Identifier: MIT

pragma solidity ^0.8.26;

// 引入 ZetaChain 协议合约中的 UniversalContract 接口

import "@zetachain/protocol-contracts/contracts/zevm/interfaces/UniversalContract.sol";

// 继承 UniversalContract，成为“全链合约”

contract Universal is UniversalContract {

// 定义一个事件，用于日志输出

event HelloEvent(string, string);

// 重写 onCall 方法，处理跨链调用

function onCall(

MessageContext calldata context, // 跨链消息的上下文信息

address zrc20, // 发送的 ZRC-20 代币地址（如 zBTC, zETH）

uint256 amount, // 发送的代币数量

bytes calldata message // 用户自定义的跨链消息数据

) external override onlyGateway { // 仅允许 ZetaChain 网关调用

// 从 message 中解码出一个字符串

string memory name = abi.decode(message, (string));

// 触发事件，打印 "Hello: \[name\]"

emit HelloEvent("Hello: ", name);

}

}

* * *

## **一、**`onCall` **是什么？**

在 ZetaChain 的 **Universal Contract（通用合约）模型**中：

> `onCall` **是跨链消息到达 ZetaChain 时自动触发的回调函数**。

当用户在**任意已连接链**（如 Bitcoin、Ethereum、Dogecoin）上向 ZetaChain 发起跨链请求（例如发送资产 + 附加消息），ZetaChain 的协议层会：

1.  验证该跨链交易；
    
2.  将其封装为一个标准化的“跨链消息”；
    
3.  **自动调用目标合约的** `onCall` **方法**，传递相关参数。
    
4.  因此，`onCall` 就是合约的“跨链入口”。
    

## **二、**`onCall` **的四个参数详解**

### **1\.** `MessageContext calldata context`

这是一个结构体，包含跨链调用的**元信息**。定义通常如下（来自 ZetaChain SDK）：

```
struct MessageContext {
    address origin;      // 源链标识（如 Bitcoin 链的地址常量）
    address caller;      // 源链上发起交易的用户地址（映射为 Zeta 格式）
    uint256 nonce;       // 防重放攻击的随机数
    bytes32 hash;        // 消息哈希
}
```

-   `context.origin`：告诉你消息来自哪条链（例如 `0x...bitcoin`）；
    
-   `context.caller`：源链用户的地址（ZetaChain 会将 BTC 地址等转换为 Ethereum 风格地址）
    

### **2\.** `address zrc20`

-   表示用户在源链上发送的**原生资产**（如 BTC、ETH、DOGE）在 ZetaChain 上对应的 **ZRC-20 代币地址**。
    
-   例如：BTC → `zBTC`，ETH → `zETH`。
    
-   若用户**只发消息没发资产**，则 `zrc20 = address(0)`。
    

![profile](https://assets.alicdn.com/g/qwenweb/qwen-webui-fe/0.0.248/static/qwen_icon_dark_84.png)

**Qwen3-Max22:58**

你提供的这段 Solidity 代码是 ZetaChain **全链智能合约（Universal Contract）** 的一个典型实现，其中重写了 `onCall` 方法。这是 ZetaChain 在其 **Zeta EVM（Zeta Chain 的兼容 EVM 的执行环境）** 中用于处理**跨链调用**的核心入口函数。

下面我们逐行解析这段代码，并重点讲解 `onCall` 方法的作用、参数含义、执行流程以及安全机制。

* * *

### **🔍 代码全貌解析**

**solidity**

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

// SPDX-License-Identifier: MIT

pragma solidity ^0.8.26;

// 引入 ZetaChain 协议合约中的 UniversalContract 接口

import "@zetachain/protocol-contracts/contracts/zevm/interfaces/UniversalContract.sol";

// 继承 UniversalContract，成为“全链合约”

contract Universal is UniversalContract {

// 定义一个事件，用于日志输出

event HelloEvent(string, string);

// 重写 onCall 方法，处理跨链调用

function onCall(

MessageContext calldata context, // 跨链消息的上下文信息

address zrc20, // 发送的 ZRC-20 代币地址（如 zBTC, zETH）

uint256 amount, // 发送的代币数量

bytes calldata message // 用户自定义的跨链消息数据

) external override onlyGateway { // 仅允许 ZetaChain 网关调用

// 从 message 中解码出一个字符串

string memory name = abi.decode(message, (string));

// 触发事件，打印 "Hello: \[name\]"

emit HelloEvent("Hello: ", name);

}

}

* * *

## **一、**`onCall` **是什么？**

在 ZetaChain 的 **Universal Contract（通用合约）模型**中：

> `onCall` **是跨链消息到达 ZetaChain 时自动触发的回调函数**。

当用户在**任意已连接链**（如 Bitcoin、Ethereum、Dogecoin）上向 ZetaChain 发起跨链请求（例如发送资产 + 附加消息），ZetaChain 的协议层会：

1.  验证该跨链交易；
    
2.  将其封装为一个标准化的“跨链消息”；
    
3.  **自动调用目标合约的** `onCall` **方法**，传递相关参数。
    

✅ 因此，`onCall` 就是你合约的“跨链入口”。

* * *

## **二、**`onCall` **的四个参数详解**

### **1\.** `MessageContext calldata context`

这是一个结构体，包含跨链调用的**元信息**。定义通常如下（来自 ZetaChain SDK）：

```
struct MessageContext {

    address origin;      // 源链标识（如 Bitcoin 链的地址常量）

    address caller;      // 源链上发起交易的用户地址（映射为 Zeta 格式）

    uint256 nonce;       // 防重放攻击的随机数

    bytes32 hash;        // 消息哈希

}
```

-   `context.origin`：告诉你消息来自哪条链（例如 `0x...bitcoin`）；
    
-   `context.caller`：源链用户的地址（ZetaChain 会将 BTC 地址等转换为 Ethereum 风格地址）；
    
-   可用于权限控制、链特定逻辑等。
    

> 📌 在你的代码中虽然没有使用 `context`，但它是关键信息源。

* * *

### **2\.** `address zrc20`

-   表示用户在源链上发送的**原生资产**（如 BTC、ETH、DOGE）在 ZetaChain 上对应的 **ZRC-20 代币地址**。
    
-   例如：BTC → `zBTC`，ETH → `zETH`。
    
-   若用户**只发消息没发资产**，则 `zrc20 = address(0)`。
    

* * *

### **3\.** `uint256 amount`

-   用户在源链发送的资产数量（已转换为 ZRC-20 的最小单位）。
    
-   例如：发送 0.01 BTC → `amount = 1_000_000`（satoshi）。
    
-   若无资产转移，则为 `0`。
    

### **4\.** `bytes calldata message`

-   **用户自定义的任意数据**，是你实现通用逻辑的关键。
    
-   通常使用 `abi.encode(...)` 在源链构造，用 `abi.decode(...)` 在 `onCall` 中解析。
    

string memory name = abi.decode(message, (string));表示用户在源链发送了一个字符串（如 "Alice"），合约将其解码并用于事件。

## **三、**`onlyGateway` **修饰符：安全核心**

```
external override onlyGateway
```

-   `onlyGateway` 是 ZetaChain 协议提供的**关键安全机制**。
    
-   它确保 `onCall` **只能由 ZetaChain 的官方网关合约（Gateway）调用**。
    
-   **普通用户或其它合约无法直接调用** `onCall`，防止伪造跨链消息。
    

## 四、执行流程示例

假设用户想从 **Ethereum** 调用这个合约，并传入名字 `"Alice"`：

使用 ZetaChain SDK（如 @zetachain/zeta-eth）：

```
const message = abi.encode(["string"], ["Alice"]);
await zetaConnector.send({
  destinationAddress: "0xYourUniversalContractOnZeta",
  message: message,
  zrc20: "0x0000000000000000000000000000000000000000", // 无资产
  amount: 0,
});
```

步骤 2：ZetaChain 处理

-   ZetaChain 观察者检测到 Ethereum 上的调用；
    
-   验证通过后，在 ZetaChain 主网执行：
    

```
universalContract.onCall(
    context: { origin: ETHEREUM_CHAIN, caller: userAddrOnZeta, ... },
    zrc20: 0x0,
    amount: 0,
    message: 0x...（"Alice" 的 ABI 编码）
);
```

### **步骤 3：合约执行**

-   解码 `message` 得到 `"Alice"`；
    
-   触发事件：`HelloEvent("Hello: ", "Alice")`；
    
-   开发者可通过事件监听器得知跨链调用成功。
<!-- DAILY_CHECKIN_2025-11-25_END -->

# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->




# 第一份WEB3笔记

## 一.ZetaChain开发文档入口

-   [https://www.zetachain.com/docs/developers](https://www.zetachain.com/docs/developers)
    

## 二.ZetaChain是什么（粗浅的理解）

1.  一个可以原生访问任何区块链的通用区块链
    
2.  可以跨链去调用不同的DAPP
    
3.  使用“全链智能合约”，一个合约可以监听和响应多条链上的事件，并在任意链上执行操作。
    

## 三.配置ZetaChain开发环境

### 1\. 配置Ubuntu远程开发环境（以下所有操作都在远程环境中进行）

(1)具体的视频资料：[wsl + vscode](https://www.bilibili.com/video/BV1fu4m1A79r/?spm_id_from=333.1007.top_right_bar_window_custom_collection.content.click&vd_source=429af1a95897362b1265c3245c2759bb)

(2)在资源管理器中查看远程环境中的文件：

```
在地址栏输入（只能是wsl2）：
\\wsl$
然后回车就行
```

(3)查看当前的wsl版本

```
wsl --list --verbose
输出示例：
  NAME            STATE           VERSION
* Ubuntu-22.04    Running         2
  Debian          Stopped         1
```

### 2.下载Foundry

在远程环境中使用以下命令（速度巨慢）

```
curl -L https://foundry.paradigm.xyz | bash
```

### 3.下载Node.js

官网命令参考：适用于Linux且使用nvm和npm的Node.js

```
# 下载并安装 nvm：
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# 代替重启 shell
\. "$HOME/.nvm/nvm.sh"

# 下载并安装 Node.js：
nvm install 24

# 验证 Node.js 版本：
node -v # Should print "v24.11.1".

# 验证 npm 版本：
npm -v # Should print "11.6.2".

```

但是在第一句命令就遇到了错误（悲~）：

```
fatal: unable to access 'https://github.com/nvm-sh/nvm.git/': GnuTLS recv error (-110): The TLS connection was not properly terminated.
Failed to clone nvm repo. Please report this!
```

以下是AI给出的解决方案，亲测可用

```
# 1. 手动克隆 nvm 仓库到 ~/.nvm
git clone https://github.com/nvm-sh/nvm.git ~/.nvm

# 2. 激活 nvm（临时）
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # 加载 nvm

# 3. 添加到 shell 配置文件（永久生效）
echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.bashrc
echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.bashrc
echo '[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"' >> ~/.bashrc

# 4. 重新加载配置
source ~/.bashrc

# 5.安装完成后验证
nvm --version
nvm install --lts
nvm use --lts
node -v
npm -v
```

## 四.注册Qwen 账号

控制台入口：[阿里云控制台](https://home.console.alibabacloud.com/home/dashboard/ProductAndService)
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->
