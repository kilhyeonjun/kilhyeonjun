# GitHub Profile

> GitHub profile README for Hyeonjun Kil (Backend Engineer).
> Budget: <=70 lines in this file. Detailed validation lives in skills/rules.

## Core Principles

1. **Identity Consistency**: README identity must match resume (Backend Engineer, not AI Native)
2. **Impact First**: First screen should show backend/platform impact before activity logs or AI-usage metrics
3. **Fix Before Report**: Propose fixes and apply after approval
4. **Feedback Loop**: Detect -> fix -> re-verify. Max 2 iterations

## Validate

No build system. Validation = `verify-readme-structure` skill.

## Architecture

- Single `README.md` — GitHub profile README
- capsule-render header/footer for visual framing
- shields.io badges (`flat-square` style) for profile links, impact snapshot, and tech stack
- Markdown tables for Open Source and Certifications
- `<details>` for lower-priority or secondary material
- Sections: About Me, Impact Snapshot, Core Strengths, Featured Highlights, Tech Stack, Open Source, Activities, Certifications

## Content Rules

See `.claude/rules/readme-content.md` for path-scoped constraints.

## Skills

| Skill | Purpose |
|-------|---------|
| `verify-readme-structure` | README sections, badges, links, OSS stats, date ordering, and removed Baekjoon check |
| `verify-implementation` | Sequential all-verify skills -> unified report |
| `manage-skills` | Skill drift detection + CLAUDE.md/AGENTS.md sync |

## Gotchas

- **Career year**: Do NOT hardcode "N년차". Resume uses dynamic calculation. Use domain-focused intro
- **Identity source of truth**: Resume repo ko.json `personalInfo.title` = "Backend Engineer"
- **OSS stats**: `> **N repos · M PRs · X Merged**` must match actual PR count in the All merged PRs table
- **Baekjoon**: Do not re-add solved.ac/Baekjoon; current profile positioning is backend/platform/OSS, not algorithm-rank based
- **AI metrics**: Tokscale belongs in a collapsible secondary section, not first-screen hero content
