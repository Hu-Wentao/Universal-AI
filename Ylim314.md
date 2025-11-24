---
timezone: UTC+8
---

# ChaplinX

**GitHub ID:** Ylim314

**Telegram:** @Tikey19

## Self-introduction

本科大三区块链工程在读

## Notes

<!-- Content_START -->
# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->
### 📝 通用 AI 残酷共学 - Day 1 学习日志

📅 日期： 2025.11.24

👤 学员： ChaplinX

✅ 进度： 完成环境配置 (Module 0) / 跑通 AI 意图识别与链上交互原型 (Module 3 & 4)

🚀 核心成果

今天完成了一个 **Read-Only AI Agent** 的最小可行性产品 (MVP)，实现了从“自然语言指令”到“链上状态检查”的完整闭环。

**项目架构：**

1.  **Agent Brain (Python + Qwen-Plus):** 通过 System Prompt 工程，强制 LLM 输出严格的 JSON 格式（Action/Token/Amount/Chain），解决了自然语言到机器语言的非结构化转换问题。
    
2.  **Agent Hand (Web3.py + ZetaChain Athens-3):** 实现了 RPC 连接、地址校验和余额查询逻辑。
    

🛠️ 踩坑与解决方案 (Troubleshooting)

**1\. Web3.py 的 Checksum 地址校验机制**

-   **问题描述：** 在调用 `w3.eth.get_balance(address)` 时报错 `web3.exceptions.InvalidAddress: ...only accepts checksum addresses`。
    
-   **原因分析：** Web3.py 强制要求 EIP-55 格式的地址校验和（即大小写混合），而我直接使用了全小写的测试网地址。这是为了防止转账错误的安全机制，但在开发初期容易被忽略。
    
-   **解决方案：** 在传入任何地址前，必须经过格式化处理：
    
    Python
    
    ```
    # 修复前：直接调用报错
    # balance = w3.eth.get_balance(address)
    
    # 修复后：增加一步转换
    checksum_address = w3.to_checksum_address(address)
    balance = w3.eth.get_balance(checksum_address)
    ```
    

**2\. 多环境下的 RPC 隔离**

-   **问题描述：** 初期 MetaMask 和代码连接的是 ZetaChain Mainnet (ChainID 7000)，导致测试币到账后查不到余额。
    
-   **复盘：** 必须严格区分开发环境。代码中已固化测试网 RPC：`https://zetachain-athens-evm.blockpi.network/v1/rpc/public` (ChainID 7001)。
    

**3\. Python 环境依赖管理**

-   **经验：** 在 VS Code 中必须显式指定解释器路径（如 Anaconda 环境），避免调用到 Windows Store 自带的空壳 Python 导致 `ModuleNotFoundError`。
    

🔮 明日计划

目前 Agent 只能“看”不能“动”。

-   **计划 1：** 生成本地钱包账户 (Account)，导出私钥并安全配置到 `.env`。
    
-   **计划 2：** 实现 `build_transaction` 和 `sign_transaction`，让 AI 真的能发出一笔上链交易。
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->
