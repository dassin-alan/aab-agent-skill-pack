---
name: aab-skill-pack
description: AAB personal agent workflow for Codex. Use this whenever working on AAB's coding, demo, frontend, competition, single-file HTML, prompt, git, or QA tasks; it routes to the AAB skills for low token usage, context discipline, efficient execution, dark sci-fi UI, single-file HTML demos, competition-ready demos, Playwright QA, minimal Git workflow, prompt optimization, and Design.md integration.
---

# AAB Skill Pack

Use this as the routing layer for AAB's personal agent workflow in Codex.

## Default Behavior

- Save tokens: avoid unnecessary context expansion and broad repository scans.
- Prefer focused edits: fix the target issue without unrelated refactors.
- Start with the smallest useful context budget.
- If one file is enough, do not read a second file.
- Before reading or modifying more than three files, explain why briefly.
- Trust tool results and avoid re-reading just to confirm.

## Skill Routing

Use the specific AAB skill when the task matches:

| Situation | Skill |
| --- | --- |
| Token/quota/context pressure, expensive tool calls | `aab-low-token` + `aab-context-discipline` |
| Need to move quickly or stop over-exploring | `aab-agent-efficiency` |
| UI, visual design, dashboard, product page, demo page | `aab-frontend-ui` |
| Single-file HTML, no framework, offline demo, `index.html` | `aab-html-single-file` |
| Competition, project defense, roadshow, classroom demo | `aab-competition-demo` |
| Browser testing, HTML verification, demo acceptance | `aab-playwright-qa` |
| Commit, push, rollback, backup/versioning | `aab-git-workflow` |
| Prompt rewrite, prompt compression, cross-agent prompt adaptation | `aab-prompt-optimizer` |
| Design document, UI spec, Design.md, design-to-code | `aab-design-integration` |

## Context Budget

| Level | Max files | Use when |
| --- | --- | --- |
| Tiny | 1-2 | Text/style/color fixes |
| Normal | 3-5 | Feature work or medium changes |
| Heavy | Unlimited after a plan | User explicitly asks for full audit or broad refactor |

Start at Tiny by default. Escalate only when the current level is insufficient.

## UI Defaults

- Dark sci-fi / cyberpunk visual direction.
- Use restrained neon blue, purple, and cyan accents.
- Favor clean data dashboards and modern AI platform aesthetics.
- Avoid particle storms, excessive glassmorphism, random gradient cards, decorative 3D rotations, and visual effects that do not help the demo.

## Single-File HTML Defaults

- Prefer one complete `index.html`.
- Inline CSS in `<style>` and JS in `<script>`.
- Avoid CDN and external dependencies unless explicitly allowed.
- Use inline SVG, Canvas, CSS, or embedded data for visuals.
- The file should run by double-clicking and work offline.

## Competition Demo Defaults

- Prioritize demo stability over visual effects.
- Every change should improve visual impact, problem clarity, technical credibility, data credibility, product completeness, business potential, or presentation safety.
- Keep a fallback path for presentations: screenshot backup, offline version, or high-contrast mode for projectors.

## Bundled References

- `README.md`: original AAB Skill Pack overview.
- `CLAUDE.md`: Claude Code routing rules.
- `AGENTS.md`: Codex/OpenCode routing rules.
