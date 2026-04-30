# HOC三层架构

> Hermes + OpenClaw + Claude Code 分工协作架构

---

## 架构图

```mermaid
graph TD
    subgraph "H — Hermes Agent（CEO/决策/创作）"
        A1[选题策划]
        A2[文案撰写]
        A3[内容排期]
        A4[决策判断]
    end
    
    subgraph "O — OpenClaw（执行层）"
        B1[浏览器自动化]
        B2[peekaboo + 真实Chrome]
        B3[文件操作]
    end
    
    subgraph "C — Claude Code（开发层）"
        C1[代码开发]
        C2[复杂脚本]
        C3[技术方案]
    end
    
    A1 --> B1
    A2 --> B1
    A3 --> B1
    A4 --> C1
    
    B1 --> D[小红书平台]
    B2 --> D
    
    style A1 fill:#7c3aed,color:#fff
    style A2 fill:#7c3aed,color:#fff
    style A3 fill:#7c3aed,color:#fff
    style A4 fill:#7c3aed,color:#fff
    style B1 fill:#2563eb,color:#fff
    style B2 fill:#2563eb,color:#fff
    style B3 fill:#2563eb,color:#fff
    style C1 fill:#059669,color:#fff
    style C2 fill:#059669,color:#fff
    style C3 fill:#059669,color:#fff
```

## 各层职责

| 层级 | 角色 | 模型 | 职责 |
|:----:|:----:|:----:|------|
| **H** | Hermes | Kimi/GLM | 决策/创作/编排 — 选题、文案、排期 |
| **O** | OpenClaw | DeepSeek | 执行 — 浏览器操作、文件处理 |
| **C** | Claude Code | Claude | 开发 — 代码、脚本、技术方案 |

## 任务分级

| 复杂度 | 耗时 | 处理层 | 示例 |
|:------:|:----:|:------:|------|
| 简单 | 秒级 | Hermes 内置工具 | 选题判断、文案审核 |
| 中等 | 十秒级 | OpenClaw | 内容发布、图片上传 |
| 复杂 | 分钟级 | Claude Code | 技术方案编写、CDP脚本开发 |

## 原则

- **统一入口**：所有任务从一个对话入口发起，不分拆独立对话
- **按需委派**：简单任务Hermes自己做，复杂任务委派下层
- **逐层闭环**：每层完成自己的任务后返回结果给上层
