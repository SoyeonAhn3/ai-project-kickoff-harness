# Phase 2 — KickoffInterview `Done`

> Develop the skill that conducts planning interview (3-1) and design interview (3-2) to collect requirements

**Status**: Done
**Prerequisites**: Phase 1 complete

---

## Overview

After type determination, this skill asks the user planning/design questions to collect project requirements. Split into Planning Interview (What) and Design Interview (How), with the design interview being skippable. Uses the B+C method (bundled questions + follow-up questions when insufficient).

---

## Deliverables

| # | Skill / Module | Status | Skill Type |
|---|---|---|---|
| 1 | `kickoff-interview` SKILL.md | Done | project-specific |
| 2 | `references/planning-questions.md` | Done | - |
| 3 | `references/design-questions.md` | Done | - |
| 4 | Interview rules applied (B+C method, recommendation rules) | Done | - |
| 5 | Functional test | Done | Verified in Phase 7 integration test |

---

## kickoff-interview

### Purpose

Collect planning/design requirements comprehensively through questions tailored to the project type.

### Implementation Files

```
.claude/skills/kickoff-interview/
├── SKILL.md
└── references/
    ├── planning-questions.md   # Type-specific planning question guide
    └── design-questions.md     # Type-specific design question guide
```

### Core Behavior

Step 3-1 (Planning Interview):
1. Present 3-5 bundled planning questions tailored to the project type
2. Collect answers -> ask follow-up questions if insufficient (C method)
3. Confirm planning completion

Step 3-2 (Design Interview):
1. Ask "Shall we move to design questions? (skip available)" for confirmation
2. If skipped -> move to kickoff-suggest
3. If proceeding -> ask questions in 4 areas:
   - Pipeline flow
   - Layer-specific table/data structure (column recommendations + reasoning)
   - Data volume and refresh frequency
   - Failure scenarios / edge cases

### Design Decisions

| Decision | Detail | Reason |
|---|---|---|
| Question method | B+C (bundled + follow-up) | Confirmed in dogfooding |
| "Recommend for me" allowed | For all technical questions | Support for non-technical users |
| Recommendation priority | Purpose-fit > ease of use | Discovered in dogfooding round 2 |
| Design interview skip | Explicit skip option provided | Support for users who only want planning |

---

## Prerequisites & Dependencies

- Phase 1 complete (type information must be in conversation context)
- Refer to skill-template structure

---

## Development Notes

- Type-specific questions require type x question mapping in references
- When user answers "I don't know", immediately provide AI recommendation
- Do not ask trivial details (maintain kickoff-level scope)
- When recommending columns in design interview, must explain "why this column is needed"

---

## Change Log

| Date | Description |
|---|---|
| 2026-05-04 | Initial creation |
| 2026-05-06 | Status update: implementation complete (Phase 7 integration test passed) |

---
---

# Phase 2 — kickoff-interview 스킬 개발 `완료`

> 기획 인터뷰(3-1)와 설계 인터뷰(3-2)를 수행하여 요구사항을 수집하는 스킬 개발

**상태**: 완료
**선행 조건**: Phase 1 완료

---

## 개요

유형 판별 후 사용자에게 기획/설계 질문을 던져 프로젝트 요구사항을 수집한다. 기획 인터뷰(What)와 설계 인터뷰(How)로 분리되며, 설계 인터뷰는 패스 가능. B+C 방식(묶음 질문 + 부족 시 추가 질문)으로 진행.

---

## 완료 예정 / 완료 항목

| # | Skill / 모듈 | 상태 | 스킬 타입 |
|---|---|---|---|
| 1 | `kickoff-interview` SKILL.md 작성 | 완료 | project-specific |
| 2 | `references/planning-questions.md` 작성 | 완료 | - |
| 3 | `references/design-questions.md` 작성 | 완료 | - |
| 4 | 인터뷰 규칙 반영 (B+C 방식, 추천 규칙) | 완료 | - |
| 5 | 동작 테스트 | 완료 | Phase 7 통합 테스트에서 검증 |

---

## kickoff-interview

### 목적

프로젝트 유형에 맞는 질문을 통해 기획/설계 요구사항을 빠짐없이 수집한다.

### 구현 파일

```
.claude/skills/kickoff-interview/
├── SKILL.md
└── references/
    ├── planning-questions.md   # 유형별 기획 질문 가이드
    └── design-questions.md     # 유형별 설계 질문 가이드
```

### 핵심 동작

Step 3-1 (기획 인터뷰):
1. 프로젝트 유형에 맞는 기획 질문 3~5개 묶어서 제시
2. 답변 수집 -> 부족하면 추가 질문 (C방식)
3. 기획 완료 확인

Step 3-2 (설계 인터뷰):
1. "설계 질문으로 넘어갈까요? (패스 가능)" 확인
2. 패스 시 -> kickoff-suggest로 이동
3. 진행 시 -> 4개 영역 질문
   - 파이프라인 흐름
   - 레이어별 테이블/데이터 구조 (컬럼 추천 + 이유 설명)
   - 데이터 볼륨 및 갱신 주기
   - 실패 시나리오 / 엣지케이스

### 설계 결정 사항

| 결정 | 내용 | 이유 |
|---|---|---|
| 질문 방식 | B+C (묶음 + 추가) | dogfooding에서 확정 |
| "추천해줘" 허용 | 모든 기술 질문에서 | 비기술 사용자 대응 |
| 추천 우선순위 | 목적에 맞는 것 > 쉬운 것 | dogfooding 2회차에서 발견 |
| 설계 인터뷰 패스 | 명시적 선택지 제공 | 기획만 원하는 사용자 대응 |

---

## 선행 조건 및 의존성

- Phase 1 완료 (유형 정보가 대화 컨텍스트에 있어야 함)
- skill-template 구조 참고

---

## 개발 시 주의사항

- 유형별 질문이 다르므로 references에 유형x질문 매핑 필요
- "잘 모르겠어" 답변 시 반드시 AI 추천을 바로 제시
- 사소한 디테일은 묻지 않음 (킥오프 수준 유지)
- 설계 인터뷰에서 컬럼 추천 시 "왜 이 컬럼이 필요한지" 설명 필수

---

## 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026-05-04 | 최초 작성 |
| 2026-05-06 | 상태 갱신: 구현 완료 반영 (Phase 7 통합 테스트 통과 확인) |
