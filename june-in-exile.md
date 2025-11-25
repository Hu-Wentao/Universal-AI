---
timezone: UTC+8
---

# 陳麒鈞

**GitHub ID:** june-in-exile

**Telegram:** @june_in_exile

## Self-introduction

A cross-disciplinary self-learner who transitioned from marketing to blockchain engineering, with a total of four years of development experience: 1 year as a Golang backend developer at a startup exchange and 2.5 years in full-stack blockchain development. Experienced in leading hackathon teams and designing system architectures. Actively involved in the Web3 community in Taiwan.

## Notes

<!-- Content_START -->
# 2025-11-25
<!-- DAILY_CHECKIN_2025-11-25_START -->
## ZetaChain 簡明摘要

### 核心功能與優勢

-   **通用跨鏈 (Universal Interoperability):** ZetaChain 是一個去中心化的 **POS** 區塊鏈（基於 Cosmos SDK/Comet BFT），能夠在多個異構鏈之間（包括 **EVM 鏈、Solana、Sui、TON 甚至比特幣**）實現**跨鏈調用**。
    
-   **原生資產交易:** 允許用戶直接使用各區塊鏈的**實際原生資產**進行交易，無需使用封裝（wrapped）或合成（synthetic）代幣。
    
-   **Gasless 解決方案:** 部署在 ZetaChain 上的**通用應用程式**在被已連接鏈調用時，**僅需在該已連接鏈上支付 Gas 費用**，解決了傳統跨鏈/合約調用中交易雙方都需要支付 Gas 的問題。
    
-   **開發者友好:** 開發環境與 **EVM 相容**，可使用熟悉的開發工具。
    
-   **向前遷移 (Forward Migration):** 新區塊鏈加入時，通用應用程式無需修改原始碼或進行額外工作即可通用。
    

* * *

### 💻 開發環境與工具

ZetaChain CLI

-   **用途:** ZetaChain 的主要工具，用於跨鏈調用、轉移代幣、追蹤交易、帳戶管理和查詢餘額等。
    
-   **安裝先決條件:** 需確保已安裝 **Node.js、Yarn、Git、jq 和 Foundry**。
    
-   **安裝指令:** `npm install -g zetachain`
    
-   **驗證指令:** `zetachain query chains list`
    

Localnet (本地開發環境)

-   **定義:** 一個包含 ZetaChain、EVM、Solana、Sui 和 TON 的**獨立環境**，是建立和測試通用應用程式最快的方法。
    
-   **運作:** Localnet 運行時會為多個鏈創建節點，並預部署核心協議合約和 ZRC-20 代幣等。
    
-   **注意:** 執行 `npx zetachain localnet start` 等指令後，環境會進入**監聽狀態**，此為正常現象，不應關閉。
    

* * *

### ⚙️ 跨鏈調用範例 (Hello Contract)

-   **合約:** 一個簡單的 `Universal` 合約，繼承 `UniversalContract` 並實作 `onCall` 函數。
    
-   **安全性:** `onCall` 函數使用 `onlyGateway` 修飾符，確保它僅作為對已連接鏈上調用的響應而被調用，以信任函數參數。
    
-   **流程 (EVM 到 ZetaChain):** 從 EVM 鏈發送訊息，通過 **Gateway** 傳輸到 ZetaChain 上的 `Universal` 合約，觸發 `onCall` 執行。
    
-   **Testnet 部署注意事項:**
    
    -   部署 Universal 合約到 **ZetaChain Testnet** 需要錢包有 **ZETA 代幣**。
        
    -   從 **Base Sepolia** 發送訊息需要錢包有該鏈的 **ETH** 以支付訊息傳遞費用。
        
    -   可以使用 `npx zetachain query cctx --hash [Tx Hash]` 追蹤跨鏈交易狀態（CCTX）。
<!-- DAILY_CHECKIN_2025-11-25_END -->
<!-- Content_END -->
