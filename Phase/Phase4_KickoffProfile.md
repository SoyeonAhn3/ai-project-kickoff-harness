# Phase 4 — KickoffProfile `Done`

> Develop the skill that structures interview answers and adopted ideas to generate project_kickoff.md

**Status**: Done
**Prerequisites**: Phase 3 complete

---

## Overview

Structures interview answers + adopted ideas accumulated in the conversation context to generate the project_kickoff.md file. This file serves as the reference document that subsequent skills (kickoff-gap, kickoff-checklist) read and append sections to.

---

## Deliverables

| # | Skill / Module | Status | Skill Type |
|---|---|---|---|
| 1 | `kickoff-profile` SKILL.md | Done | project-specific |
| 2 | `references/profile-template.md` | Done | - |
| 3 | Section 1-4 structure definition | Done | - |
| 4 | Section omission logic when design interview is skipped | Done | - |
| 5 | Functional test | Done | Verified in Phase 7 integration test |

---

## kickoff-profile

### Purpose

Consolidate scattered interview results into a single structured reference document, serving as the Single Source of Truth for all subsequent steps.

### Implementation Files

```
.claude/skills/kickoff-profile/
├── SKILL.md
└── references/
    └── profile-template.md   # project_kickoff.md standard structure/section guide
```

### Core Behavior

1. Collect interview answers + adopted ideas from conversation context
2. Create `{project}/pre-requirement/` folder in the harness parent directory (BL-002)
3. Update the output path in state file section 0 to the new project folder
4. Write project_kickoff.md referencing profile-template.md:
   - Section 1: Project Profile (basic info, purpose, users, core features, tech stack, constraints)
   - Section 2: System Architecture (pipeline flow, component structure)
   - Section 3: Data Structure (layer-specific tables, columns, volume, refresh frequency)
   - Section 4: Failure Scenarios / Edge Cases
5. If design interview (3-2) was skipped, omit sections 2, 3, 4
6. Save file and confirm with user

### Design Decisions

| Decision | Detail | Reason |
|---|---|---|
| Save location | ../{project}/pre-requirement/{project}_kickoff.md | Separate harness and project (BL-002) |
| Folder creation timing | At profile execution (just before document creation) | Not needed during interview phase |
| Format | Markdown | Confirmed during interview |
| Sections 2-4 conditional | Omitted when design interview is skipped | Support for users who only want planning |
| Template usage | references/profile-template.md | Ensure consistent output, enable independent updates |

---

## Prerequisites & Dependencies

- Phase 3 complete (interview answers + adopted ideas must be in context)
- Refer to skill-template structure

---

## Development Notes

- project_kickoff.md is read and appended to by subsequent skills, so section header format must be maintained clearly
- Items answered with "recommend for me" during interview should be marked as AI-recommended
- Adopted ideas must clearly indicate MVP/future expansion classification

---

## Change Log

| Date | Description |
|---|---|
| 2026-05-04 | Initial creation |
| 2026-05-06 | Status update: implementation complete (Phase 7 integration test passed) |
| 2026-05-07 | BL-002 applied: added STEP 2 project folder creation, changed output path to outside harness |

---
---

# Phase 4 — kickoff-profile 스킬 개발 `완료`

> 인터뷰 답변과 채택 아이디어를 구조화하여 project_kickoff.md를 생성하는 스킬 개발

**상태**: 완료
**선행 조건**: Phase 3 완료

---

## 개요

대화 컨텍스트에 쌓인 인터뷰 답변 + 채택된 아이디어를 구조화하여 project_kickoff.md 파일을 생성한다. 이 파일은 이후 kickoff-gap, kickoff-checklist가 읽고 섹션을 추가하는 기준 문서.

---

## 완료 예정 / 완료 항목

| # | Skill / 모듈 | 상태 | 스킬 타입 |
|---|---|---|---|
| 1 | `kickoff-profile` SKILL.md 작성 | 완료 | project-specific |
| 2 | `references/profile-template.md` 작성 | 완료 | - |
| 3 | 섹션 1~4 구조 정의 | 완료 | - |
| 4 | 설계 인터뷰 패스 시 섹션 생략 로직 | 완료 | - |
| 5 | 동작 테스트 | 완료 | Phase 7 통합 테스트에서 검증 |

---

## kickoff-profile

### 목적

흩어진 인터뷰 결과를 하나의 구조화된 기준 문서로 만들어, 이후 모든 단계의 Single Source of Truth가 되게 한다.

### 구현 파일

```
.claude/skills/kickoff-profile/
├── SKILL.md
└── references/
    └── profile-template.md   # project_kickoff.md 표준 구조/섹션 가이드
```

### 핵심 동작

1. 대화 컨텍스트에서 인터뷰 답변 + 채택 아이디어 수집
2. 하네스 상위 디렉토리에 `{프로젝트명}/pre-requirement/` 폴더 생성 (BL-002)
3. 상태 파일 섹션 0의 산출물 경로를 새 프로젝트 폴더로 갱신
4. profile-template.md 참조하여 project_kickoff.md 작성:
   - 섹션 1: 프로젝트 프로필 (기본정보, 목적, 사용자, 핵심기능, 기술스택, 제약사항)
   - 섹션 2: 시스템 아키텍처 (파이프라인 흐름, 컴포넌트 구성)
   - 섹션 3: 데이터 구조 (레이어별 테이블, 컬럼, 볼륨, 갱신주기)
   - 섹션 4: 실패 시나리오 / 엣지케이스
5. 설계 인터뷰(3-2)를 패스한 경우 섹션 2, 3, 4 생략
6. 파일 저장 후 사용자에게 확인

### 설계 결정 사항

| 결정 | 내용 | 이유 |
|---|---|---|
| 저장 위치 | ../{프로젝트명}/pre-requirement/{프로젝트명}_kickoff.md | 하네스와 프로젝트 분리 (BL-002) |
| 폴더 생성 시점 | profile 실행 시 (문서 생성 직전) | 인터뷰 단계에서는 아직 불필요 |
| 포맷 | Markdown | 인터뷰에서 확정 |
| 섹션 2~4 조건부 | 설계 인터뷰 패스 시 생략 | 기획만 원하는 사용자 대응 |
| template 사용 | references/profile-template.md | 일관된 출력 보장, 독립 업데이트 가능 |

---

## 선행 조건 및 의존성

- Phase 3 완료 (인터뷰 답변 + 채택 아이디어가 컨텍스트에 있어야 함)
- skill-template 구조 참고

---

## 개발 시 주의사항

- project_kickoff.md는 이후 스킬이 읽고 추가하므로, 섹션 헤더 포맷을 명확히 유지
- 사용자가 인터뷰에서 "추천해줘"로 답한 항목은 AI 추천 내용이 반영됨을 표기
- 채택된 아이디어는 MVP/확장 분류를 명시

---

## 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026-05-04 | 최초 작성 |
| 2026-05-06 | 상태 갱신: 구현 완료 반영 (Phase 7 통합 테스트 통과 확인) |
| 2026-05-07 | BL-002 반영: STEP 2 프로젝트 폴더 생성 추가, 산출물 경로를 하네스 외부로 변경 |
