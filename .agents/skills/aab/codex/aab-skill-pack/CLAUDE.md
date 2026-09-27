# AAB Claude Code Rules

You are working with AAB (文刀同学)'s personal agent workflow.

## Core priorities

1. **Save tokens.** Avoid unnecessary context expansion. Read only what you need.
2. **Prefer focused edits.** Fix one thing at a time. Don't refactor unrelated code.
3. **Don't scan the whole repository** unless explicitly required.
4. **Frontend/demo tasks** → dark sci-fi, cyberpunk, neon blue-purple, modern AI platform style (see aab-frontend-ui).
5. **Competition/demo tasks** → optimize for presentation, credibility, clarity, and judge-friendly storytelling.
6. **Single-file HTML** → keep everything in one file, zero external dependencies.
7. **Validation** → minimal targeted checks before full test suites.

## Skill routing

When you encounter these situations, invoke the corresponding skill:

| Situation | Skill to use |
|-----------|-------------|
| Token/quota/context is running high | `aab-low-token` + `aab-context-discipline` |
| Need to execute quickly, skip exploration | `aab-agent-efficiency` |
| Building any UI / visual work | `aab-frontend-ui` |
| Building a single-file HTML demo | `aab-html-single-file` |
| Competition/project packaging | `aab-competition-demo` |
| Browser testing / QA check | `aab-playwright-qa` |
| Commit / backup / versioning | `aab-git-workflow` |
| Writing or compressing prompts | `aab-prompt-optimizer` |
| Design document → code | `aab-design-integration` |

## Default behavior

- Before reading more than 3 files, explain why in one sentence.
- Before modifying more than 3 files, list them briefly.
- Before running long commands, use filtered output (`| tail -50`).
- If the task can be solved with 1 file, don't read a second file.
- Read files with `limit`/`offset` — don't read 2000 lines when you need 50.
- Trust tool return values. Don't re-read files just to "confirm" edits.

## Context budget (auto-select, start from lowest)

| Level | Max files | When to use |
|-------|-----------|-------------|
| **Tiny** | 1-2 | Text/style/color fixes |
| **Normal** | 3-5 | Feature work, medium changes |
| **Heavy** | Unlimited (plan first) | User explicitly asks for full audit |

Default: start at Tiny. Escalate only when needed. Never jump straight to Heavy.

## UI style defaults

- Dark sci-fi / cyberpunk aesthetic
- Color: `#0a0e14` bg, `#3b8beb` accent, `#e6e8ec` text
- Restrained neon glow (opacity ≤ 0.15)
- No generic AI aesthetics: avoid particle storms, excessive glassmorphism, random gradients
- System fonts only (no Google Fonts CDN)
- Competition demos: stability > features > visual polish
