---
name: verify-readme-structure
description: GitHub 프로필 README.md의 구조, 링크 형식, 테이블 정합성, 날짜 정렬을 검증합니다. README 수정 후 사용.
---

# README 구조 검증

## Purpose

GitHub 프로필 README.md의 품질과 일관성을 검증합니다:

1. **필수 섹션 존재** — 프로필에 반드시 포함되어야 하는 섹션이 모두 있는지
2. **링크/뱃지 형식 일관성** — shields.io 뱃지와 외부 링크의 URL 형식이 올바른지
3. **Open Source 통계 정합성** — 요약 통계와 실제 PR 목록이 일치하는지
4. **날짜 역시간순 정렬** — 활동, 스터디, 자격증이 최신순으로 정렬되어 있는지
5. **Markdown 테이블 구조** — 테이블 헤더와 행의 컬럼 수가 일치하는지

## When to Run

- README.md를 수정한 후
- 새로운 Open Source PR을 추가한 후
- 활동, 자격증 등 날짜가 포함된 항목을 추가/수정한 후
- 뱃지나 링크를 추가/변경한 후

## Related Files

| File | Purpose |
|------|---------|
| `README.md` | GitHub 프로필 README (검증 대상) |

## Workflow

### Step 1: 필수 섹션 존재 확인

**파일:** `README.md`

**검사:** 다음 필수 섹션 헤더가 모두 존재하는지 확인합니다.

필수 섹션 목록:
- `## 👋 About Me`
- `## 🛠️ Tech Stack`
- `## 📅 Key Activities`
- `## 🌍 Open Source Contributions`
- `## 📜 Certifications`
- `## 🏆 Baekjoon Solved Rank`

```bash
for section in "## 👋 About Me" "## 🛠️ Tech Stack" "## 📅 Key Activities" "## 🌍 Open Source Contributions" "## 📜 Certifications" "## 🏆 Baekjoon Solved Rank"; do
  grep -c "$section" README.md > /dev/null 2>&1 || echo "MISSING: $section"
done
```

**PASS:** 모든 필수 섹션이 존재함.
**FAIL:** 하나 이상의 필수 섹션이 누락됨. 누락된 섹션을 추가합니다.

### Step 2: capsule-render header/footer 확인

**파일:** `README.md`

**검사:** capsule-render header(section=header)와 footer(section=footer)가 모두 존재하는지 확인합니다.

```bash
grep -c "capsule-render.vercel.app.*section=header" README.md
grep -c "capsule-render.vercel.app.*section=footer" README.md
```

**PASS:** header와 footer 모두 존재 (각각 1 이상).
**FAIL:** header 또는 footer가 누락됨.

### Step 3: 상단 프로필 뱃지 확인

**파일:** `README.md`

**검사:** 상단에 Resume, Blog, Email, LinkedIn 뱃지 4개가 모두 존재하는지 확인합니다.

```bash
for badge in "Resume" "Blog" "Email\|gmail" "LinkedIn"; do
  grep -ci "$badge.*img.shields.io/badge" README.md > /dev/null 2>&1 || echo "MISSING BADGE: $badge"
done
```

**PASS:** 4개 프로필 뱃지 모두 존재.
**FAIL:** 누락된 뱃지가 있음.

### Step 4: shields.io 뱃지 URL 형식 일관성

**파일:** `README.md`

**검사:** 모든 shields.io 뱃지가 `style=flat-square` 스타일을 사용하는지 확인합니다.

Grep을 사용하여 `img.shields.io/badge` 패턴을 찾고, `flat-square`가 아닌 스타일을 사용하는 뱃지를 탐지합니다.

```bash
grep "img.shields.io/badge" README.md | grep -v "flat-square"
```

**PASS:** 출력 없음 (모든 뱃지가 flat-square 스타일).
**FAIL:** flat-square가 아닌 스타일을 사용하는 뱃지가 있음. `style=flat-square`로 통일합니다.

### Step 5: Open Source 통계 정합성

**파일:** `README.md`

**검사:** 요약 줄(`> **N repos · M PRs · X Merged**`)의 숫자가 실제 PR 목록과 일치하는지 확인합니다.

1. 요약 줄에서 repos, PRs, Merged 숫자를 추출합니다.
2. README 내 모든 PR 링크(`github.com/.../pull/`)의 개수를 셉니다.
3. `✅ Merged` 상태의 PR 개수를 셉니다.
4. 고유한 repository 개수를 셉니다.

```bash
# 요약 줄 추출
grep -o '[0-9]* repos · [0-9]* PRs · [0-9]* Merged' README.md

# 실제 PR 수 카운트
grep -c "github.com/.*/pull/" README.md

# Merged 수 카운트
grep -c "✅ Merged" README.md
```

**PASS:** 요약 숫자와 실제 카운트가 일치.
**FAIL:** 숫자 불일치. 요약 줄을 실제 카운트에 맞게 업데이트합니다.

### Step 6: Markdown 테이블 구조 검증

**파일:** `README.md`

**검사:** 모든 Markdown 테이블의 헤더 컬럼 수와 각 행의 컬럼 수가 일치하는지 확인합니다.

README.md를 읽고 각 테이블을 파싱하여:
1. 헤더 행의 `|` 구분자 수를 셈
2. 구분선 행 (`|---|`) 존재 확인
3. 데이터 행의 `|` 구분자 수가 헤더와 동일한지 확인

**PASS:** 모든 테이블의 컬럼 수가 일관됨.
**FAIL:** 컬럼 수 불일치 테이블 존재. 해당 행의 컬럼을 맞춥니다.

### Step 7: 날짜 역시간순 정렬 확인

**파일:** `README.md`

**검사:** 날짜가 포함된 목록 항목이 역시간순(최신 → 과거)으로 정렬되어 있는지 확인합니다.

확인 대상:
- **Key Activities** 내 각 하위 섹션 (발표, 스터디, 교육)
- **Certifications** 테이블

README.md를 읽고 각 섹션에서 `[YYYY.MM]` 패턴의 날짜를 순서대로 추출하여, 내림차순인지 확인합니다.

**PASS:** 모든 섹션에서 날짜가 역시간순.
**FAIL:** 정렬이 깨진 항목 존재. 올바른 위치로 이동합니다.

## Output Format

```markdown
## README 구조 검증 결과

| # | 검사 | 상태 | 상세 |
|---|------|------|------|
| 1 | 필수 섹션 | PASS/FAIL | ... |
| 2 | capsule-render | PASS/FAIL | ... |
| 3 | 프로필 뱃지 | PASS/FAIL | ... |
| 4 | 뱃지 스타일 | PASS/FAIL | ... |
| 5 | OSS 통계 정합성 | PASS/FAIL | ... |
| 6 | 테이블 구조 | PASS/FAIL | ... |
| 7 | 날짜 정렬 | PASS/FAIL | ... |
```

## Exceptions

다음은 **위반이 아닙니다**:

1. **외부 서비스 뱃지** — Baekjoon(mazassumnida), 항해 플러스 수료 뱃지 등 shields.io가 아닌 외부 서비스 뱃지는 `flat-square` 스타일 검사에서 제외
2. **HTML 태그 내 이미지** — `<img>` 태그로 삽입된 이미지(YouTube 썸네일, 수료 뱃지 등)는 shields.io 뱃지 형식 검사에서 제외
3. **collapsible 섹션** — `<details>` 태그 내부의 테이블도 Open Source 통계 카운트에 포함해야 함
