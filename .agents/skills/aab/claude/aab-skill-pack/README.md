# AAB Skill Pack v0.2

> 为 AAB（文刀同学）定制的 10 个 Agent Skill
>
> 适配平台：Claude Code / OpenAI Codex / Antigravity / Gemini CLI

## 安装

### Claude Code（当前已安装）

Skills 已安装在 `~/.claude/skills/` 下，系统自动识别并触发。

将 `CLAUDE.md` 复制到你的项目根目录，Claude Code 启动时会自动加载。

### Codex / OpenCode

将 `AGENTS.md` 复制到项目根目录。Skills 的 markdown 内容可以直接作为 Codex 的 skill 文件导入。

### Antigravity / Gemini CLI

Skills 目录下的每个 `SKILL.md` 包含完整指令，按对应平台的 skill 格式导入即可。

## 目录结构

```
aab-skill-pack/
├── README.md              ← 你在这里
├── CLAUDE.md              ← Claude Code 总控规则（复制到项目根目录）
├── AGENTS.md              ← Codex/OpenCode 总控规则（复制到项目根目录）
└── skills/
    ├── aab-low-token/             🔥 必装 — Token 消耗控制
    ├── aab-context-discipline/    🔥 必装 — 上下文纪律
    ├── aab-agent-efficiency/      🔥 必装 — 减少探索
    ├── aab-frontend-ui/           🔥 必装 — 暗色科技风 UI
    ├── aab-html-single-file/      🔥 必装 — 单文件 HTML 规范
    ├── aab-competition-demo/      🔥 必装 — 比赛 Demo 六步法
    ├── aab-playwright-qa/         🔥 必装 — 自动验收
    ├── aab-git-workflow/          ○ 可选 — 极简 Git
    ├── aab-prompt-optimizer/      ○ 可选 — Prompt 优化
    └── aab-design-integration/    ○ 可选 — Design.md 集成
```

## 三层结构

| 层级 | Skills | 职责 |
|------|--------|------|
| **基础层**（省） | Low Token + Context Discipline + Agent Efficiency | 控制 Agent 成本和行为 |
| **实现层**（做） | Frontend UI + HTML Single File + Competition Demo | 控制输出质量和风格 |
| **保障层**（稳） | Playwright QA + Git Workflow + Prompt Optimizer + Design Integration | 控制质量和可持续性 |

## 核心改进（v0.2）

相比 v0.1，基于 GPT 的审查意见做了以下增强：

1. **Low Token** — 增加 Hard Rules（硬性数字限制）+ 任务分级预算
2. **Context Discipline** — 增加 Tiny/Normal/Heavy 三档上下文模式
3. **Agent Efficiency** — 增加 Stop Conditions（停止探索条件）
4. **Frontend UI** — 增加 Avoid Generic AI UI（避免廉价 AI 感）
5. **Competition Demo** — 增加 Competition Scoring Lens（比赛评分导向）
6. **Playwright QA** — 重构为 Quick/Demo/Competition 三档 QA
7. **HTML Single File** — 增加稳定性优先排序
8. **CLAUDE.md + AGENTS.md** — 新增总控路由文件

## 测试建议

优先在实际项目中测试这三个（最常用）：

1. `aab-low-token` — 任意日常开发任务
2. `aab-frontend-ui` — 任何需要 UI 的场景
3. `aab-html-single-file` — 比赛 Demo / 工具页面

## 维护

- 每个 Skill 控制在 150-300 行
- 正文中文，YAML description 中英双语触发关键词
- 修改视觉规范时同步更新 aab-frontend-ui
- 每年 6 月和 12 月回顾一次，删掉不再适用的规则
