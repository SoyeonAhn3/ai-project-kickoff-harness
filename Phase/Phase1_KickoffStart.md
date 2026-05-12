# Phase 1 — KickoffStart `Done`

> Develop the entry skill that receives user ideas and determines the project type

**Status**: Done
**Prerequisites**: None (first Phase)

---

## Overview

The first skill of the harness. When a user inputs a project idea in free text, the AI determines the project type and asks the user to confirm. Serves as the entry point leading into kickoff-interview.

---

## Deliverables

| # | Skill / Module | Status | Skill Type |
|---|---|---|---|
| 1 | `kickoff-start` SKILL.md | Done | project-specific |
| 2 | `references/project-types.md` | Done | - |
| 3 | Type determination logic definition | Done | - |
| 4 | Functional test | Done | Verified in Phase 7 integration test |

---

## kickoff-start

### Purpose

Collect the user's vague idea and automatically determine the project type, setting the direction for subsequent interviews.

### Implementation Files

```
.claude/skills/kickoff-start/
├── SKILL.md
└── references/
    └── project-types.md    # Type classification criteria and characteristics per type
```

### Core Behavior

1. Request idea input from user (free text, Korean/English)
2. Analyze keywords/patterns from input -> determine type
3. Present determination result to user + request confirmation
4. Pass confirmed type to conversation context -> used by kickoff-interview

### Design Decisions

| Decision | Detail | Reason |
|---|---|---|
| Number of type categories | 7 (AI, Automation, BI, Pipeline, WebApp, CLI, Library) | Classification defined in Plan.txt |
| Allow complex types | Yes (e.g., "Data Pipeline + BI") | Complex types observed in dogfooding round 2 |
| On determination failure | Request direct selection from user | User decision is more accurate than forced AI determination |

### Usage Example

```
User: /kickoff-start
AI: "What project would you like to build? Please describe freely."
User: "A system that monitors production data, detects anomalies, and has AI analyze the root cause"
AI: "Project type determined as: Data Pipeline + AI. Is this correct?"
User: "Yes"
AI: "Confirmed. Please proceed to the next step with /kickoff-interview."
```

---

## Prerequisites & Dependencies

- Refer to skill-template structure (frontmatter, STEP, failure handling)
- Reference project type list from Plan.txt

---

## Development Notes

- Type determination relies on "user confirmation" rather than accuracy. Even if incorrectly determined, the user can correct it.
- For complex types, distinguish between primary type + secondary type
- If idea input is too short (1-2 words), request additional explanation

---

## Change Log

| Date | Description |
|---|---|
| 2026-05-04 | Initial creation |
| 2026-05-06 | Status update: implementation complete (Phase 7 integration test passed) |

---
---

# Phase 1 — kickoff-start 스킬 개발 `완료`

> 사용자의 아이디어를 입력받고 프로젝트 유형을 판별하는 진입 스킬 개발

**상태**: 완료
**선행 조건**: 없음 (첫 Phase)

---

## 개요

하네스의 첫 번째 스킬. 사용자가 자유 텍스트로 프로젝트 아이디어를 입력하면, AI가 프로젝트 유형을 판별하고 사용자에게 확인을 받는다. 이후 kickoff-interview로 이어지는 진입점 역할.

---

## 완료 예정 / 완료 항목

| # | Skill / 모듈 | 상태 | 스킬 타입 |
|---|---|---|---|
| 1 | `kickoff-start` SKILL.md 작성 | 완료 | project-specific |
| 2 | `references/project-types.md` 작성 | 완료 | - |
| 3 | 유형 판별 로직 정의 | 완료 | - |
| 4 | 동작 테스트 | 완료 | Phase 7 통합 테스트에서 검증 |

---

## kickoff-start

### 목적

사용자의 막연한 아이디어를 수집하고, 프로젝트 유형을 자동 판별하여 이후 인터뷰의 방향을 결정한다.

### 구현 파일

```
.claude/skills/kickoff-start/
├── SKILL.md
└── references/
    └── project-types.md    # 유형 분류 기준 및 각 유형별 특성
```

### 핵심 동작

1. 사용자에게 아이디어 입력 요청 (자유 텍스트, 한/영)
2. 입력 내용에서 키워드/패턴 분석 -> 유형 판별
3. 판별 결과를 사용자에게 제시 + 확인 요청
4. 확정된 유형을 대화 컨텍스트에 전달 -> kickoff-interview에서 사용

### 설계 결정 사항

| 결정 | 내용 | 이유 |
|---|---|---|
| 유형 분류 개수 | 7개 (AI, 자동화, BI, 파이프라인, 웹앱, CLI, 라이브러리) | Plan.txt에서 정의된 분류 |
| 복합 유형 허용 | 예 (예: "데이터 파이프라인 + BI") | dogfooding 2회차에서 복합 유형 발생 확인 |
| 판별 실패 시 | 사용자에게 직접 선택 요청 | AI가 모를 때 강제 판별보다 사용자 결정이 정확 |

### 사용 예시

```
사용자: /kickoff-start
AI: "어떤 프로젝트를 만들고 싶으신가요? 자유롭게 설명해주세요."
사용자: "생산 데이터를 보고 이상을 감지하고 AI가 원인을 분석해주는 시스템"
AI: "프로젝트 유형: 데이터 파이프라인 + AI로 판별됩니다. 맞나요?"
사용자: "맞아"
AI: "확정되었습니다. /kickoff-interview로 다음 단계를 진행해주세요."
```

---

## 선행 조건 및 의존성

- skill-template 구조 참고 (frontmatter, STEP, 실패 처리)
- Plan.txt의 프로젝트 유형 목록 참조

---

## 개발 시 주의사항

- 유형 판별은 정확도보다 "사용자 확인"에 의존. 잘못 판별해도 사용자가 수정 가능하게.
- 복합 유형 시 주요 유형 + 부가 유형으로 구분
- 아이디어 입력이 너무 짧으면 (1~2단어) 추가 설명 요청

---

## 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026-05-04 | 최초 작성 |
| 2026-05-06 | 상태 갱신: 구현 완료 반영 (Phase 7 통합 테스트 통과 확인) |
