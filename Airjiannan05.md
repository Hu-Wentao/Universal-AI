---
timezone: UTC+8
---

# jianlin chen

**GitHub ID:** Airjiannan05

**Telegram:** @none

## Self-introduction

在校计算机大学生一枚，专攻ai前沿技术，有相关的链上开发基础，对区块链加ai的发展有浓厚的兴趣。Blockchain is the future.

## Notes

<!-- Content_START -->
# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->
# DAY1

**学习资料**

-   ZetaChain 总文档
    
-   [https://www.zetachain.com/docs/](https://www.zetachain.com/docs/)
    
-   ZetaChain Developers（入口总览）
    
-   [https://www.zetachain.com/docs/developers](https://www.zetachain.com/docs/developers)
    
-   Qwen 总文档（Quickstart / Key Concepts）
    
-   [https://qwen.readthedocs.io/zh-cn/latest/](https://qwen.readthedocs.io/zh-cn/latest/)
    

# 什么是ZetaChain

目标：不同链之间互联，能够原生访问任何区块链，让加密货币变得像互联网一样易于访问、多样化和互联

ZetaChain 是一个赋能开发者创建通用，能够无缝交互任何区块链的应用。

官网的developer界面

![](https://av1ln7qpa6l.feishu.cn/space/api/box/stream/download/asynccode/?code=ODYzZjU5M2FjMDgyOGIzZTFmMWU5MDMwYzYyZjZmZTlfNFZydGwwZDF0SEIxSzA0VEpPOWJJOTFxWVR2VnQ3MjNfVG9rZW46WFU2ZmJoQ0xmb05lcUd4OGZoWmN5ano1blFlXzE3NjM5Njk2MzM6MTc2Mzk3MzIzM19WNA)

# 环境搭建

## 先决条件

-   [**Node.js**](https://nodejs.org/en)**（推荐v21或更晚版本）：**必须 运行 ZetaChain CLI 并管理 JavaScript 依赖。(node -v)
    
-   **Yarn或者NPM：**用于安装和 更新项目库。两种方法都可以，随你喜欢。(npm version)
    
-   [**Git**](https://git-scm.com/)**:**管理项目资源必不可少 编程和与他人协作。
    
-   [**JQ**](https://jqlang.org/)**:**一个轻量级命令行JSON处理器， 对于解析Localnet输出和编写shell脚本非常有用。(win bash:winget install jqlang.jq)
    
-   [**Foundry**](https://getfoundry.sh/)**:**一个快速、模块化的以太坊工具包 发展。你会用它来编译契约、管理依赖和运行 Localnet。
    

### Windows

在 Windows 上安装 Foundry 需要一些额外的步骤，因为`foundryup` 目前不支持 PowerShell 或命令提示符 (Cmd)。您需要使用 Windows Subsystem for Linux (WSL) 或 Git BASH 来进行安装。\[[1](https://www.google.com/url?sa=E&q=https%3A%2F%2Fvertexaisearch.cloud.google.com%2Fgrounding-api-redirect%2FAUZIYQF7zCQXvNYyf1lIuwj_SykCNnDx-Fs34VfoYyf3ctjVjTHBXDt9T0oqAn542wsnl088smS_Lj9n5l0cI11E24eFj4qehO9A6AVp_pYN5L5ge9jDRaDvVX27gbPWQ6fqk1C7PraRa8LPv4_aAiap)\]\[[2](https://www.google.com/url?sa=E&q=https%3A%2F%2Fvertexaisearch.cloud.google.com%2Fgrounding-api-redirect%2FAUZIYQGzBjoCSkl_rKeTK2BbapcE-MR8_4zguUZ9YJcyYxxAba1j2J8NNYf7Ngy3woDdVyZklosYbRjydKx1rmO2L3EchMCOQmvlb60R0ca6L4t2ptSATdjLG3pCcg9-kkO_oWYGTzb3fsmBgw9C8qVaXox6pr0W8S2782AXTvGgkg7KxFeIBh6SWdN_l4YBnA%3D%3D)\]

**步骤 1：安装 Windows Subsystem for Linux (WSL)**

1.  打开 PowerShell 或 Windows 命令提示符，并以管理员身份运行。
    
2.  输入以下命令来安装 WSL：
    
3.  codeBash
    

```Plain
wsl --install
```

**步骤 2：在 WSL 中安装 Foundry**

1.  打开您的 WSL 终端 (例如 Ubuntu)。
    
2.  运行与 macOS 和 Linux 相同的 `curl` 命令来安装 `foundryup`：
    

```Plain
curl -L https://foundry.paradigm.xyz | bash
```

1.  按照屏幕上的指示完成安装，然后运行 `foundryup` 来安装 Foundry 工具链：
    

```Plain
foundryup
```

## 环境建设

Install the ZetaChain CLI:

```Shell
npm install -g zetachain
```

Run:

```Shell
zetachain query chains list
```

这个命令可以打印所有当前连接在ZetaChain上的链条

对于本地开发，推荐运行Localnet，一个自给自足的平台。该环境包括ZetaChain、EVM、Solana、Sui和TON。Localnet 是构建和测试通用应用最快的方法，无需依赖公共测试网。

注意：必须要有Foundry才可以运行Localnet

# qwen账号注册和进入控制台

1.进入阿里云百炼，注册，创建API key即可

[https://bailian.console.aliyun.com/?tab=model#/model-market/detail/qwen3-max](https://bailian.console.aliyun.com/?tab=model#/model-market/detail/qwen3-max)
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->
