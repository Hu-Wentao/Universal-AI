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
