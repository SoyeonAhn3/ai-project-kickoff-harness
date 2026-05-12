# Phase 7 — IntegrationTest `Done`

> End-to-end flow (1->9) integration test and dogfooding documentation

**Status**: Done
**Prerequisites**: Phase 6

---

## Overview

Verify all skills work seamlessly from start to finish. Run with a new project idea, fix discovered issues, and update dogfooding_log.md with the final verification results.

---

## Deliverables

| # | Skill / Module | Status | Skill Type |
|---|---|---|---|
| 1 | Test scenario document | Done | - |
| 2 | Full flow execution (with design interview) | Done | - |
| 3 | Full flow execution (design interview skipped) | Skipped | - |
| 4 | Bug fixes | Done | - |
| 5 | dogfooding_log.md update | Done | - |
| 6 | Plan.txt final status update | Done | - |

---

## Test Scenarios

### Scenario A: Full Course (with design interview)

```
kickoff-start -> kickoff-interview (3-1 + 3-2) -> kickoff-suggest
-> kickoff-profile (sections 1-4) -> kickoff-gap -> kickoff-checklist -> kickoff-skills
```

Verification points:
- project_kickoff.md contains sections 1-6
- Design info (architecture, data structure, edge cases) is included
- 7 base skills present in .claude/skills/

### Scenario B: Planning Only (design interview skipped)

```
kickoff-start -> kickoff-interview (3-1 only) -> kickoff-suggest
-> kickoff-profile (section 1 only) -> kickoff-gap -> kickoff-checklist -> kickoff-skills
```

Verification points:
- project_kickoff.md does NOT contain sections 2-4
- Gap analysis scoped to profile (section 1) only

### Scenario C: Edge Cases

- 1-word idea input -> additional explanation requested
- "Recommend me" answer -> AI provides recommendation
- "Pass all" -> idea suggestion step skipped
- gh CLI not installed -> pass flow works

---

## Prerequisites & Dependencies

- Phase 1-6 all skills complete
- 1-2 test project ideas prepared

---

## Development Notes

- Bugs found during integration test must be fixed in the original Phase skill
- Re-run integration test after each fix to verify no regressions
- Record results in dogfooding_log.md round 3

---

## Change Log

| Date | Description |
|---|---|
| 2026-05-04 | Initial creation |
| 2026-05-06 | Scenario A (full course) integration test complete. 1 bug fixed. dogfooding_log round 3 recorded |

---
---

# Phase 7 — 통합 테스트 + 문서화 `완료`

> 전체 흐름(1->9) 통합 실행 검증 및 dogfooding 기록 갱신

**상태**: 완료
**선행 조건**: Phase 6 완료

---

## 개요

모든 스킬이 완성된 후 처음부터 끝까지 끊김 없이 동작하는지 검증한다. 새로운 프로젝트 아이디어로 전체 흐름을 실행하고, 발견된 문제를 수정. dogfooding_log.md를 갱신하여 최종 검증 결과를 기록.

---

## 완료 예정 / 완료 항목

| # | Skill / 모듈 | 상태 | 스킬 타입 |
|---|---|---|---|
| 1 | 통합 테스트 시나리오 작성 | 완료 | - |
| 2 | 전체 흐름 실행 (설계 인터뷰 포함) | 완료 | - |
| 3 | 전체 흐름 실행 (설계 인터뷰 패스) | 스킵 | - |
| 4 | 발견된 버그 수정 | 완료 | - |
| 5 | dogfooding_log.md 갱신 | 완료 | - |
| 6 | Plan.txt 최종 상태 반영 | 완료 | - |

---

## 테스트 시나리오

### 시나리오 A: 풀 코스 (설계 인터뷰 포함)

```
kickoff-start -> kickoff-interview (3-1 + 3-2) -> kickoff-suggest
-> kickoff-profile (섹션 1~4) -> kickoff-gap -> kickoff-checklist -> kickoff-skills
```

검증 포인트:
- project_kickoff.md에 섹션 1~6 모두 존재
- 설계 정보(아키텍처, 데이터구조, 엣지케이스) 포함 여부
- .claude/skills/에 기본 7개 스킬 존재

### 시나리오 B: 기획만 (설계 인터뷰 패스)

```
kickoff-start -> kickoff-interview (3-1만) -> kickoff-suggest
-> kickoff-profile (섹션 1만) -> kickoff-gap -> kickoff-checklist -> kickoff-skills
```

검증 포인트:
- project_kickoff.md에 섹션 2~4가 없음
- gap 점검이 프로필(섹션 1) 범위 내에서만 수행됨

### 시나리오 C: 엣지케이스

- 아이디어가 1단어일 때 추가 설명 요청 동작
- "추천해줘" 답변 시 AI 추천 제공 동작
- "전부 패스" 시 아이디어 제안 건너뛰기 동작
- gh CLI 미설치 시 패스 동작

---

## 선행 조건 및 의존성

- Phase 1~6 모든 스킬 완료
- 테스트용 프로젝트 아이디어 1~2개 준비

---

## 주의사항

- 통합 테스트에서 발견된 문제는 해당 Phase 스킬로 돌아가서 수정
- 수정 후 다시 통합 테스트 재실행하여 회귀 확인
- dogfooding_log.md에 3회차(자동화된 하네스 실행) 결과 기록

---

## 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026-05-04 | 최초 작성 |
| 2026-05-06 | 시나리오 A (풀 코스) 통합 테스트 완료. 버그 1건 수정. dogfooding_log 3회차 기록 |
