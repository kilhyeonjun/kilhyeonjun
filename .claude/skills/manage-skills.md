---
description: Triggers on "스킬 관리", "스킬 업데이트", "CLAUDE.md 동기화", "skill drift", "skill sync", "하네스 관리". Detects drift between skill files and CLAUDE.md catalog, then auto-syncs. Use when adding, removing, or modifying skills, or when CLAUDE.md might be out of date. Self-executing.
---

# manage-skills

## Do NOT Use When
- README content editing — use verify-readme-structure instead
- Running verification checks — use verify-implementation instead

## Procedure

### Step 1: Collect Current Skill Files

```bash
ls -1 /Users/gameduo/kilhyeonjun/kilhyeonjun/.claude/skills/*.md 2>/dev/null
```

For each file, extract the `description` from YAML frontmatter.

### Step 2: Extract CLAUDE.md Skill Table

Read `CLAUDE.md` → find `## Skills` section → parse the markdown table rows.

### Step 3: Drift Detection

Compare skill files vs CLAUDE.md table:

| Drift Type | Condition |
|------------|-----------|
| **Missing from CLAUDE.md** | Skill file exists but no table row |
| **Orphan in CLAUDE.md** | Table row exists but no skill file |
| **Description mismatch** | File description doesn't match table purpose |

### Step 4: Apply Synchronization

For each drift detected:
- **Missing from CLAUDE.md** → add row to Skills table
- **Orphan in CLAUDE.md** → remove row from Skills table
- **Description mismatch** → update table purpose to match file

### Step 5: Report

```markdown
## Skill Sync Report

| Skill | Status | Action Taken |
|-------|--------|--------------|
| verify-readme-structure | IN_SYNC / ADDED / UPDATED / REMOVED | ... |
| verify-implementation | IN_SYNC / ADDED / UPDATED / REMOVED | ... |
| manage-skills | IN_SYNC / ADDED / UPDATED / REMOVED | ... |

**Drift detected: N items → N fixed**
```

## Registered Skills

This is the canonical list. CLAUDE.md must mirror it.

| Skill | Description | Covered Files |
|-------|-------------|---------------|
| `verify-readme-structure` | README sections, badges, links, OSS stats, date ordering | `README.md` |
| `verify-implementation` | Sequential all-verify skills → unified report | (orchestrator) |
| `manage-skills` | Skill drift detection + CLAUDE.md sync | `.claude/skills/*.md`, `CLAUDE.md` |

## Exceptions

1. Lock files, generated files — no skill coverage needed
2. `.git/` directory — not tracked by skills
