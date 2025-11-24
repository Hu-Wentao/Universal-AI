---
timezone: UTC+8
---

# JunzheLiu

**GitHub ID:** JunZ-Leo

**Telegram:** @junzhecc

## Self-introduction

期望能够通过这次的残酷残酷共学提高下自己的技术能力，并认识更多的新朋友🤞

## Notes

<!-- Content_START -->
# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->
\## 概要

在本地 ZetaChain localnet (anvil) 上进行了实践操作，目标是熟悉本地链交互、ERC-20 查询与转账，（利用VSCode远程SSH到Linux服务器进行开发）>

\- 创建并运行 Node 工具 `scripts/interact.js`（查看 ETH、查询 ERC‑20、发送 ERC‑20）。

\- 查询 `USDC.ETH` 与 `zetaToken` 余额。

\- 生成临时地址并从默认钱包转出 1 USDC（已成功，交易已确认）。

\- 抓取并保存交易对象与回执到 `tx.json` 与 `receipt.json`。

\## 环境与关键信息

\- Local RPC: `http://127.0.0.1:8545`

\- Default wallet: `0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266`

\- Default private key (anvil): `0xac0974be...f2ff80`

\- USDC.ETH (local): `0x1fA02b2d6A771842690194Cf62D91bdd92BfE28d`

\- zetaToken (local): `0x7a2088a1bFc9d81c55368AE168C2C02570cB814F`

\- 临时收款地址（示例）: `0x211A65Cd9CE07Cc64Ba712228dcd4489FB013ECc`

\- 转账交易哈希: `0x6ca5c4768d01f9a9bb30a4afa6a5051f5d13036d47bfba3872b9e8a6fdd5b2dd`

保存文件（路径均在 `/root/canku`）

\- `scripts/interact.js` — 交互脚本（已创建）

\- `tx.json` — 保存的交易对象

\- `receipt.json` — 保存的交易回执（包含 logs）

\## 已执行的可复现命令

1\. 安装并运行交互脚本（根目录）：

```
cd /root/canku
npm install --no-audit --no-fund
node scripts/interact.js balance
```

2\. 查询 ERC‑20 余额（注意 --，防止 minimist 把 0x 地址解析为数字）：

```
bash
node scripts/interact.js token -- 0x1fA02b2d6A771842690194Cf62D91bdd92BfE28d
```

3\. 生成临时收款地址：

```
bash
node -e "const ethers=require('ethers');console.log(ethers.Wallet.createRandom().address)"
```

4\. 发送 1 USDC（示例）：

```
bash
node scripts/interact.js send -- 0x1fA02b2d6A771842690194Cf62D91bdd92BfE28d 0x211A65Cd9CE07Cc64Ba712228dc
```

5\. 获取并保存交易信息

```
`bash
cat tx.json
cat receipt.json
```

\## 关键代码片段

\- interact.js: 查询 ETH 余额与 ERC‑20, 发送 ERC‑20

```
`js
const ethers = require('ethers');
const provider = new ethers.providers.JsonRpcProvider(process.env.RPC_URL || 'http://127.0.0.1:8545');
const wallet = new ethers.Wallet(process.env.PRIVATE_KEY || '<priv>', provider);

// 查询 ETH
const bal = await provider.getBalance(await wallet.getAddress());
console.log('ETH', ethers.utils.formatEther(bal));

// 查询 token
const token = new ethers.Contract(tokenAddress, ['function balanceOf(address) view returns (uint256)', 'f>
const raw = await token.balanceOf(await wallet.getAddress());
const decimals = await token.decimals();
console.log('token balance', ethers.utils.formatUnits(raw, decimals));

// 发送 token
const tWithSigner = token.connect(wallet);
const tx = await tWithSigner.transfer(recipient, ethers.utils.parseUnits(amountStr, decimals));
await tx.wait();
```

\## 关于 `call` 示例（跨链）

\- `call` 示例位于 `/root/canku/call`，包含 `contracts/Universal.sol` 與 `contracts/Connected.sol` 以及 CL>

\- 用 Foundry `forge`) 成功编译`forge build`），并能够用 `forge create` 或脚本把合约部署到本地 RP>

\- 用 `forge` 部署 `Universal` 和 `Connected` 到 localnet 并运行 `commands/connected/call` 示例（我已就\[>

\- 或基于 localnet 上已存在的合约（registry）进行交互示例。

示例 Foundry 部署命令：

```
bash
# 在 /root/canku/call
forge build
forge create contracts/Universal.sol:Universal --rpc-url http://127.0.0.1:8545 --private-key <PRIVATE_KEY>
forge create contracts/Connected.sol:Connected --rpc-url http://127.0.0.1:8545 --private-key <PRIVATE_KEY>
```
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->
