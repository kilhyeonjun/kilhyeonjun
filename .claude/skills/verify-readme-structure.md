---
description: Triggers on "README 검증", "구조 검증", "verify readme", "프로필 검증", "badge check", "링크 검증", "프로필 체크". Validates GitHub profile README.md structure, badges, links, OSS statistics, and date ordering. Use whenever the user edits README.md or asks to check the profile. Self-executing.
---

# verify-readme-structure

## Do NOT Use When
- Editing non-README files (CLAUDE.md, skills) — use manage-skills instead
- Only checking skill drift — use manage-skills instead

## Procedure

Run all 7 steps sequentially on `README.md`. Report results as a table at the end.

### Step 1: Required Sections

Check that these 6 section headers exist:

```bash
cd /Users/gameduo/kilhyeonjun/kilhyeonjun
for section in "About Me" "Tech Stack" "Key Activities" "Open Source" "Certifications" "Baekjoon"; do
  grep -q "## .*${section}" README.md && echo "PASS: ${section}" || echo "FAIL: ${section}"
done
```

### Step 2: capsule-render Header/Footer

```bash
grep -c "capsule-render.vercel.app.*section=header" README.md | xargs -I{} test {} -ge 1 && echo "PASS: header" || echo "FAIL: header"
grep -c "capsule-render.vercel.app.*section=footer" README.md | xargs -I{} test {} -ge 1 && echo "PASS: footer" || echo "FAIL: footer"
```

### Step 3: Profile Badges

4 required badges: Resume, Blog, Email, LinkedIn

```bash
for badge in "Resume" "Blog" "Email\|kboxstar" "LinkedIn"; do
  grep -qE "\[${badge}.*\]" README.md && echo "PASS: ${badge}" || echo "FAIL: ${badge}"
done
```

### Step 4: Badge Style Consistency

All shields.io badges should use `flat-square`:

```bash
# Count shields.io badges without flat-square (excluding external service badges)
grep "img.shields.io" README.md | grep -v "flat-square" | grep -v "mazassumnida\|solved.ac\|spartacodingclub" | head -5
```

If any output → FAIL. No output → PASS.

**Exceptions**: External service badges (Baekjoon/solved.ac, 항해 completion badge) are exempt.

### Step 5: Open Source Statistics Accuracy

The summary line `> **N repos · M PRs · X Merged**` must match actual counts.

```bash
cd /Users/gameduo/kilhyeonjun/kilhyeonjun

# Extract claimed stats from summary line
claimed=$(grep -oE '[0-9]+ repos · [0-9]+ PRs · [0-9]+ Merged' README.md)

# Count actual PRs (including inside <details>)
actual_prs=$(grep -cE '\[#[0-9]+\]' README.md)

# Count merged
actual_merged=$(grep -c '✅ Merged' README.md)

echo "Claimed: ${claimed}"
echo "Actual PRs: ${actual_prs}, Actual Merged: ${actual_merged}"
```

Compare claimed vs actual. Mismatch → FAIL.

**Note**: `<details>` content is included in the count.

### Step 6: Markdown Table Structure

Every table's header column count must match its data row column counts:

```bash
cd /Users/gameduo/kilhyeonjun/kilhyeonjun
# Extract tables and check column consistency
awk '/^\|/{n=split($0,a,"|")-2; if(!h){h=n}else if(n!=h){print "FAIL: column mismatch line " NR ": expected " h " got " n}} /^$/{h=0}' README.md
```

No output → PASS. Any output → FAIL with line numbers.

### Step 7: Date Reverse-Chronological Order

Dates in Key Activities subsections and Certifications must be newest-first:

```bash
cd /Users/gameduo/kilhyeonjun/kilhyeonjun
# Extract dates from activities and certifications, check ordering
grep -oE '\[\d{4}\.\d{2}' README.md | tr -d '['
```

Visually verify the extracted dates are in descending order. Out of order → FAIL.

## Output Format

```markdown
## verify-readme-structure Report

| # | Check | Status | Details |
|---|-------|--------|---------|
| 1 | Required Sections | PASS/FAIL | missing: ... |
| 2 | capsule-render | PASS/FAIL | |
| 3 | Profile Badges | PASS/FAIL | missing: ... |
| 4 | Badge Style | PASS/FAIL | non-flat-square: ... |
| 5 | OSS Stats | PASS/FAIL | claimed vs actual |
| 6 | Table Structure | PASS/FAIL | mismatched lines: ... |
| 7 | Date Ordering | PASS/FAIL | out of order: ... |

**Result: N/7 PASS**
```

## Exceptions

1. External service badges (Baekjoon, 항해 completion) exempt from flat-square check
2. HTML `<img>` tags exempt from shields.io format check
3. `<details>` content included in OSS statistics count
