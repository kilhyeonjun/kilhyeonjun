---
description: Triggers on "README 검증", "구조 검증", "verify readme", "프로필 검증", "badge check", "링크 검증", "프로필 체크". Validates GitHub profile README.md structure, badges, links, OSS statistics, no-Baekjoon positioning, and date ordering. Use whenever the user edits README.md or asks to check the profile. Self-executing.
---

# verify-readme-structure

## Do NOT Use When
- Editing non-README files (CLAUDE.md, skills) — use manage-skills instead
- Only checking skill drift — use manage-skills instead

## Procedure

Run all 9 steps sequentially on `README.md`. Report results as a table at the end.

### Step 1: Required Sections

Check that these 8 section headers exist:

```bash
cd /path/to/kilhyeonjun
for section in "About Me" "Impact Snapshot" "Core Strengths" "Featured Highlights" "Tech Stack" "Open Source" "Activities" "Certifications"; do
  grep -q "## .*${section}" README.md && echo "PASS: ${section}" || echo "FAIL: ${section}"
done
```

### Step 2: No Baekjoon / solved.ac

```bash
if grep -Eiq 'baekjoon|solved\.ac|mazassumnida|boj=' README.md; then
  echo "FAIL: Baekjoon/solved.ac content remains"
else
  echo "PASS: no Baekjoon/solved.ac"
fi
```

### Step 3: capsule-render Header/Footer

```bash
grep -c "capsule-render.vercel.app.*section=header" README.md | xargs -I{} test {} -ge 1 && echo "PASS: header" || echo "FAIL: header"
grep -c "capsule-render.vercel.app.*section=footer" README.md | xargs -I{} test {} -ge 1 && echo "PASS: footer" || echo "FAIL: footer"
```

### Step 4: Profile Badges

4 required badges: Resume, Blog, Email, LinkedIn

```bash
for badge in "Resume" "Blog" "Email\|kboxstar" "LinkedIn"; do
  grep -qE "\[${badge}.*\]" README.md && echo "PASS: ${badge}" || echo "FAIL: ${badge}"
done
```

### Step 5: Badge Style Consistency

All shields.io badges should use `flat-square`:

```bash
grep "img.shields.io" README.md | grep -v "flat-square" | head -5
```

If any output → FAIL. No output → PASS.

### Step 6: Open Source Statistics Accuracy

The summary line `> **N repos · M PRs · X Merged**` must match actual counts in the All merged PRs table.

```bash
claimed=$(grep -oE '[0-9]+ repos · [0-9]+ PRs · [0-9]+ Merged' README.md)
actual_prs=$(awk '/All merged PRs/{flag=1} flag && /\[#[0-9]+\]/{count++} /<\/details>/{if(flag){print count; exit}}' README.md)
actual_merged=$(awk '/All merged PRs/{flag=1} flag && /✅ Merged/{count++} /<\/details>/{if(flag){print count; exit}}' README.md)
echo "Claimed: ${claimed}"
echo "Actual PRs: ${actual_prs}, Actual Merged: ${actual_merged}"
```

Compare claimed vs actual. Mismatch → FAIL.

### Step 7: Markdown Table Structure

Every table's header column count must match its data row column counts:

```bash
python3 - <<'PY'
from pathlib import Path
for i,line in enumerate(Path('README.md').read_text().splitlines(),1):
    if line.startswith('|') and line.endswith('|'):
        cols=line.count('|')-1
        print(i, cols, line[:80])
PY
```

Visually verify each table block keeps a stable column count.

### Step 8: Date Reverse-Chronological Order

Dates in Activities and Certifications must be newest-first:

```bash
grep -oE '\[\d{4}\.\d{2}|\| [0-9]{4}\.[0-9]{2} ' README.md
```

Visually verify extracted dates are in descending order within each section. Out of order → FAIL.

### Step 9: Link Check

```bash
python3 - <<'PY'
import re, urllib.request, urllib.error
from pathlib import Path
urls=sorted(set(re.findall(r'https?://[^)\s">]+', Path('README.md').read_text())))
for u in urls:
    try:
        req=urllib.request.Request(u, method='HEAD', headers={'User-Agent':'HermesReadmeVerifier/1.0'})
        with urllib.request.urlopen(req, timeout=8) as r:
            print('PASS', r.status, u)
    except urllib.error.HTTPError as e:
        if 'linkedin.com' in u and e.code in (999, 403, 429):
            print('WARN', e.code, u, '(bot-block expected)')
        else:
            print('FAIL', e.code, u)
    except Exception as e:
        print('FAIL', type(e).__name__, u)
PY
```

## Output Format

```markdown
## verify-readme-structure Report

| # | Check | Status | Details |
|---|-------|--------|---------|
| 1 | Required Sections | PASS/FAIL | missing: ... |
| 2 | No Baekjoon | PASS/FAIL | |
| 3 | capsule-render | PASS/FAIL | |
| 4 | Profile Badges | PASS/FAIL | missing: ... |
| 5 | Badge Style | PASS/FAIL | non-flat-square: ... |
| 6 | OSS Stats | PASS/FAIL | claimed vs actual |
| 7 | Table Structure | PASS/FAIL | mismatched lines: ... |
| 8 | Date Ordering | PASS/FAIL | out of order: ... |
| 9 | Link Check | PASS/WARN/FAIL | LinkedIn bot-block may warn |

**Result: N/9 PASS**
```

## Exceptions

1. LinkedIn may return bot-block status to automated checks; keep as WARN if public browser opens it.
2. HTML `<img>` tags exempt from shields.io format check.
3. Tokscale is allowed only inside a collapsible secondary section.
