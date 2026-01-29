# 🦞 TutuClawdbot — Enhancing Clawdbot with OpenRouter & DingTalk

> [!NOTE]
> 本项目是 [Clawdbot](https://github.com/clawdbot/clawdbot) 的开源增强分支。
> **English speakers:** Please refer to the [Original README](https://github.com/clawdbot/clawdbot) for the basic documentation.

---

**TutuClawdbot** 是一个为您在电脑上运行的 *个人 AI 助手*。它可以通过您常用的社交软件（如：Telegram、钉钉、WhatsApp 等）直接与您交流。它不仅能聊天，还能控制浏览器助手执行任务、管理您的长期记忆。

---

### 🌟 本分支核心增强 (Key Enhancements)

1. **OpenRouter 全面集成 (OpenRouter Integration)**
   - 无需为每个模型厂家单独配置 Key，通过 [OpenRouter](https://openrouter.ai) 即可访问 **Claude 4.5/Sonnet 4.5**, **Gemini 2.0**, **GPT-5** 等前沿模型。
   - **智能路由**: 自动处理认证并支持视觉/长上下文能力。

2. **钉钉 (DingTalk) 流模式支持 (测试中)**
   - 专为国内办公场景开发的 **钉钉 Stream 模式** 插件。
   - **部署极简**: 无需公网 IP 或反向代理，长连接直连。 *（期待您的反馈，未作过多测试因为要开会员）*

3. **Telegram 原生优化**
   - 针对个人使用场景优化的 Telegram 机器人支持，开箱即用。

---

### 📖 快速上手指南 (新手傻瓜版：以 Telegram 为例)

这是为第一次接触项目的用户准备的“保姆级”启动步骤：

#### 1. 准备工作
在开始之前，请先获取以下信息：
- **OpenRouter API Key**: 在 [OpenRouter.ai](https://openrouter.ai/keys) 创建一个密钥
- **Telegram Bot Token** (可选): 在 Telegram 搜索 [@BotFather](https://t.me/BotFather)，发送 `/newbot` 创建机器人并获取 Token

#### 2. 环境安装 (Windows 使用 PowerShell)
```powershell
# 克隆代码
git clone https://github.com/zhaotututu/tutuclawdbot.git
cd tutuclawdbot

# 安装依赖并构建
pnpm install
pnpm build
```

#### 3. 运行配置向导 🚀

> [!WARNING]
> **Windows 用户注意**：Gateway 服务安装需要管理员权限。请以**管理员身份**运行 PowerShell：
> 1. 在开始菜单搜索 "PowerShell"
> 2. 右键点击 → 选择"以管理员身份运行"
> 3. 然后执行以下命令

```powershell
# 设置 OpenRouter Key (向导会用到)
$env:OPENROUTER_API_KEY="您的_OPENROUTER_KEY"

# 启动交互式配置向导
pnpm clawdbot onboard
```

**向导会自动引导您完成：**
- ✅ AI 模型认证配置 (OpenRouter)
- ✅ Gateway 网关设置
- ✅ 聊天频道配置 (Telegram / 钉钉 / WhatsApp 等)
- ✅ 技能和插件安装

#### 4. 启动并配对
```powershell
# 启动 Gateway
pnpm clawdbot gateway --verbose
```

在手机上向您的机器人发送消息，它会回复一个 **配对码** (例如: `ABC123`)

**打开新的终端窗口**，运行配对命令：
```powershell
cd tutuclawdbot
pnpm clawdbot pairing approve telegram ABC123
```

✅ **完成！现在机器人已经彻底属于你了！**

---

## 🦞 Clawdbot 原版功能概览 (Core Subsystems)

### 核心子系统
- **Gateway (网关)**: WebSocket 控制平面，负责处理所有会话、渠道、工具和事件。
- **Pi Agent 运行时**: 负责处理推理、工具流和长短期记忆。
- **多渠道接入**: 原生支持 WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, Microsoft Teams 等。
- **实时 Canvas**: 助手驱动的可视化工作区，实时查看 AI 生成的各种资产。

### 关键组件
- **浏览器控制**: 助手可以启动并自主控制 Chrome/Chromium 浏览器，进行网页截图、操作和上传。
- **技能注册表 (ClawdHub)**: 助手可以自动搜索并拉取社区技能。

### 工作原理示意
```text
Telegram / 钉钉 / Slack / Discord ...
               │
               ▼
┌───────────────────────────────┐
│            Gateway            │
│          (网关控制中心)         │
│     ws://127.0.0.1:18789      │
└──────────────┬────────────────┘
               │
               ├─ Pi 代理引擎 (RPC 模式)
               ├─ 命令行工具 (clawdbot …)
               ├─ WebChat 网页聊天
               ├─ macOS 原生 App
               └─ 移动端节点 (iOS / Android)
```

### 安全模型 (Security)
- **沙箱隔离**: 支持 Docker 隔离模式，确保在群聊或非信任会话中工具运行的安全。
- **权限管理**: 支持基于会话的权限提升（Elevated bash）。

---

## 声明
- 本项目部分代码逻辑参考并增强自官方项目。
- 官方项目链接: [https://github.com/clawdbot/clawdbot](https://github.com/clawdbot/clawdbot)
- 协议: [MIT License](LICENSE)

---
*Created with 🦞 by zhaotututu & Clawd Community.*
