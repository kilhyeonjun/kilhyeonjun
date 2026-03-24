---
description: Triggers on "전체 검증", "통합 검증", "verify all", "verify implementation", "프로필 검증 전체". Orchestrates all verify-* skills sequentially with feedback loop. Use when the user wants a comprehensive check of the entire profile, not just one aspect. Self-executing.
---

# verify-implementation

## Do NOT Use When
- Single specific check needed — use the individual verify skill directly
- Skill management — use manage-skills instead

## Execution Target Skills

| # | Skill | Description |
|---|-------|-------------|
| 1 | `verify-readme-structure` | README sections, badges, links, OSS stats, date ordering |

## Procedure

### Step 1: Run All Verify Skills

Execute each skill in the table above sequentially. Collect all issues with:
- Check name
- Status (PASS/FAIL)
- Details (what's wrong, where)
- Fix suggestion

### Step 2: Unified Report

```markdown
## Verification Report

### Summary
| Skill | PASS | FAIL | Total |
|-------|------|------|-------|
| verify-readme-structure | N | M | 7 |
| **Total** | N | M | 7 |

### Issues Found
| # | Skill | Check | Issue | Fix Suggestion |
|---|-------|-------|-------|----------------|
| 1 | ... | ... | ... | ... |
```

### Step 3: Fix Pass (if issues found)

Present options to user:
1. **Fix all** — apply all suggested fixes
2. **Fix individually** — choose which to fix
3. **Skip** — report only, no changes

### Step 4: Re-verify (if fixes applied)

Re-run only the skills that had FAILs. Max 2 iterations.

If still failing after 2 fix cycles → report as manual action item. Do NOT loop further.

### Step 5: Final Status

```markdown
### Final Result: ALL PASS / N issues remaining
```
