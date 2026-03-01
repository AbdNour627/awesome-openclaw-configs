# 安全最佳实践

> 保护你的 OpenClaw 实例和数据安全。

## 1. 访问控制：永远不要用 "open" 模式

```json5
// ❌ 危险：任何人都能和你的 AI 聊天
{ channels: { whatsapp: { dmPolicy: "open", allowFrom: ["*"] } } }

// ✅ 安全：配对模式，需要你审批
{ channels: { whatsapp: { dmPolicy: "pairing" } } }

// ✅ 安全：白名单模式
{ channels: { whatsapp: { dmPolicy: "allowlist", allowFrom: ["+86你的号码"] } } }
```

## 2. API Key 管理

### 不要把密钥硬编码在配置文件里

```json5
// ❌ 不推荐：密钥明文写在配置中
{ env: { MOONSHOT_API_KEY: "sk-abc123..." } }

// ✅ 推荐：使用环境变量引用
{ env: { MOONSHOT_API_KEY: "${MOONSHOT_API_KEY}" } }
```

### 使用 OpenClaw 的 auth profile 系统

```bash
# 通过向导安全存储密钥
openclaw onboard --auth-choice moonshot-api-key

# 密钥存储在 ~/.openclaw/auth-profiles.json（不进入配置文件）
```

### 飞书 App Secret 泄露应急

1. 立即在飞书开放平台重置 App Secret
2. 更新 OpenClaw 配置
3. 重启 Gateway

## 3. 群聊安全

```json5
{
  channels: {
    whatsapp: {
      // 群聊白名单：只允许指定群
      groupPolicy: "allowlist",
      groupAllowFrom: ["+86管理员号码"],

      // 群聊必须 @提及 才回复
      groups: { "*": { requireMention: true } },
    },
  },
}
```

## 4. 日志脱敏

```json5
{
  logging: {
    level: "info",
    // 脱敏工具输出（不记录完整的命令执行结果）
    redactSensitive: "tools",
  },
}
```

## 5. 会话存储安全

```json5
{
  session: {
    maintenance: {
      // 定期清理旧会话
      pruneAfter: "7d",
      // 限制存储大小
      maxDiskBytes: "500mb",
      // 归档保留期限
      resetArchiveRetention: "30d",
    },
  },
}
```

## 6. 网络安全

### 飞书 Webhook 绑定

```json5
{
  channels: {
    feishu: {
      // Webhook 只绑定到 localhost（默认）
      // 不要改成 0.0.0.0 除非你知道在做什么
      webhookHost: "127.0.0.1",
    },
  },
}
```

### WhatsApp 重连策略

```json5
{
  web: {
    heartbeatSeconds: 60,
    reconnect: {
      initialMs: 2000,
      maxMs: 120000,
      factor: 1.4,
      jitter: 0.2,
      maxAttempts: 0,  // 0 = 无限重试
    },
  },
}
```

## 7. 多用户环境

在企业/团队部署中：

- **每个用户一个 agent**：通过 `bindings` 隔离用户会话
- **配对审批**：所有新用户必须经过管理员审批
- **日志审计**：开启文件日志，定期检查

```json5
{
  agents: {
    list: [
      { id: "user-alice" },
      { id: "user-bob" },
    ],
  },
  bindings: [
    {
      agentId: "user-alice",
      match: { channel: "feishu", peer: { kind: "direct", id: "ou_alice" } },
    },
    {
      agentId: "user-bob",
      match: { channel: "feishu", peer: { kind: "direct", id: "ou_bob" } },
    },
  ],
}
```

## 8. 安全检查清单

- [ ] DM Policy 不是 `"open"`
- [ ] API Key 没有明文写在配置文件中
- [ ] 群聊设置了白名单或 @提及 要求
- [ ] 日志启用了敏感信息脱敏
- [ ] 会话有自动清理策略
- [ ] 飞书 App Secret 没有泄露到代码仓库
- [ ] Webhook 只绑定在 localhost
- [ ] 定期运行 `openclaw doctor` 检查配置健康
