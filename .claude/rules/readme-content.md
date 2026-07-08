---
globs: ["README.md"]
---

# README Content Rules

When editing README.md:

1. **Identity = Backend Engineer** — header desc and About Me must lead with backend/platform, not AI usage
2. **Impact first** — first screen should expose measurable impact: 270x scaling, 9 merged OSS PRs, 0→1 AI dev infra
3. **About Me ordering** — backend-core domains first, AI development infrastructure last
4. **No hardcoded career year** — "N년차" drifts every year. Use domain-focused intro instead
5. **shields.io badges use `style=flat-square`** — consistent across all badges
6. **OSS summary stats must match actual PR count** — repos/PRs/Merged in summary line = counted from the All merged PRs table rows
7. **Date ordering is reverse-chronological** — newest first in Activities and Certifications
8. **All external links must be valid or intentionally bot-blocked** — LinkedIn may return anti-bot responses; other links should pass
9. **Markdown table column counts must be consistent** — header columns = data row columns
10. **Identity source of truth** — resume repo `src/content/resume/ko.json` `personalInfo.title`
11. **No Baekjoon/solved.ac** — algorithm rank is no longer part of the intended positioning
12. **AI activity metrics are secondary** — Tokscale is allowed only in a collapsible section below primary career evidence
