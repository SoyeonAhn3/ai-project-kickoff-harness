# Phase 3 — KickoffSuggest `Done`

> Develop the skill that suggests additional ideas based on interview results

**Status**: Done
**Prerequisites**: Phase 2 complete

---

## Overview

After the interview is complete, AI analyzes the project type and answers to suggest up to 5 additional ideas. Each idea includes a usefulness rationale, difficulty level, and estimated time. Users can adopt/reject/modify/pass all.

---

## Deliverables

| # | Skill / Module | Status | Skill Type |
|---|---|---|---|
| 1 | `kickoff-suggest` SKILL.md | Done | project-specific |
| 2 | Suggestion output format definition | Done | - |
| 3 | Functional test | Done | Verified in Phase 7 integration test |

---

## kickoff-suggest

### Purpose

Suggest useful features/structures the user may not have considered, elevating the tool from a "document organizer" to a "co-planning partner."

### Implementation Files

```
.claude/skills/kickoff-suggest/
└── SKILL.md
```

No references needed (suggestion logic relies on AI context analysis, no static data)

### Core Behavior

1. Analyze interview answers + project type
2. Generate up to 5 ideas (table format)
3. Each idea: suggestion content + why useful + difficulty (Low/Medium/High) + estimated time
4. User selection: adopt by number / "pass all" / adopt with modifications
5. Classify adopted ideas as MVP or "future expansion"
6. Pass results to conversation context -> reflected in kickoff-profile

### Design Decisions

| Decision | Detail | Reason |
|---|---|---|
| Maximum 5 ideas | Prevent scope creep | Confirmed in dogfooding |
| Difficulty + time required | Necessary for adoption judgment | Discovered in dogfooding round 2 |
| "Pass all" explicit | Reference only, not mandatory | Minimize user burden |
| No references | No static data needed | AI generates dynamically based on context |

---

## Prerequisites & Dependencies

- Phase 2 complete (interview answers must be in conversation context)
- Refer to skill-template structure

---

## Development Notes

- Recommendations should prioritize alignment with user's purpose/context (follow recommendation rules)
- Do not duplicate features the user has already mentioned
- Clearly organize adoption results (MVP vs future expansion classification)

---

## Change Log

| Date | Description |
|---|---|
| 2026-05-04 | Initial creation |
| 2026-05-06 | Status update: implementation complete (Phase 7 integration test passed) |

---
---

# Phase 3 — kickoff-suggest 스킬 개발 `완료`

> 인터뷰 결과 기반으로 AI가 추가 아이디어를 제안하는 스킬 개발

**상태**: 완료
**선행 조건**: Phase 2 완료

---

## 개요

인터뷰 완료 후 AI가 프로젝트 유형과 답변을 분석하여 최대 5개의 추가 아이디어를 제안한다. 각 아이디어에 유용성 근거, 난이도, 예상 시간을 포함. 사용자가 채택/거절/수정/전부 패스를 선택.

---

## 완료 예정 / 완료 항목

| # | Skill / 모듈 | 상태 | 스킬 타입 |
|---|---|---|---|
| 1 | `kickoff-suggest` SKILL.md 작성 | 완료 | project-specific |
| 2 | 제안 출력 포맷 정의 | 완료 | - |
| 3 | 동작 테스트 | 완료 | Phase 7 통합 테스트에서 검증 |

---

## kickoff-suggest

### 목적

사용자가 생각하지 못한 유용한 기능/구조를 제안하여, "정리만 하는 도구"에서 "같이 기획하는 도구"로 가치를 높인다.

### 구현 파일

```
.claude/skills/kickoff-suggest/
└── SKILL.md
```

references 불필요 (제안 로직은 AI의 컨텍스트 분석에 의존, 정적 데이터 없음)

### 핵심 동작

1. 인터뷰 답변 + 프로젝트 유형을 분석
2. 최대 5개 아이디어 생성 (테이블 형태)
3. 각 아이디어: 제안 내용 + 왜 유용한지 + 난이도(낮/중/높) + 예상 시간
4. 사용자 선택: 번호로 채택 / "전부 패스" / 수정 채택
5. 채택된 아이디어를 MVP 또는 "이후 확장"으로 분류
6. 결과를 대화 컨텍스트에 전달 -> kickoff-profile에서 반영

### 설계 결정 사항

| 결정 | 내용 | 이유 |
|---|---|---|
| 최대 5개 | scope creep 방지 | dogfooding에서 확정 |
| 난이도+시간 필수 | 채택 판단에 필요 | dogfooding 2회차에서 발견 |
| "전부 패스" 명시 | 강제가 아닌 참고용 | 사용자 부담 최소화 |
| references 없음 | 정적 데이터 불필요 | AI가 컨텍스트 기반으로 동적 생성 |

---

## 선행 조건 및 의존성

- Phase 2 완료 (인터뷰 답변이 대화 컨텍스트에 있어야 함)
- skill-template 구조 참고

---

## 개발 시 주의사항

- 제안은 사용자의 목적/맥락에 맞는 것 우선 (추천 규칙 준수)
- 이미 사용자가 언급한 기능을 중복 제안하지 않기
- 채택 결과를 명확히 정리 (MVP vs 확장 분류)

---

## 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026-05-04 | 최초 작성 |
| 2026-05-06 | 상태 갱신: 구현 완료 반영 (Phase 7 통합 테스트 통과 확인) |
