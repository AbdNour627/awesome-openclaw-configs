<![CDATA[<div align="center">

# 🦞 Awesome OpenClaw Configs

**开箱即用的 OpenClaw / Clawdbot 配置模板大全**

[![GitHub stars](https://img.shields.io/github/stars/ShuyuZ1999/awesome-openclaw-configs?style=social)](https://github.com/ShuyuZ1999/awesome-openclaw-configs)
[![GitHub forks](https://img.shields.io/github/forks/ShuyuZ1999/awesome-openclaw-configs?style=social)](https://github.com/ShuyuZ1999/awesome-openclaw-configs/fork)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

[English](README_EN.md) | 中文

</div>

---

## 为什么需要这个项目？

OpenClaw 的配置文件（`config.json5`）功能强大但上手门槛不低——尤其是当你想接入**国产模型**（DeepSeek、Kimi、Qwen、智谱 GLM、MiniMax、百度千帆、小米 MiMo）、连接**多个聊天渠道**（微信、WhatsApp、Telegram、飞书）、或者做**自动化任务**时，从零写配置既费时又容易踩坑。

这个仓库收集了 **20+ 经过实测的配置模板**，覆盖从新手入门到企业部署的各种场景。每个配置都有详细的中文注释，复制粘贴即可使用。

> 💡 **配合使用：** 如果你在国产模型接入过程中遇到 API 错误，可以参考 [llm-provider-errors](https://github.com/ShuyuZ1999/llm-provider-errors) —— 收录了各模型提供者的常见报错和解决方案。

---

## 📁 目录结构

```
configs/
├── starter/          # 🚀 新手入门
├── china-providers/  # 🇨🇳 国产模型接入
├── multi-channel/    # 📱 多渠道聊天
├── automation/       # ⚡ 定时任务 & 自动化
├── budget/           # 💰 省钱 & 免费方案
├── developer/        # 👨‍💻 开发者工具
├── smart-home/       # 🏠 智能家居
└── enterprise/       # 🏢 企业部署
tips/
├── common-pitfalls.md  # 常见踩坑
├── performance.md      # 性能调优
└── security.md         # 安全最佳实践
```

---

## 📋 配置一览

### 🚀 新手入门（Starter）

| 文件 | 说明 |
|------|------|
| [`minimal.json5`](configs/starter/minimal.json5) | 最简配置，3 行搞定，先跑起来再说 |
| [`recommended.json5`](configs/starter/recommended.json5) | 推荐入门配置，Kimi K2.5 + WhatsApp，适合大多数中国用户 |

### 🇨🇳 国产模型接入（China Providers）

| 文件 | 说明 |
|------|------|
| [`moonshot-kimi.json5`](configs/china-providers/moonshot-kimi.json5) | Kimi K2.5 / K2 Thinking 配置，OpenAI 兼容接口 |
| [`deepseek-via-openrouter.json5`](configs/china-providers/deepseek-via-openrouter.json5) | DeepSeek 系列，通过 OpenRouter 网关访问 |
| [`qwen-free-oauth.json5`](configs/china-providers/qwen-free-oauth.json5) | 通义千问 Qwen 免费 OAuth，每天 2000 次，零成本 |
| [`glm-zai.json5`](configs/china-providers/glm-zai.json5) | 智谱 GLM-5 / GLM-4.7，通过 Z.AI 平台接入 |
| [`minimax-m2.json5`](configs/china-providers/minimax-m2.json5) | MiniMax M2.1，Anthropic 兼容 API |
| [`qianfan-baidu.json5`](configs/china-providers/qianfan-baidu.json5) | 百度千帆，一个 Key 访问文心一言全系列 |
| [`xiaomi-mimo.json5`](configs/china-providers/xiaomi-mimo.json5) | 小米 MiMo V2，Anthropic Messages API 兼容 |

### 📱 多渠道聊天（Multi-Channel）

| 文件 | 说明 |
|------|------|
| [`wechat-whatsapp-telegram.json5`](configs/multi-channel/wechat-whatsapp-telegram.json5) | 微信 + WhatsApp + Telegram 三合一，统一管理 |
| [`feishu-enterprise.json5`](configs/multi-channel/feishu-enterprise.json5) | 飞书企业机器人，WebSocket 长连接，无需公网 IP |

### ⚡ 自动化（Automation）

| 文件 | 说明 |
|------|------|
| [`cron-morning-brief.json5`](configs/automation/cron-morning-brief.json5) | 每日早报，每天 8:00 自动推送天气+日历+待办 |
| [`heartbeat-proactive.json5`](configs/automation/heartbeat-proactive.json5) | 心跳主动助手，定期检查邮件/日历，有事才通知 |
| [`reminder-oneshot.json5`](configs/automation/reminder-oneshot.json5) | 一次性定时提醒，触发后自动删除 |

### 💰 省钱 & 免费方案（Budget）

| 文件 | 说明 |
|------|------|
| [`free-tier-qwen.json5`](configs/budget/free-tier-qwen.json5) | 零成本：Qwen 免费 OAuth，无需信用卡 |
| [`ollama-local-free.json5`](configs/budget/ollama-local-free.json5) | 零成本：Ollama 本地模型，完全离线可用 |
| [`smart-fallback.json5`](configs/budget/smart-fallback.json5) | 智能降级：便宜模型打主力，贵模型做兜底 |

### 👨‍💻 开发者（Developer）

| 文件 | 说明 |
|------|------|
| [`github-code-review.json5`](configs/developer/github-code-review.json5) | GitHub CI 监控 + 自动 Code Review |

### 🏠 智能家居（Smart Home）

| 文件 | 说明 |
|------|------|
| [`hue-sonos-eight.json5`](configs/smart-home/hue-sonos-eight.json5) | Hue 灯光 + Sonos 音响 + Eight Sleep 床垫控制 |

### 🏢 企业部署（Enterprise）

| 文件 | 说明 |
|------|------|
| [`multi-user-secure.json5`](configs/enterprise/multi-user-secure.json5) | 多用户安全部署，配对模式 + 渠道路由 |

---

## 🚀 快速使用

### 方式一：直接复制

1. 找到适合你的配置文件
2. 复制内容到你的 OpenClaw 配置文件：
   ```bash
   # 默认路径
   ~/.openclaw/config.json5
   ```
3. 按注释修改 API Key、手机号等参数
4. 重启 OpenClaw：
   ```bash
   openclaw gateway restart
   ```

### 方式二：Clone 后选用

```bash
git clone https://github.com/ShuyuZ1999/awesome-openclaw-configs.git
cd awesome-openclaw-configs

# 比如用推荐入门配置
cp configs/starter/recommended.json5 ~/.openclaw/config.json5

# 修改你的参数
nano ~/.openclaw/config.json5

# 重启
openclaw gateway restart
```

### ⚠️ 注意事项

- 所有配置中的 API Key、手机号等敏感信息都是**占位符**，使用前必须替换
- 建议先看 [`tips/common-pitfalls.md`](tips/common-pitfalls.md) 避免踩坑
- 安全相关请看 [`tips/security.md`](tips/security.md)

---

## 📖 Tips 指南

| 文件 | 内容 |
|------|------|
| [常见踩坑](tips/common-pitfalls.md) | 新手最常遇到的问题和解决方案 |
| [性能调优](tips/performance.md) | 模型切换、Token 优化、并发控制 |
| [安全最佳实践](tips/security.md) | 密钥管理、权限控制、生产环境加固 |

---

## 🤝 贡献

欢迎提交新的配置模板！请阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 了解贡献流程。

---

## 📎 关联项目

| 项目 | 说明 |
|------|------|
| [OpenClaw](https://github.com/nichochar/open-claw) | OpenClaw 主仓库 |
| [llm-provider-errors](https://github.com/ShuyuZ1999/llm-provider-errors) | 国产模型 API 错误代码速查手册，搭配本项目使用 |

---

## 📄 License

[MIT](LICENSE) © Shuyu Zhang
]]>