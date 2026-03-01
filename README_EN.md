<![CDATA[<div align="center">

# 🦞 Awesome OpenClaw Configs

**Curated, ready-to-use config templates for OpenClaw / Clawdbot**

[![GitHub stars](https://img.shields.io/github/stars/ShuyuZ1999/awesome-openclaw-configs?style=social)](https://github.com/ShuyuZ1999/awesome-openclaw-configs)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

[中文](README.md) | English

</div>

---

## What is this?

OpenClaw's `config.json5` is powerful but can be tricky to set up from scratch — especially when integrating Chinese LLM providers (DeepSeek, Kimi, Qwen, GLM, MiniMax, Baidu Qianfan, Xiaomi MiMo), connecting multiple chat channels (WeChat, WhatsApp, Telegram, Feishu/Lark), or configuring automation.

This repo provides **20+ battle-tested config templates** with detailed comments. Copy, paste, customize, done.

---

## Configs

| Category | Configs | Description |
|----------|---------|-------------|
| **Starter** | `minimal`, `recommended` | Get up and running in minutes |
| **China Providers** | `moonshot-kimi`, `deepseek-via-openrouter`, `qwen-free-oauth`, `glm-zai`, `minimax-m2`, `qianfan-baidu`, `xiaomi-mimo` | Configs for popular Chinese LLM providers |
| **Multi-Channel** | `wechat-whatsapp-telegram`, `feishu-enterprise` | Connect multiple chat platforms at once |
| **Automation** | `cron-morning-brief`, `heartbeat-proactive`, `reminder-oneshot` | Scheduled tasks and proactive assistant |
| **Budget** | `free-tier-qwen`, `ollama-local-free`, `smart-fallback` | Zero-cost and cost-optimized setups |
| **Developer** | `github-code-review` | GitHub CI monitoring + auto code review |
| **Smart Home** | `hue-sonos-eight` | Hue + Sonos + Eight Sleep control |
| **Enterprise** | `multi-user-secure` | Multi-user deployment with pairing & routing |

See the [Chinese README](README.md) for full descriptions and directory structure.

---

## Quick Start

```bash
git clone https://github.com/ShuyuZ1999/awesome-openclaw-configs.git
cd awesome-openclaw-configs

# Pick a config and copy it
cp configs/starter/recommended.json5 ~/.openclaw/config.json5

# Edit your API keys and phone number
nano ~/.openclaw/config.json5

# Restart OpenClaw
openclaw gateway restart
```

> ⚠️ All API keys and phone numbers in configs are **placeholders**. Replace them before use.

---

## Tips

- [Common Pitfalls](tips/common-pitfalls.md) — Avoid the most frequent mistakes
- [Performance](tips/performance.md) — Token optimization, model switching
- [Security](tips/security.md) — Key management, production hardening

---

## Related Projects

- [OpenClaw](https://github.com/nichochar/open-claw) — The main OpenClaw repository
- [llm-provider-errors](https://github.com/ShuyuZ1999/llm-provider-errors) — Error code reference for Chinese LLM providers

---

## Contributing

PRs welcome! See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE) © Shuyu Zhang
]]>