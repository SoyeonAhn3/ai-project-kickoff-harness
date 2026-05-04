🌐 [한국어](./README_ko.md) | [English](./README.md)

# AI Project Kickoff Harness

> 막연한 프로젝트 아이디어를 AI 인터뷰와 검증을 통해 개발 가능한 계획으로 전환하는 CLI 자동화 하네스

## 개요

많은 프로젝트가 실패하는 이유는 코드가 아니라, 개발 전에 요구사항이 명확하지 않기 때문이다. 이 하네스는 구조화된 인터뷰를 진행하고, 누락과 모순을 찾아내고, 포괄적인 킥오프 문서를 생성한다 — 코드 한 줄 쓰기 전에.

이 하네스는 자기 자신을 사용해서(dogfooding) 개발되었다: 2회의 반복을 통해 7건의 설계 개선을 발견하고 즉시 반영했다.

## 목차

- [동작 흐름](#동작-흐름)
- [기술 스택](#기술-스택)
- [빠른 시작](#빠른-시작)
- [프로젝트 구조](#프로젝트-구조)
- [개발 방법론](#개발-방법론)
- [문서](#문서)
- [현재 상태](#현재-상태)
- [로드맵](#로드맵)

## 동작 흐름

```
사용자 아이디어 (자유 텍스트)
  → 프로젝트 유형 판별
  → 기획 인터뷰 (무엇을 만들 것인가)
  → 설계 인터뷰 (어떻게 만들 것인가 — 패스 가능)
  → AI 아이디어 제안 (최대 5개, 난이도+시간 포함)
  → project_kickoff.md 생성 (프로필 + 아키텍처 + 데이터 구조)
  → 누락/모순 점검 (개발 전에 문제 발견)
  → 개발 착수 체크리스트 생성
  → 기본 스킬 세팅 (GitHub에서 7개 스킬 가져오기)
```

## 기술 스택

| 기술 | 역할 | 선택 이유 |
|---|---|---|
| Claude Code Skill | 하네스 엔진 (오케스트레이터) | Claude CLI와 네이티브 통합, 스킬 체이닝 |
| Markdown | 산출물 포맷 | 사람이 읽기 쉽고, 버전 관리 가능, 범용적 |
| Git / GitHub | 스킬 배포, 프로젝트 공유 | 오픈소스 협업 표준 |
| gh CLI | Skill_package에서 스킬 가져오기 | 전체 clone 없이 특정 폴더만 선택 복사 가능 |

## 빠른 시작

### 사전 요구사항

- Claude Code CLI 설치
- gh CLI 설치 및 인증
- Git 초기화 완료

### 사용법

각 스킬을 순서대로 실행:

```
/kickoff-start          # 아이디어 입력 + 프로젝트 유형 판별
/kickoff-interview      # 기획 & 설계 인터뷰
/kickoff-suggest        # AI 추가 아이디어 제안
/kickoff-profile        # project_kickoff.md 생성
/kickoff-gap            # 누락/모순 점검
/kickoff-checklist      # 개발 착수 체크리스트 생성
/kickoff-skills         # GitHub에서 기본 스킬 가져오기
```

### 산출물

```
pre-requirement/project_kickoff.md    # 단일 기준 문서
.claude/skills/*                      # 기본 개발 스킬 7개
```

## 프로젝트 구조

```
AI-Project-Kickoff-Harness/
├── .claude/skills/          # 개발 스킬 (기본 7개 + kickoff 스킬)
│   ├── dev-log/             # 에러/변경 기록 (JSONL)
│   ├── gen-manual/          # 매뉴얼 생성
│   ├── github-push/         # 커밋 & 푸시 자동화
│   ├── phase-doc/           # Phase 문서 관리
│   ├── readme-gen/          # README 생성
│   ├── skill-template/      # 스킬 생성 템플릿
│   └── test-scenario/       # 테스트 시나리오 생성
├── Phase/                   # Phase별 개발 문서
│   ├── Phase1_kickoff-start.md
│   ├── Phase2_kickoff-interview.md
│   ├── Phase3_kickoff-suggest.md
│   ├── Phase4_kickoff-profile.md
│   ├── Phase5_kickoff-gap.md
│   ├── Phase6_checklist-skills.md
│   └── Phase7_integration-test.md
└── pre-requirement/         # 기획 & dogfooding 산출물
    ├── Plan.txt             # 마스터 플랜 (dogfooding으로 갱신됨)
    ├── project_profile.md   # Dogfooding 1회차 산출물
    ├── gap_report.md        # Dogfooding 1회차 산출물
    ├── dev_checklist.md     # Dogfooding 1회차 산출물
    └── dogfooding_log.md    # Dogfooding 과정 기록
```

## 개발 방법론

이 하네스는 **dogfooding** 방식으로 개발되었다 — 자기 자신의 프로세스를 사용해서 자기 자신을 기획했다.

- **1회차**: 하네스 흐름을 하네스 자체 기획에 적용. 4건의 설계 문제 발견 (포맷 불일치, 누락 단계, 구조 미정).
- **2회차**: 다른 프로젝트(주식 분석)에 하네스 적용. 3건의 추가 개선사항 발견 (인터뷰 규칙, 추천 로직, 난이도 정보).

7건의 발견 사항을 모두 즉시 설계에 반영. 상세 내용은 [pre-requirement/dogfooding_log.md](./pre-requirement/dogfooding_log.md) 참고.

## 문서

| 문서 | 설명 |
|---|---|
| [Plan.txt](./pre-requirement/Plan.txt) | 전체 흐름, 규칙, 로드맵이 담긴 마스터 플랜 |
| [dogfooding_log.md](./pre-requirement/dogfooding_log.md) | Dogfooding 1, 2회차 발견 및 개선 내역 |
| [project_profile.md](./pre-requirement/project_profile.md) | Dogfooding 1회차 산출물 (하네스 자체 프로필) |
| [gap_report.md](./pre-requirement/gap_report.md) | Dogfooding 1회차 누락/모순 분석 |
| [dev_checklist.md](./pre-requirement/dev_checklist.md) | Dogfooding 1회차 개발 착수 체크리스트 |

## 현재 상태

| Phase | 상태 | 산출물 |
|---|---|---|
| Phase 1 — kickoff-start | 🔲 미시작 | 아이디어 입력 + 유형 판별 스킬 |
| Phase 2 — kickoff-interview | 🔲 미시작 | 기획 & 설계 인터뷰 스킬 |
| Phase 3 — kickoff-suggest | 🔲 미시작 | AI 아이디어 제안 스킬 |
| Phase 4 — kickoff-profile | 🔲 미시작 | project_kickoff.md 생성 스킬 |
| Phase 5 — kickoff-gap | 🔲 미시작 | 누락/모순 점검 스킬 |
| Phase 6 — checklist + skills | 🔲 미시작 | 체크리스트 생성 + GitHub 스킬 가져오기 |
| Phase 7 — 통합 테스트 | 🔲 미시작 | 전체 흐름 검증 + 문서화 |

## 로드맵

### v2 (예정)

- Phase 문서 자동 생성
- 설계 문서 7종 자동 생성 (architecture, data model, requirements 등)
- Codex CLI / Gemini CLI 지원
- README 자동 생성 (readme-gen 스킬 활용)
- 인터뷰 종료 조건 (충분한 정보 수집 시 자동 감지)
- 프로젝트 유형별 질문 템플릿

---

<p align="center">Made with AI-assisted development</p>
