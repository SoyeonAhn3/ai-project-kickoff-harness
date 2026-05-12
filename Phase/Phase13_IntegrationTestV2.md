# Phase 13 — IntegrationTestV2 `Completed`

> End-to-end validation of v2 design document chain

**Completed**: 2026-05-12
**Status**: ✅ Completed
**Prerequisites**: Phase 12 complete
**Version**: v2

---

## Overview

Validate the complete design document chain works seamlessly with the kickoff flow. Run design skills on a completed kickoff project and verify all sections are correctly added to `_kickoff.md`.

---

## Deliverables

| # | Item | Status | Notes |
|---|---|---|---|
| 1 | Test scenarios defined | ✅ | 5 scenarios (A-E) |
| 2 | Scenario A: full flow with AI project | ✅ | design-requirements through ai-workflow |
| 3 | Scenario B: full flow non-AI project | ✅ | Skip ai-workflow |
| 4 | Scenario C: "undecided" tech stack | ✅ | Forced resolution test |
| 5 | Scenario D: re-run / edit test | ✅ | Edit existing + Revision History |
| 6 | Scenario E: cross-section edit test | ✅ | User confirmation flow |
| 7 | dogfooding_log update | ✅ | v2 round results — BL-012~016 discovered and resolved |

---

## Test Scenarios

### Scenario A — AI Project (Full Flow)

**Flow**: design-requirements -> design-architecture -> design-data-model -> design-ai-workflow -> kickoff-gap -> kickoff-checklist

**Verification**:
- Sections 9-12 all present in `_kickoff.md`
- Section 12 (AI Workflow) included with full content
- Type-specific content matches AI project patterns (serving/training split, prompt design, etc.)
- `last_skill` correctly updated at each step
- YAML frontmatter reflects final state: `last_skill: design-ai-workflow`
- gap detects v2 cross-section consistency issues (category 7)
- checklist generates project structure tree + .env.example

### Scenario B — Non-AI Project

**Flow**: design-requirements -> design-architecture -> design-data-model -> kickoff-gap -> kickoff-checklist

**Verification**:
- Sections 9, 10, 11 present in `_kickoff.md`
- Section 12 does NOT exist (ai-workflow skipped)
- gap correctly follows data-model (`last_skill` = `design-data-model` as prerequisite)
- Type-specific content matches non-AI patterns (e.g., WebApp: DB schema, component/page-based structure)

### Scenario C — "Undecided" Tech Stack

**Setup**: Completed kickoff project with "undecided" in tech stack section

**Flow**: Run design-requirements

**Verification**:
- design-requirements detects "undecided" before STEP 1
- User prompted to confirm tech stack (or request AI recommendation)
- After resolution, kickoff doc tech stack section is edited
- Revision History records the tech stack update
- STEP 1 proceeds only after resolution

### Scenario D — Re-run (Edit Existing)

**Setup**: Completed project with sections 9-13 already present

**Flow**: Run design-requirements again

**Verification**:
- Existing section 9 is edited in-place (NOT duplicated)
- Revision History table at document bottom is updated with new entry
- Content reflects any changes from the re-run
- No orphaned or duplicated sections in `_kickoff.md`

### Scenario E — Cross-Section Edit

**Setup**: During design-architecture, a requirements gap is discovered

**Flow**: design-architecture detects section 9 needs modification

**Verification**:
- User asked: "Section 9 [item] needs modification. Proceed?"
- If user agrees: section 9 is edited + Revision History updated
- If user declines: section 10 contains note about the gap
- Document coherence maintained after edit

---

## Dependencies

- Phase 11 and Phase 12 skill development complete
- At least one completed kickoff project available (from v1 integration test or newly created)
- All 4 design skills functional: design-requirements, design-architecture, design-data-model, design-ai-workflow

---

## Test Execution Notes

- Fix bugs discovered in original Phase skills during testing, then re-test after fix
- Update dogfooding_log with v2 round observations
- Verify `_kickoff.md` remains a coherent single file throughout all scenarios
- Check that YAML frontmatter `last_skill` is correctly chained at every step
- Confirm Revision History table accumulates entries correctly across multiple runs

---

## Verification

1. All 5 scenarios (A-E) pass without errors
2. `_kickoff.md` remains a coherent, well-structured single file after full flow
3. AI project flow includes all 4 design sections (9-12)
4. Non-AI project flow includes 3 design sections (9-11) with section 12 skipped
5. Re-run produces edits (not duplicates) with Revision History tracking
6. Cross-section edit flow respects user confirmation
7. BL-012~016 discovered and resolved through finance_data_platform integration test

---

## Change Log

| Date | Description |
|---|---|
| 2026-05-12 | Initial creation |
| 2026-05-12 | Completed — design-impl-spec removed (BL-013), scenarios updated to 4 design skills, BL-012~016 resolved |

---
---

# Phase 13 — IntegrationTestV2 `완료`

> v2 설계 문서 체인의 엔드투엔드 검증

**완료일**: 2026-05-12
**상태**: ✅ 완료
**선행 조건**: Phase 12 완료
**버전**: v2

---

## 개요

설계 문서 체인 전체가 킥오프 플로우와 매끄럽게 연결되는지 검증한다. 완료된 킥오프 프로젝트에 설계 스킬을 실행하고, 모든 섹션이 `_kickoff.md`에 올바르게 추가되는지 확인한다.

---

## 완료 예정 항목

