# AAB Agent Rules

You are working on AAB (文刀同学)'s coding and demo projects.

## Primary goals

1. Save tokens — every tool call costs.
2. Avoid unnecessary repository scanning.
3. Make focused, minimal edits.
4. Preserve existing functionality.
5. Improve demo quality and presentation value.

## Default constraints

- Do NOT read the whole repository.
- Do NOT modify unrelated files.
- Do NOT run long commands without output filtering (`| tail -50`).
- Do NOT add dependencies unless explicitly allowed.
- Do NOT do broad refactors unless explicitly requested.
- If one file is enough, only use one file.
- If more context is needed, explain what file and why.
- Read at most 3 files before making the first edit.

## Context budget (apply automatically)

| Level | Max files | Trigger |
|-------|-----------|---------|
| Tiny | 1-2 | Simple text/style/color change |
| Normal | 3-5 | Adding a feature or component |
| Heavy | Unlimited (plan first) | User says "full audit" or "refactor everything" |

Always start at Tiny. Escalate only when the current level is insufficient.

## Frontend style preference

- Dark sci-fi / cyberpunk
- Neon blue/purple/cyan accents
- Clean data dashboards
- Modern AI platform aesthetic
- Competition-ready visual hierarchy

**Avoid generic AI UI:**
- NO particle storms or starfield backgrounds
- NO excessive glassmorphism
- NO random gradient cards
- NO purely decorative 3D rotations
- Only use visual effects you can justify to a judge

## For single-file HTML demos

- Prefer one complete `index.html`.
- Inline CSS in `<style>`, JS in `<script>`.
- Avoid CDN unless explicitly allowed.
- Use inline SVG/Canvas/CSS for visuals.
- The file MUST run by double-clicking.
- Must work offline — all data embedded.

## For competition projects

- Prioritize: demo stability > presentation clarity > visual effects.
- Every change should improve at least one of: visual impact, problem clarity, technical credibility, data credibility, product completeness, business potential, presentation safety.
- Always have a fallback: screenshot backup, offline version, high-contrast mode for projectors.

## Stop conditions

Stop exploring when:
- The target file/function/component is found.
- One reliable implementation path is clear.
- The user's request can be completed without more context.
- You're about to repeat a search you already did.

Do NOT continue searching just to be exhaustive.
