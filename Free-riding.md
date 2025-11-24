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
