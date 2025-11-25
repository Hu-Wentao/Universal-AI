---
timezone: UTC-8
---

# David

**GitHub ID:** yedeyu

**Telegram:** @yedeyu

## Self-introduction

Web3 新手

## Notes

<!-- Content_START -->
# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->
官方文档

[https://www.zetachain.com/docs/developers/tutorials/intro](https://www.zetachain.com/docs/developers/tutorials/intro)

\## 手动安装环境

<details>

<summary>Prerequisites</summary>

Before you begin, make sure your system is set up with the following tools:

\* **Node.js** (v21 or later recommended): Required to run the ZetaChain CLI and manage JavaScript dependencies.

\* **Yarn** or **npm**: Package managers used to install and update project libraries. Either works, use whichever you prefer.

\* **Git**: Essential for managing your project source code and collaborating with others.

\* **jq**: A lightweight command-line JSON processor, useful for parsing Localnet output and writing shell scripts.

\* **Foundry**: A fast, modular toolkit for Ethereum development. You’ll use it to compile contracts, manage dependencies, and run Localnet.

\`\`\`

$ node --version

v22.21.1

$ yarn --version

1.22.22

$ jq --version

jq-1.7

$ foundryup --version

zsh: command not found: foundryup

\`\`\`

</details>

<details>

<summary>Install `foundryup`</summary>

\`\`\`

$ curl -L [https://foundry.paradigm.xyz](https://foundry.paradigm.xyz) | bash

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current

                                 Dload  Upload   Total   Spent    Left  Speed

100   167  100   167    0     0   1741      0 --:--:-- --:--:-- --:--:--  1757

100  2198  100  2198    0     0  10234      0 --:--:-- --:--:-- --:--:-- 10234

Installing foundryup...

Detected your preferred shell is bash and added foundryup to PATH.

Run 'source /home/codespace/.bashrc' or start a new terminal session to use foundryup.

Then, simply run 'foundryup' to install Foundry.

\`\`\`

I use zsh, so

\`\`\`

echo 'export PATH="$PATH:/home/codespace/.foundry/bin"' >> /home/codespace/.zshrc

\`\`\`

After running this command, reload your shell configuration with `source /home/codespace/.zshrc` or restart your terminal for the PATH change to take effect.

In a new shell:

\`\`\`

$ foundryup

.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx

 ╔═╗ ╔═╗ ╦ ╦ ╔╗╔ ╔╦╗ ╦═╗ ╦ ╦         Portable and modular toolkit

 ╠╣  ║ ║ ║ ║ ║║║  ║║ ╠╦╝ ╚╦╝    for Ethereum Application Development

 ╚   ╚═╝ ╚═╝ ╝╚╝ ═╩╝ ╩╚═  ╩                 written in Rust.

.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx

Repo       : [https://github.com/foundry-rs/foundry](https://github.com/foundry-rs/foundry)

Book       : [https://book.getfoundry.sh/](https://book.getfoundry.sh/)

Chat       : [https://t.me/foundry\_rs/](https://t.me/foundry_rs/)

Support    : [https://t.me/foundry\_support/](https://t.me/foundry_support/)

Contribute : [https://github.com/foundry-rs/foundry/blob/HEAD/CONTRIBUTING.md](https://github.com/foundry-rs/foundry/blob/HEAD/CONTRIBUTING.md)

.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx.xOx

foundryup: checking if foundryup is up to date...

foundryup: foundryup is up to date.

foundryup: installing foundry (version stable, tag stable)

foundryup: checking if forge, cast, anvil, and chisel for stable version are already installed

#################################################################################################### 100.0%

foundryup: found attestation for stable version, downloading attestation artifact, checking...

#################################################################################################### 100.0%

foundryup: binaries not found or do not match expected hashes, downloading new binaries

foundryup: downloading forge, cast, anvil, and chisel for stable version

#################################################################################################### 100.0%

forge

cast

anvil

chisel

foundryup: downloading manpages

#################################################################################################### 100.0%

foundryup: verifying downloaded binaries against the attestation file

foundryup: forge verified ✓

foundryup: cast verified ✓

foundryup: anvil verified ✓

foundryup: chisel verified ✓

foundryup: use - forge 1.4.4-stable (05794498bf 2025-11-03T23:44:21.031788094Z)

foundryup: use - cast 1.4.4-stable (05794498bf 2025-11-03T23:44:21.031788094Z)

foundryup: use - anvil 1.4.4-stable (05794498bf 2025-11-03T23:44:21.031788094Z)

foundryup: use - chisel 1.4.4-stable (05794498bf 2025-11-03T23:44:21.031788094Z)

\`\`\`

\`\`\`

$ foundryup --version

foundryup: 1.4.0

$ forge --version

forge Version: 1.4.4-stable

Commit SHA: 05794498bf47257b144e2e2789a1d5bf8566be0e

Build Timestamp: 2025-11-03T23:44:21.031788094Z (1762213461)

Build Profile: maxperf

\`\`\`

</details>

<details>

<summary>Setting up Environment</summary>

\`\`\`

npm install -g zetachain

\`\`\`

\`\`\`

npm WARN ERESOLVE overriding peer dependency

npm WARN While resolving: @ton/ton@15.4.0

npm WARN Found: @ton/core@0.60.1

npm WARN node\_modules/zetachain/node\_modules/@zetachain/toolkit/node\_modules/@ton/core

npm WARN   @ton/core@"^0.60.1" from @zetachain/toolkit@16.3.0

npm WARN   node\_modules/zetachain/node\_modules/@zetachain/toolkit

npm WARN     @zetachain/toolkit@"16.3.0" from zetachain@7.4.0

npm WARN     node\_modules/zetachain

npm WARN 

npm WARN Could not resolve dependency:

npm WARN peer @ton/core@">=0.62.0 <1.0.0" from @ton/ton@15.4.0

npm WARN node\_modules/zetachain/node\_modules/@zetachain/toolkit/node\_modules/@ton/ton

npm WARN   @ton/ton@"^15.2.1" from @zetachain/toolkit@16.3.0

npm WARN   node\_modules/zetachain/node\_modules/@zetachain/toolkit

npm WARN 

npm WARN Conflicting peer dependency: @ton/core@0.62.0

npm WARN node\_modules/@ton/core

npm WARN   peer @ton/core@">=0.62.0 <1.0.0" from @ton/ton@15.4.0

npm WARN   node\_modules/zetachain/node\_modules/@zetachain/toolkit/node\_modules/@ton/ton

npm WARN     @ton/ton@"^15.2.1" from @zetachain/toolkit@16.3.0

npm WARN     node\_modules/zetachain/node\_modules/@zetachain/toolkit

npm WARN deprecated rimraf@3.0.2: Rimraf versions prior to v4 are no longer supported

npm WARN deprecated glob@7.2.3: Glob versions prior to v9 are no longer supported

npm WARN deprecated glob@7.2.3: Glob versions prior to v9 are no longer supported

npm WARN deprecated glob@7.2.3: Glob versions prior to v9 are no longer supported

npm WARN deprecated inflight@1.0.6: This module is not supported, and leaks memory. Do not use it. Check out lru-cache if you want a good and tested way to coalesce async requests by a key value, which is much more comprehensive and powerful.

npm WARN deprecated glob@8.1.0: Glob versions prior to v9 are no longer supported

npm WARN deprecated glob@7.2.3: Glob versions prior to v9 are no longer supported

npm WARN deprecated sudo-prompt@9.2.1: Package no longer supported. Contact Support at [https://www.npmjs.com/support](https://www.npmjs.com/support) for more info.

npm WARN deprecated @uniswap/v3-staker@1.0.0: Please upgrade to 1.0.1

npm WARN deprecated @uniswap/swap-router-contracts@1.3.1: Package no longer supported. Contact Support at [https://www.npmjs.com/support](https://www.npmjs.com/support) for more info.

added 1289 packages in 2m

\`\`\`

\`\`\`

zetachain query chains list

\`\`\`

\`\`\`

$ zetachain query chains list

✔ Successfully fetched 13 supported chains, 32 tokens, and 13 chain params

┌──────────┬────────────────────┬───────┬──────────────────────────────────┐

│ Chain ID │ Chain Name         │ Count │ Tokens                           │

├──────────┼────────────────────┼───────┼──────────────────────────────────┤

│ 97       │ bsc\_testnet        │ 20    │ USDC.BSC, BNB.BSC                │

├──────────┼────────────────────┼───────┼──────────────────────────────────┤

│ 7001     │ zeta\_testnet       │ 3     │ -                                │

├──────────┼────────────────────┼───────┼──────────────────────────────────┤

│ 11155111 │ sepolia\_testnet    │ 14    │ ETH.ETHSEP, USDTT.SEPOLIA,       │

│          │                    │       │ USDC.ETHSEP, USDCT.SEPOLIA       │

├──────────┼────────────────────┼───────┼──────────────────────────────────┤

│ 80002    │ amoy\_testnet       │ 32    │ POL.AMOY, USDC.AMOY              │

├──────────┼────────────────────┼───────┼──────────────────────────────────┤

│ 84532    │ base\_sepolia       │ 32    │ ETH.BASESEP, USDCT.BASESEP,      │

│          │                    │       │ USDTT.BASESEP, USDC.BASESEP      │

├──────────┼────────────────────┼───────┼──────────────────────────────────┤

│ 901      │ solana\_devnet      │ 32    │ SOL.SOL, USDC.SOL                │

├──────────┼────────────────────┼───────┼──────────────────────────────────┤

│ 18333    │ btc\_signet\_testnet │ 2     │ sBTC.BTC                         │

├──────────┼────────────────────┼───────┼──────────────────────────────────┤

│ 18334    │ btc\_testnet4       │ 10    │ tBTC.BTC                         │

├──────────┼────────────────────┼───────┼──────────────────────────────────┤

│ 421614   │ arbitrum\_sepolia   │ 5     │ USDTT.ARBSEP, UPKRW.ARBSEP,      │

│          │                    │       │ ETH.ARBSEP, USDC.ARBSEP,         │

│          │                    │       │ USDCT.ARBSEP                     │

├──────────┼────────────────────┼───────┼──────────────────────────────────┤

│ 43113    │ avalanche\_testnet  │ 20    │ USDC.FUJI, USDCT.FUJI,           │

│          │                    │       │ HanaKRW.FUJI, AVAX.FUJI,         │

│          │                    │       │ USDTT.FUJI                       │

├──────────┼────────────────────┼───────┼──────────────────────────────────┤

│ 2015141  │ ton\_testnet        │ 1     │ TON.TON                          │

├──────────┼────────────────────┼───────┼──────────────────────────────────┤

│ 103      │ sui\_testnet        │ 1     │ SUI.SUI, USDC.SUI                │

├──────────┼────────────────────┼───────┼──────────────────────────────────┤

│ 1001     │ kaia\_testnet       │ 1     │ KBKRW.KAIROS, TSKRW.KAIROS,      │

│          │                    │       │ KAIA.KAIROS                      │

└──────────┴────────────────────┴───────┴──────────────────────────────────┘

Note: Count refers to the number of confirmations required for a transaction

from that connected chain to be observed

\`\`\`

</details>

\## 使用 `Dev Container`

示例仓库：

[https://github.com/yedeyu/ZetaChain-Codespace/](https://github.com/yedeyu/ZetaChain-Codespace/)

<details>

<summary>查看相关文件</summary>

`./devcontainer/devcontainer.json`

\`\`\`json

{

"name": "ZetaChain Environment",

// 使用官方 Node.js 22 镜像，满足 prerequisites

"image": "mcr.microsoft.com/devcontainers/javascript-node:1-22-bookworm",

// 安装系统级依赖 (jq)

"features": {

"ghcr.io/devcontainers-contrib/features/apt-packages:1": {

"packages": "jq"

}

},

// 创建容器后运行的脚本 (安装 Foundry 和 ZetaChain CLI)

"postCreateCommand": "bash .devcontainer/[setup.sh](http://setup.sh)",

// 这里的设置可选，推荐安装 Solidity 插件

"customizations": {

"vscode": {

"extensions": \[

"JuanBlanco.solidity",

"esbenp.prettier-vscode"

\]

}

},

// 确保使用普通用户 'node' 运行，而不是 root

"remoteUser": "node"

}

\`\`\`

`./devcontainer/setup.sh`

\`\`\`sh

#!/bin/bash

set -e

echo "--- Starting Environment Setup ---"

\# 1. 安装 Foundry (包含 forge, cast, anvil, chisel)

if ! command -v forge &> /dev/null; then

echo "Installing Foundry..."

curl -L [https://foundry.paradigm.xyz](https://foundry.paradigm.xyz) | bash

\# 将 Foundry 添加到当前 PATH (用于脚本后续执行)

export PATH="$PATH:$HOME/.foundry/bin"

\# 运行 foundryup 下载二进制文件

foundryup

\# 将 PATH 永久添加到 bashrc 和 zshrc (确保下次进入终端时可用)

\# 注意：在 javascript-node 镜像中，用户目录通常是 /home/node

echo 'export PATH="$PATH:$HOME/.foundry/bin"' >> $HOME/.bashrc

echo 'export PATH="$PATH:$HOME/.foundry/bin"' >> $HOME/.zshrc

echo "Foundry installed successfully."

else

echo "Foundry is already installed."

fi

\# 2. 安装 ZetaChain CLI

echo "Installing ZetaChain CLI..."

\# 使用 sudo 以避免全局安装时的权限问题 (Codespace 中 sudo 是免密的)

sudo npm install -g zetachain

echo "--- Setup Complete! ---"

echo "Run 'source ~/.zshrc' if commands are not found immediately."

\`\`\`
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->
