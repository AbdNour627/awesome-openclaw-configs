# 常见坑和解决方案

> 本文整理了 OpenClaw 配置过程中最常见的问题和解决方法。

## 1. Gateway 启动失败：配置验证错误

**症状：** Gateway 拒绝启动，只有 `openclaw doctor` 等诊断命令可用。

**原因：** OpenClaw 对配置有严格的 schema 验证，不允许未知字段、错误类型或无效值。

**解决：**
```bash
# 查看具体报错
openclaw doctor

# 自动修复
openclaw doctor --fix

# 或手动编辑配置
nano ~/.openclaw/openclaw.json
```

**预防：** 使用 JSON5 格式，善用注释标注每个字段用途。

---

## 2. 模型名大小写敏感

**症状：** `Unknown model: minimax/minimax-m2.1`

**原因：** 模型 ID 是大小写敏感的。

**正确写法：**
- ✅ `minimax/MiniMax-M2.1`
- ❌ `minimax/minimax-m2.1`
- ✅ `moonshot/kimi-k2.5`
- ✅ `zai/glm-5`

**排查：**
```bash
openclaw models list
```

---

## 3. Moonshot vs Kimi Coding 密钥不互通

**症状：** 用 Moonshot 的 key 调 Kimi Coding 模型报错（反之亦然）。

**原因：** Moonshot 和 Kimi Coding 是两个独立的 provider：
- Moonshot → `moonshot/kimi-k2.5`，端点 `api.moonshot.ai/v1`
- Kimi Coding → `kimi-coding/k2p5`，端点不同

**解决：** 分别获取两个 API Key，分别配置。

---

## 4. 国内网络访问超时

**症状：** 使用国际端点时请求超时或连接失败。

**解决：**
- Moonshot 使用 `.cn` 端点：`https://api.moonshot.cn/v1`
- MiniMax 使用 `.com` 端点：`https://api.minimaxi.com/anthropic`
- 或使用 OpenRouter 统一代理

---

## 5. Qwen OAuth 令牌过期

**症状：** Qwen 模型调用失败，提示认证错误。

**解决：**
```bash
# 重新登录
openclaw models auth login --provider qwen-portal --set-default
```

令牌会自动刷新，但如果刷新失败需要重新认证。

---

## 6. WhatsApp 连接断开

**症状：** WhatsApp 消息不再收到回复。

**解决：**
```bash
# 检查状态
openclaw gateway status

# 重新连接
openclaw channels login --channel whatsapp

# 重启 Gateway
openclaw gateway restart

# 查看日志
openclaw logs --follow
```

---

## 7. 飞书事件订阅保存失败

**症状：** 飞书长连接事件订阅无法保存。

**原因：** 配置事件订阅时 Gateway 必须正在运行。

**解决：**
1. 先运行 `openclaw channels add` 配置飞书
2. 启动 Gateway：`openclaw gateway`
3. 然后再去飞书开放平台配置事件订阅

---

## 8. 心跳过于频繁 / Token 消耗大

**症状：** API 消耗快速增长，心跳导致 token 浪费。

**解决：**
```json5
{
  agents: {
    defaults: {
      heartbeat: {
        every: "2h",  // 降低频率
        activeHours: { start: "08:00", end: "22:00" },  // 限制活跃时间
      },
    },
  },
}
```

使用免费模型（Qwen OAuth）跑心跳也是好策略。

---

## 9. 配置文件被 Gateway 锁定

**症状：** 修改配置文件后不生效。

**说明：** Gateway 支持配置热重载，通常修改会自动生效。如果不生效：

```bash
openclaw gateway restart
```

---

## 10. Ollama 模型不显示

**症状：** `openclaw models list` 看不到 Ollama 模型。

**前提条件：**
1. Ollama 服务正在运行
2. 设置了 `OLLAMA_API_KEY`（任意值即可）
3. 没有显式定义 `models.providers.ollama`（否则跳过自动发现）

```bash
# 检查 Ollama 状态
ollama list

# 设置环境变量
export OLLAMA_API_KEY="ollama-local"

# 重启 Gateway
openclaw gateway restart
```
