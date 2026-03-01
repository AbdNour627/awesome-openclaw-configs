# 性能优化指南

> 让你的 OpenClaw 跑得更快、更省钱。

## 1. 选对模型

| 场景 | 推荐模型 | 理由 |
|------|---------|------|
| 日常聊天 | `moonshot/kimi-k2.5` | 快速、免费额度 |
| 编程任务 | `moonshot/kimi-k2-thinking` | 推理能力强 |
| 复杂任务 | `minimax/MiniMax-M2.1` | 综合能力强 |
| 省钱首选 | `qwen-portal/coder-model` | 完全免费 |
| 离线场景 | `ollama/qwen2.5-coder:32b` | 零成本 |

## 2. Fallback 链：价格从低到高

```json5
{
  agents: {
    defaults: {
      model: {
        primary: "moonshot/kimi-k2.5",        // 先用免费的
        fallbacks: [
          "qwen-portal/coder-model",          // 降级到免费 OAuth
          "minimax/MiniMax-M2.1",             // 再降级到付费
        ],
      },
    },
  },
}
```

## 3. 消息队列优化

避免用户连续发多条消息导致多次 API 调用：

```json5
{
  routing: {
    queue: {
      mode: "collect",     // 收集模式：等一会再处理
      debounceMs: 1500,    // 1.5 秒内的消息合并处理
      cap: 20,             // 最多收集 20 条
      drop: "summarize",   // 超出时自动摘要
    },
  },
}
```

## 4. 会话管理

定期清理会话，避免上下文过长：

```json5
{
  session: {
    reset: {
      mode: "daily",       // 每天重置
      atHour: 4,           // 凌晨 4 点
      idleMinutes: 60,     // 或空闲 60 分钟后重置
    },
    maintenance: {
      pruneAfter: "7d",    // 7 天前的会话存档清理
      maxEntries: 200,     // 最多保留 200 条
      rotateBytes: "5mb",  // 文件超过 5MB 轮转
    },
  },
}
```

## 5. 心跳频率调优

心跳每次都消耗 token。根据需求调整：

| 场景 | 推荐间隔 |
|------|---------|
| 活跃使用（白天） | 30m |
| 轻度使用 | 1h - 2h |
| 省钱模式 | 4h 或关闭 |

```json5
{
  agents: {
    defaults: {
      heartbeat: {
        every: "2h",
        activeHours: { start: "08:00", end: "22:00" },
      },
    },
  },
}
```

## 6. 图片处理优化

图片会消耗大量 vision token。降低分辨率可以省钱：

```json5
{
  agents: {
    defaults: {
      // 图片最大尺寸（默认 1200px，降低可省 token）
      imageMaxDimensionPx: 800,
    },
  },
}
```

## 7. 本地模型 + 云端混合

日常用本地模型，复杂任务手动切换到云端：

```json5
{
  agents: {
    defaults: {
      model: { primary: "ollama/qwen2.5-coder:32b" },
      models: {
        "ollama/qwen2.5-coder:32b": { alias: "本地" },
        "moonshot/kimi-k2-thinking": { alias: "云端" },
      },
    },
  },
}
```

使用 `/model 云端` 命令切换。

## 8. 按渠道分配模型

不同渠道使用不同级别的模型：

```json5
{
  channels: {
    modelByChannel: {
      telegram: {
        "-1001234567890": "ollama/qwen2.5-coder:32b",  // 群聊用本地
      },
      whatsapp: {},  // 默认用主模型
    },
  },
}
```
