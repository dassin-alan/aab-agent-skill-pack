---
name: "aab-skill-pack"
description: "AAB Skill Pack v0.2——Agent Skill 体系总控路由，含上下文预算和效率准则"
---

# AAB Skill Pack v0.2

> 为 AAB（文刀同学）定制 Agent Skill 体系

## 核心优先级

1. **省 token** — 避免不必要的上下文扩展，只读需要的
2. **精确编辑** — 一次改一个东西，不重构无关代码
3. **不扫描整个仓库** — 除非明确要求
4. **前端/Demo 任务** → 暗色科技风（参考 aab-frontend-ui）
5. **比赛/Demo 任务** → 优化展示、可信度、评委友好
6. **单文件 HTML** → 全在一个文件，零外部依赖
7. **验证** → 最小针对性检查，不跑全套测试

## Skill 路由表

| 场景 | 使用的 Skill |
|------|-------------|
| Token/额度/上下文快用完了 | `aab-low-token` + `aab-context-discipline` |
| 需要快速执行，跳过探索 | `aab-agent-efficiency` |
| 构建任何 UI / 视觉工作 | `aab-frontend-ui` |
| 构建单文件 HTML Demo | `aab-html-single-file` |
| 比赛/项目包装 | `aab-competition-demo` |
| 浏览器测试 / QA 检查 | `aab-playwright-qa` |
| 提交/备份/版本管理 | `aab-git-workflow` |
| 写或压缩 Prompt | `aab-prompt-optimizer` |
| 设计文档 → 代码 | `aab-design-integration` |

## 默认行为

- 读超过 3 个文件前，用一句话解释为什么
- 改超过 3 个文件前，简要列出
- 跑长命令前，用过滤输出（`| tail -50`）
- 如果一个文件能解决问题，不读第二个
- 用 limit/offset 读文件，不读 2000 行只要 50 行的内容
- 信任工具返回值，不重读文件"确认"编辑

## 上下文预算（自动选择，从最低开始）

| 级别 | 最多文件 | 何时使用 |
|------|---------|----------|
| **Tiny** | 1-2 | 文字/样式/颜色修复 |
| **Normal** | 3-5 | 功能开发，中等改动 |
| **Heavy** | 不限（先列计划） | 用户明确要求全面审计 |

默认：从 Tiny 开始。只在不够时升级。永远不要跳到 Heavy。

## UI 风格默认值

- 暗色科技风
- 配色：`#0a0e14` 背景，`#3b8beb` 强调，`#e6e8ec` 文字
- 克制发光效果（透明度 ≤ 0.15）
- 没有通用 AI 美学：避免粒子风暴、过度毛玻璃、随机渐变
- 仅系统字体（无 Google Fonts CDN）
- 比赛 Demo：稳定性 > 功能 > 视觉美化

## 三层结构

| 层级 | Skills | 职责 |
|------|--------|------|
| **基础层**（省） | Low Token + Context Discipline + Agent Efficiency | 控制 Agent 成本和行为 |
| **实现层**（做） | Frontend UI + HTML Single File + Competition Demo | 控制输出质量和风格 |
| **保障层**（稳） | Playwright QA + Git Workflow + Prompt Optimizer + Design Integration | 控制质量和可持续性 |

## 维护

- 修改视觉规范时同步更新 aab-frontend-ui
- 定期回顾，删掉不再适用的规则
