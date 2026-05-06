🌐 [한국어](./README_ko.md) | [English](./README.md)

# AI Project Kickoff Harness

> 막연한 프로젝트 아이디어를 AI 인터뷰와 검증을 통해 개발 가능한 계획으로 전환하는 CLI 자동화 하네스

## 개요

많은 프로젝트가 실패하는 이유는 코드가 아니라, 개발 전에 요구사항이 명확하지 않기 때문이다. 이 하네스는 구조화된 인터뷰를 진행하고, 누락과 모순을 찾아내고, 포괄적인 킥오프 문서를 생성한다 — 코드 한 줄 쓰기 전에.

이 하네스는 자기 자신을 사용해서(dogfooding) 개발되었다: 3회의 반복을 통해 8건 이상의 설계 개선을 발견하고 즉시 반영했다.

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
/kickoff-context     → 사용자 메타 정보 수집 (목적, 수준, 시간 예산)
/kickoff-start       → 사용자 아이디어 (자유 텍스트) → 프로젝트 유형 판별
/kickoff-interview   → 기획 인터뷰 (What) + 설계 인터뷰 (How — 패스 가능)
/kickoff-suggest     → AI 아이디어 제안 (최대 5개, 난이도+시간 포함)
/kickoff-profile     → project_kickoff.md 생성 (프로필 + 아키텍처 + 데이터 구조)
/kickoff-evaluate    → 정직한 평가 (가치 + 실현가능성 점검) [v1.5]
/kickoff-gap         → 누락/모순 점검 (개발 전에 문제 발견)
/kickoff-checklist   → 개발 착수 체크리스트 생성
/kickoff-done        → 완료 조건 생성 (측정 가능한 완료 기준) [v1.5]
/kickoff-skills      → 기본 스킬 세팅 (GitHub에서 7개 스킬 가져오기)
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
/kickoff-context        # (선택) 목적, 수준, 시간 예산 수집
/kickoff-start          # 아이디어 입력 + 프로젝트 유형 판별
/kickoff-interview      # 기획 & 설계 인터뷰
/kickoff-suggest        # AI 추가 아이디어 제안
/kickoff-profile        # project_kickoff.md 생성
/kickoff-evaluate       # 정직한 평가 (v1.5 — 개발 중)
/kickoff-gap            # 누락/모순 점검
/kickoff-checklist      # 개발 착수 체크리스트 생성
/kickoff-done           # 완료 조건 생성 (v1.5 — 개발 중)
/kickoff-skills         # GitHub에서 기본 스킬 가져오기
```

### 산출물

```
output/{프로젝트명}/{프로젝트명}_kickoff.md    # 단일 기준 문서
output/{프로젝트명}/kickoff_state.md          # 진행 상태 추적
.claude/skills/*                              # 기본 개발 스킬 7개
```

## 프로젝트 구조

```
AI-Project-Kickoff-Harness/
├── .claude/skills/              # Kickoff 스킬 + 개발 스킬
│   ├── kickoff-context/         # 사용자 컨텍스트 수집 (v1.5)
│   ├── kickoff-start/           # 아이디어 입력 + 유형 판별
│   ├── kickoff-interview/       # 기획 & 설계 인터뷰
│   ├── kickoff-suggest/         # AI 아이디어 제안
│   ├── kickoff-profile/         # 킥오프 문서 생성
│   ├── kickoff-gap/             # 누락/모순 점검
│   ├── kickoff-checklist/       # 개발 착수 체크리스트
│   ├── kickoff-skills/          # GitHub 스킬 가져오기
│   ├── dev-log/                 # 에러/변경 기록 (JSONL)
│   ├── github-push/             # 커밋 & 푸시 자동화
│   └── ...                      # 기타 기본 스킬
├── Phase/                       # Phase별 개발 문서
│   ├── Phase1~7                 # 핵심 스킬 (완료)
│   ├── Phase8_kickoff-context.md    # v1.5 — 컨텍스트 (완료)
│   ├── Phase9_kickoff-evaluate.md   # v1.5 — 정직한 평가
│   └── Phase10_kickoff-done.md      # v1.5 — 완료 조건
├── output/                      # 프로젝트별 킥오프 산출물
│   └── hr_data_analytics/       # 통합 테스트 산출물
└── pre-requirement/             # 기획 & dogfooding 산출물
    ├── Plan.txt                 # 마스터 플랜
    ├── backlog.md               # 개선 백로그
    └── dogfooding_log.md        # Dogfooding 3회차 기록
```

## 개발 방법론

이 하네스는 **dogfooding** 방식으로 개발되었다 — 자기 자신의 프로세스를 사용해서 자기 자신을 기획했다.

- **1회차**: 하네스 흐름을 하네스 자체 기획에 적용. 4건의 설계 문제 발견 (포맷 불일치, 누락 단계, 구조 미정).
- **2회차**: 다른 프로젝트(주식 분석)에 하네스 적용. 3건의 추가 개선사항 발견 (인터뷰 규칙, 추천 로직, 난이도 정보).
- **3회차**: HR 데이터 분석 프로젝트로 통합 테스트. 전체 흐름(start → interview → suggest → profile → gap → checklist) 검증. 버그 1건, gap 이슈 2건 발견 및 해결.

8건 이상의 발견 사항을 모두 즉시 설계에 반영. 상세 내용은 [pre-requirement/dogfooding_log.md](./pre-requirement/dogfooding_log.md) 참고.

## 문서

| 문서 | 설명 |
|---|---|
| [Plan.txt](./pre-requirement/Plan.txt) | 전체 흐름, 규칙, 로드맵이 담긴 마스터 플랜 |
| [dogfooding_log.md](./pre-requirement/dogfooding_log.md) | Dogfooding 1~3회차 발견 및 개선 내역 |
| [backlog.md](./pre-requirement/backlog.md) | 개선 백로그 (결정 배경 포함) |
| [project_profile.md](./pre-requirement/project_profile.md) | Dogfooding 1회차 산출물 (하네스 자체 프로필) |

## 현재 상태

| Phase | 상태 | 산출물 |
|---|---|---|
| Phase 1 — kickoff-start | ✅ 완료 | 아이디어 입력 + 유형 판별 스킬 |
| Phase 2 — kickoff-interview | ✅ 완료 | 기획 & 설계 인터뷰 스킬 |
| Phase 3 — kickoff-suggest | ✅ 완료 | AI 아이디어 제안 스킬 |
| Phase 4 — kickoff-profile | ✅ 완료 | project_kickoff.md 생성 스킬 |
| Phase 5 — kickoff-gap | ✅ 완료 | 누락/모순 점검 스킬 |
| Phase 6 — checklist + skills | ✅ 완료 | 체크리스트 생성 + GitHub 스킬 가져오기 |
| Phase 7 — 통합 테스트 | ✅ 완료 | 전체 흐름 검증 + 문서화 |
| Phase 8 — kickoff-context | ✅ 완료 | 컨텍스트 인식 프롬프팅 (v1.5) |
| Phase 9 — kickoff-evaluate | 🔲 미시작 | 정직한 평가 레이어 (v1.5) |
| Phase 10 — kickoff-done | 🔲 미시작 | 완료 조건 생성 (v1.5) |

## 로드맵

### v1.5 (진행 중)

- ✅ 컨텍스트 인식 프롬프팅 — 킥오프 전에 사용자 목적/수준/시간 수집
- 🔲 정직한 평가 레이어 — 5+1개 차원으로 프로젝트 실현가능성 점검
- 🔲 완료 조건 생성 — 측정 가능한 프로젝트 완료 기준 정의
- 🔲 조건부 보안 평가 (웹/앱 + 외부 사용자 대상만 활성화)

### v2 (예정)

- Phase 문서 자동 생성
- 설계 문서 7종 자동 생성 (architecture, data model, requirements 등)
- Codex CLI / Gemini CLI 지원
- 인터뷰 종료 조건 (충분한 정보 수집 시 자동 감지)

---

<p align="center">Made with AI-assisted development</p>