| # | 항목 | 상태 | 비고 |
|---|---|---|---|
| 1 | 테스트 시나리오 정의 | ✅ | 5개 시나리오 (A-E) |
| 2 | 시나리오 A: AI 프로젝트 전체 흐름 | ✅ | design-requirements부터 ai-workflow까지 |
| 3 | 시나리오 B: 비AI 프로젝트 전체 흐름 | ✅ | ai-workflow 건너뜀 |
| 4 | 시나리오 C: "미정" 기술 스택 | ✅ | 강제 해소 테스트 |
| 5 | 시나리오 D: 재실행 / 편집 테스트 | ✅ | 기존 섹션 Edit + Revision History |
| 6 | 시나리오 E: 교차 섹션 편집 테스트 | ✅ | 사용자 확인 흐름 |
| 7 | dogfooding_log 업데이트 | ✅ | v2 라운드 결과 — BL-012~016 발견 및 해결 |

---

## 테스트 시나리오

### 시나리오 A — AI 프로젝트 (전체 흐름)

**흐름**: design-requirements -> design-architecture -> design-data-model -> design-ai-workflow -> kickoff-gap -> kickoff-checklist

**검증 항목**:
- `_kickoff.md`에 섹션 9~12 모두 존재
- 섹션 12 (AI 워크플로우) 전체 내용 포함
- AI 프로젝트 패턴에 맞는 유형별 콘텐츠 (서빙/학습 분리, 프롬프트 설계 등)
- 각 단계에서 `last_skill` 정상 갱신
- YAML frontmatter 최종 상태: `last_skill: design-ai-workflow`
- gap이 v2 교차 섹션 정합성 점검 (카테고리 7)
- checklist가 프로젝트 구조 트리 + .env.example 생성

### 시나리오 B — 비AI 프로젝트

**흐름**: design-requirements -> design-architecture -> design-data-model -> kickoff-gap -> kickoff-checklist

**검증 항목**:
- `_kickoff.md`에 섹션 9, 10, 11 존재
- 섹션 12 미존재 (ai-workflow 건너뜀)
- gap이 data-model 직후 실행 (`last_skill` = `design-data-model`이 사전 조건)
- 비AI 패턴에 맞는 유형별 콘텐츠 (예: 웹앱이면 DB 스키마, 컴포넌트/페이지별 구조)

### 시나리오 C — "미정" 기술 스택

**설정**: 기술 스택에 "미정"이 포함된 킥오프 완료 프로젝트

**흐름**: design-requirements 실행

**검증 항목**:
- design-requirements가 STEP 1 전에 "미정" 감지
- 사용자에게 기술 스택 확정 요청 (또는 AI 추천 요청)
- 해소 후 킥오프 문서 기술 스택 섹션 편집 완료
- Revision History에 기술 스택 변경 기록
- 해소 후에만 STEP 1 진행

### 시나리오 D — 재실행 (기존 섹션 편집)

**설정**: 섹션 9~13이 이미 존재하는 완료된 프로젝트

**흐름**: design-requirements 재실행

**검증 항목**:
- 기존 섹션 9가 제자리에서 편집됨 (중복 생성 안 됨)
- 문서 하단 Revision History 테이블에 새 항목 추가
- 재실행 결과가 내용에 반영
- `_kickoff.md`에 고아 또는 중복 섹션 없음

### 시나리오 E — 교차 섹션 편집

**설정**: design-architecture 수행 중 요구사항 누락 발견

**흐름**: design-architecture가 섹션 9 수정 필요 감지

**검증 항목**:
- 사용자에게 "섹션 9의 [항목]을 수정해야 합니다. 수정할까요?" 확인
- 사용자 동의 시: 섹션 9 편집 + Revision History 업데이트
- 사용자 거부 시: 섹션 10에 해당 누락 사항 메모 포함
- 편집 후 문서 일관성 유지

---

## 의존성

- Phase 11, Phase 12 스킬 개발 완료
- 킥오프 완료 프로젝트 최소 1개 (v1 통합 테스트 또는 신규 생성)
- 설계 스킬 4종 모두 동작: design-requirements, design-architecture, design-data-model, design-ai-workflow

---

## 테스트 실행 시 주의사항

- 테스트 중 발견된 기존 Phase 스킬 버그 수정 후 재테스트
- dogfooding_log에 v2 라운드 관찰사항 기록
- 모든 시나리오에서 `_kickoff.md`가 일관된 단일 파일로 유지되는지 확인
- 매 단계에서 YAML frontmatter `last_skill`이 올바르게 체이닝되는지 확인
- 여러 번 실행 시 Revision History 테이블이 누적 기록되는지 확인

---

## 검증 방법

1. 5개 시나리오 (A-E) 모두 오류 없이 통과
2. 전체 흐름 후 `_kickoff.md`가 일관된 단일 파일로 유지
3. AI 프로젝트 흐름에 설계 섹션 4개 (9-12) 모두 포함
4. 비AI 프로젝트 흐름에 설계 섹션 3개 (9-11) 포함 + 섹션 12 건너뜀
5. 재실행 시 편집 (중복 아님) + Revision History 추적
6. 교차 섹션 편집 흐름에서 사용자 확인 준수
7. finance_data_platform 통합테스트로 BL-012~016 발견 및 해결

---

## 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026-05-12 | 최초 작성 |
| 2026-05-12 | 완료 — design-impl-spec 삭제 (BL-013), 시나리오를 4종 설계 스킬 기준으로 갱신, BL-012~016 해결 |
