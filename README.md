# Hyeonjun Kil

**Backend Engineer · Platform Part Leader**

6개 라이브 게임의 공통 백엔드를 설계·운영합니다. DB 병목·동시성·공통 패키지를 다루며, BE·FE·AI 3인 파트의 설계·검증 기준을 이끕니다.

<div align="center">

  [![Resume](https://img.shields.io/badge/Resume-30A9DE?style=flat-square&logo=Google%20Docs&logoColor=white)](https://career.kilpenguin.com/)
  [![Blog](https://img.shields.io/badge/Blog-DD0B78?style=flat-square&logo=Astro&logoColor=white)](https://blog.kilpenguin.com/)
  [![Email](https://img.shields.io/badge/kboxstar@gmail.com-EA4335?style=flat-square&logo=Gmail&logoColor=white)](mailto:kboxstar@gmail.com)
  [![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=LinkedIn&logoColor=white)](https://linkedin.com/in/kilhyeonjun)

  ![Open Source](https://img.shields.io/badge/Open%20Source-9%20Merged%20PRs-2DA44E?style=flat-square)
  ![AI Dev Infra](https://img.shields.io/badge/AI%20Dev%20Infra-0--to--1%20Platform-8B5CF6?style=flat-square)

</div>

## 👋 About Me

직접 설계·구현하는 백엔드 엔지니어입니다. 공통 패키지와 완료 기준을 팀에 적용하고, AI 도구 산출물은 테스트·리뷰로 검증합니다. 아래 실무 사례에는 선택 이유와 측정 조건을, 공개 프로젝트에는 직접 확인할 수 있는 코드·테스트를 연결했습니다.

## Impact Snapshot

- **운영 DB 병목:** 백필 처리량 **9.3→247건/분** — [원인 분석과 쿼리 변경](https://career.kilpenguin.com/portfolio/rds-saturation-rca/).
- **채팅 서버 설계:** **6K msg/s 부하 시험에서 ACK p95 767.6→6.6ms** — [채널 샤딩과 원자성 경계](https://career.kilpenguin.com/portfolio/realtime-game-chat/). dev/sandbox 시험이며 라이브 트래픽 수치가 아닙니다.
- **공통 플랫폼:** **7개 프로젝트 업그레이드 반영 약 3시간→15분** — [패키지·CI 설계와 이관 회귀](https://career.kilpenguin.com/portfolio/shared-package-ci-platform/).

## Core Strengths

- **Backend Architecture** — DB 최적화, 동시성 제어, 이벤트 기반 아키텍처
- **Game / Cloud Infrastructure** — 게임 서버, AWS 인프라, 운영 자동화
- **Engineering Quality** — 테스트, 코드 리뷰, GitHub Actions, 반복 가능한 개발 프로세스
- **AI Development Infrastructure** — Claude Code, Codex, Amazon Q, RAG, MCP, Git Hooks 기반 컨텍스트/품질 관리

## Featured Highlights

### 🎤 Games on AWS 2025

**Amazon Q Developer를 활용한 개발 생산성 향상** 발표<br>
개발자 1인이 10일 만에 **시간당 병렬 처리 Job 수 기준** 데이터 파이프라인 용량을 **270배 확장**한 사례를 공유했습니다.

[📺 발표 영상](https://www.youtube.com/watch?v=2jRicD15jXk) · [발표 후기](https://www.linkedin.com/posts/kilhyeonjun_%EC%A0%9C-%EC%83%9D%EC%95%A0-%EC%B2%AB-%EB%8C%80%EC%99%B8-%EC%BB%A8%ED%8D%BC%EB%9F%B0%EC%8A%A4-%EB%B0%9C%ED%91%9C%EB%A5%BC-%EC%84%B1%EA%B3%B5%EC%A0%81%EC%9C%BC%EB%A1%9C-%EB%A7%88%EC%B3%A4%EC%8A%B5%EB%8B%88%EB%8B%A4-%EC%A7%80%EB%82%9C-10%EC%9B%94-activity-7383826538632249344--0Yz)

<a href="https://www.youtube.com/watch?v=2jRicD15jXk">
  <img src="https://img.youtube.com/vi/2jRicD15jXk/maxresdefault.jpg" alt="Games on AWS 2025" width="520" />
</a>

### 공개 코드로 확인할 수 있는 작업

| 프로젝트 | 확인할 설계·검증 | 근거 |
|---|---|---|
| [Harness Launcher](https://github.com/kilhyeonjun/harness-launcher) | 프로젝트 경계별 런타임 격리, 영속 접수·목적지별 FIFO, 중복 접수·대기 timeout 처리 | [사례와 검증 범위](https://career.kilpenguin.com/portfolio/ai-coding-harness/) |
| [대신물류 배차 원장](https://github.com/kilhyeonjun/daesin-logistics-bot-be) | ARM64 배포·복구, singleton 수집, 실제 변경 행과 API 일치 관측 | [운영 사례와 한계](https://career.kilpenguin.com/portfolio/daesin-logistics-bot/) |
| [콘서트 예약](https://github.com/hhpb-code/hhplus-concert) | 좌석·지갑 경합 범위, 낙관적 락·사용자 단위 분산 락, 공개 부하 보고서 | [코드·테스트 연결](https://career.kilpenguin.com/portfolio/concert-reservation/) |

Harness Launcher는 개인 공개 프로젝트입니다. 회사의 팀 공유 컨텍스트·내부 데이터·운영 인덱스는 별도 범위이며, 이 저장소의 공개 근거에 포함하지 않습니다. 대신물류의 운영 기록은 운영자가 기록한 단일 배포 관측으로, 독립 검증이나 가동률·최신성 SLA가 아닙니다.

### 🌍 Open Source Fixes

CLI 안정성, provider 호환성, 인증/토큰 갱신, Jira Cloud API 마이그레이션 등 실제 사용 중 마주친 문제를 고쳐 upstream에 반영했습니다.

> **7 repos · 9 PRs · 9 Merged**

## 🛠️ Tech Stack

<div align="center">

**Backend**<br>
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=TypeScript&logoColor=white)
![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=NestJS&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=Node.js&logoColor=white)

**Infra / Data**<br>
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=Amazon%20AWS&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=Docker&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=MySQL&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=Redis&logoColor=white)

**Quality / Automation**<br>
![Jest](https://img.shields.io/badge/Jest-C21325?style=flat-square&logo=Jest&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=GitHub%20Actions&logoColor=white)
![Git Hooks](https://img.shields.io/badge/Git%20Hooks-181717?style=flat-square&logo=Git&logoColor=white)

**AI Dev Infra**<br>
![Claude Code](https://img.shields.io/badge/Claude%20Code-D97757?style=flat-square)
![Codex](https://img.shields.io/badge/Codex-111827?style=flat-square)
![Amazon Q](https://img.shields.io/badge/Amazon%20Q-FF9900?style=flat-square&logo=Amazon%20AWS&logoColor=white)
![RAG](https://img.shields.io/badge/RAG-8B5CF6?style=flat-square)
![MCP](https://img.shields.io/badge/MCP-6366F1?style=flat-square)

</div>

## 🌍 Open Source Contributions

### Featured PRs

| Project | PR | Impact |
|---------|----|--------|
| [opencode](https://github.com/anomalyco/opencode) ⭐131k | [#15136](https://github.com/anomalyco/opencode/pull/15136) | macOS sidecar spawn hang 방지 |
| [CodexBar](https://github.com/steipete/CodexBar) | [#288](https://github.com/steipete/CodexBar/pull/288) | Kiro CLI 1.24+ Q Developer format 지원 |
| [kiro-gateway](https://github.com/jwadow/kiro-gateway) | [#22](https://github.com/jwadow/kiro-gateway/pull/22), [#23](https://github.com/jwadow/kiro-gateway/pull/23) | AWS SSO credential reload, toolResults 변환 안정화 |
| [atlassian-skills](https://github.com/langpingxue/atlassian-skills) | [#6](https://github.com/langpingxue/atlassian-skills/pull/6), [#7](https://github.com/langpingxue/atlassian-skills/pull/7) | Jira Cloud Search API / ADF comment API v3 대응 |

<details>
<summary><b>All merged PRs</b></summary>

| Project | PR | Description | Status |
|---------|----|-------------|--------|
| [opencode](https://github.com/anomalyco/opencode) | [#15136](https://github.com/anomalyco/opencode/pull/15136) | fix(desktop): remove interactive shell flag from sidecar spawn to prevent hang on macOS | ✅ Merged |
| [oh-my-openagent](https://github.com/code-yeongyu/oh-my-openagent) | [#2664](https://github.com/code-yeongyu/oh-my-openagent/pull/2664) | fix(shared): respect cached model context limits for Anthropic providers post-GA | ✅ Merged |
| [CodexBar](https://github.com/steipete/CodexBar) | [#288](https://github.com/steipete/CodexBar/pull/288) | fix(kiro): support kiro-cli 1.24+ Q Developer format | ✅ Merged |
| [kiro-gateway](https://github.com/jwadow/kiro-gateway) | [#23](https://github.com/jwadow/kiro-gateway/pull/23) | fix(converters): skip thinking tag injection when toolResults present | ✅ Merged |
| [kiro-gateway](https://github.com/jwadow/kiro-gateway) | [#22](https://github.com/jwadow/kiro-gateway/pull/22) | fix(auth): reload SQLite credentials before AWS SSO OIDC token refresh | ✅ Merged |
| [atlassian-skills](https://github.com/langpingxue/atlassian-skills) | [#7](https://github.com/langpingxue/atlassian-skills/pull/7) | fix: use ADF format for comments in Jira Cloud API v3 | ✅ Merged |
| [atlassian-skills](https://github.com/langpingxue/atlassian-skills) | [#6](https://github.com/langpingxue/atlassian-skills/pull/6) | fix: migrate to new Jira Cloud search API endpoint | ✅ Merged |
| [SuperClaude_Plugin](https://github.com/SuperClaude-Org/SuperClaude_Plugin) | [#18](https://github.com/SuperClaude-Org/SuperClaude_Plugin/pull/18) | fix: correct marketplace name in documentation | ✅ Merged |
| [cyan](https://github.com/coralblack/cyan) | [#110](https://github.com/coralblack/cyan/pull/110) | feat: add NOT IN operator to FindOperatorComp | ✅ Merged |

</details>

## 📅 Activities

- **[2026.04 ~ 진행중] AI 코딩 하네스 프레임워크** — 팀 공유 AI 개발 인프라, RAG/MCP/Git Hooks 기반 컨텍스트·품질 관리
- **[2026.01 ~ 진행중] 시스템 디자인 스터디 2권** — [리포지토리](https://github.com/seungwontech/system-design-study2)
- **[2025.10] Games on AWS 2025 컨퍼런스 발표** — 시간당 병렬 처리 Job 수 기준 파이프라인 용량 270배 확장 사례
- **[2025.10 ~ 2025.12] Node.js 디자인 패턴 바이블 스터디** — [리포지토리](https://github.com/TSBM-Studio/nodejs-design-pattern-study)
- **[2025.08 ~ 2025.10] 시스템 디자인 스터디 1권** — [리포지토리](https://github.com/jyjae/system-design-study)
- **[2024.09 ~ 2024.11] 항해 플러스 백엔드 6기** — TDD, Clean Architecture, 대용량 트래픽 처리 — [프로젝트](https://github.com/hhpb-code)
- **[2024.03] AWS SES 이벤트 로깅 기술 세미나** — [세미나 내용 보기](https://jnp.tech/posts/2024-03-aws-ses-event-log)

## 📜 Certifications

| Date | Certification | Issuer |
|------|---------------|--------|
| 2025.12 | SQLD (Structured Query Language Developer) | 한국데이터산업진흥원 |
| 2023.06 | 정보처리기사 | 한국산업인력공단 |

<details>
<summary><b>AI coding activity</b></summary>

[![Tokscale Stats](https://tokscale.ai/api/embed/kilhyeonjun/svg?template=minimal&color=blue&graph=1)](https://tokscale.ai/u/kilhyeonjun)

</details>

![footer](https://capsule-render.vercel.app/api?type=waving&color=30A9DE&height=120&section=footer)
