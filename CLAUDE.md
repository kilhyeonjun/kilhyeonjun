# GitHub Profile

> GitHub profile README for Hyeonjun Kil (Backend Engineer).
> Budget: <=50 lines. Overflow -> move to rules/.

## Core Principles

1. **Identity Consistency**: README identity must match resume (Backend Engineer, not AI Native)
2. **Fix Before Report**: Propose fixes and apply after approval
3. **Feedback Loop**: Detect -> fix -> re-verify. Max 2 iterations

## Validate

No build system. Validation = verify-readme-structure skill.

## Architecture

- Single `README.md` — GitHub profile README
- capsule-render header/footer for visual framing
- shields.io badges (`flat-square` style) for profile links and tech stack
- Markdown tables for Open Source, Certifications
- Sections: About Me, Tech Stack, Key Activities, Open Source, Certifications, Baekjoon

## Content Rules

See `.claude/rules/readme-content.md` for path-scoped constraints.

## Skills

| Skill | Purpose |
|-------|---------|
| `verify-readme-structure` | README sections, badges, links, OSS stats, date ordering |
| `verify-implementation` | Sequential all-verify skills -> unified report |
| `manage-skills` | Skill drift detection + CLAUDE.md/AGENTS.md sync |

## Gotchas

- **Career year**: Do NOT hardcode "N년차". Resume uses dynamic calculation. Use domain-focused intro
- **Identity source of truth**: Resume repo ko.json `personalInfo.title` = "Backend Engineer"
- **OSS stats**: `> **N repos . M PRs . X Merged**` must match actual PR count in tables
