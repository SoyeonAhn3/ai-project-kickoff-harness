# Phase 11 — DesignRequirementsArchitecture `Completed`

> Requirements specification (section 9) and system architecture (section 10) design skills

**Completed**: 2026-05-12
**Status**: ✅ Completed
**Prerequisites**: Phase 10 complete
**Version**: v2

---

## Overview

Transition from kickoff (What+Why) to design (How). Two skills that add sections to `_kickoff.md`:
- **design-requirements** (section 9): Decompose core features into detailed requirements, define NFRs and user flows
- **design-architecture** (section 10): Define system structure, tech selection rationale, component design

design-requirements is the v2 entry point, so it handles "undecided" tech stack forced resolution and kickoff completion verification.

---

## Deliverable Rules (v2 Common)

| Item | Decision |
|---|---|
| Output location | Sections added to `_kickoff.md` (no separate files) |
| Creation | First run: add section, re-run: Edit existing |
| Change history | Revision History table at document bottom |
| Cross-section edits | Ask user first, or note in current section |
| Progress tracking | YAML frontmatter `last_skill` |

---

## Deliverables

| # | Skill / Module | Status | Notes |
|---|---|---|---|
| 1 | `design-requirements` SKILL.md | ✅ | 7 STEPs, depends_on: kickoff-done |
| 2 | `references/requirements-template.md` | ✅ | FR/NFR/flow rules, 7 type overrides |
| 3 | `references/nfr-checklist.md` | ✅ | 7 NFR categories, conditional activation |
| 4 | `design-architecture` SKILL.md | ✅ | 7 STEPs, depends_on: design-requirements |
| 5 | `references/architecture-template.md` | ✅ | Section 10 structure, deployment rules |
| 6 | `references/architecture-patterns.md` | ✅ | Type-specific patterns, ADR template |
| 7 | `profile-template.md` (modified) | ✅ | Section 9-13 placeholders + Revision History |
| 8 | `kickoff-skills/SKILL.md` (modified) | ✅ | v2 design transition prompt in STEP 4 |

---

## 1. design-requirements

### Prerequisites

1. Kickoff document exists (`**/*_kickoff.md` Glob)
2. YAML frontmatter `last_skill` >= `kickoff-done`
3. **"Undecided" tech stack forced resolution**: If `### Tech Stack` contains "undecided", request confirmation
   - "Don't know / recommend" allowed -> AI recommends based on type+purpose with rationale
   - After confirmation, reflect in kickoff doc (Edit) -> proceed to STEP 1

### STEP Structure

| STEP | Description | Output |
|---|---|---|
| STEP 1 | Analyze kickoff doc + confirm project type | Requirements extraction input |
| STEP 2 | Functional requirements (decompose core features) | Feature list draft (FR-001...) |
| STEP 3 | Non-functional requirements by type+purpose | NFR list |
| STEP 4 | User flows (2-5 key scenarios) | User flow diagrams |
| STEP 5 | Additional interview (gaps only) | Supplemented requirements |
| STEP 6 | Present + confirm -> add section 9 to kickoff doc | `last_skill` updated |

### STEP 1 — Kickoff Document Analysis

| Section to Read | Extraction Target |
|---|---|
| Basic Info -> Type | Select type-specific template |
| Core Features table | Feature list + mandatory/optional classification |
| Tech Stack | Implementation constraints |
| Constraints/Risks | NFR candidates |
| Project Context | Purpose, skill level, time budget |
| Adopted AI Suggestions | Additional feature candidates |
| Done Conditions | Acceptance criteria linkage |

### STEP 2 — Functional Requirements

| Field | Description |
|---|---|
| Feature ID | FR-001, FR-002, ... |
| Feature Name | Inherited from kickoff doc feature names |
| Detailed Description | 1-2 sentences |
| Input / Output | Data flow |
| Priority | Mandatory (MVP) / Optional (v2+) — inherited from kickoff classification |
| Acceptance Criteria | Linked to done conditions |

### STEP 3 — Non-Functional Requirements (NFR)

| NFR Category | Applicable When |
|---|---|
| Performance | Always |
| Security | Web/app + external users |
| Scalability / Availability | Production deployment |
| Usability | Has UI |
| Maintainability | Always |

### STEP 4 — User Flows

| Project Type | Flow Format |
|---|---|
| WebApp | Page navigation flow |
| Data Pipeline | Data flow (source -> transform -> load) |
| AI Project | Inference flow (input -> model -> output) |
| CLI Tool | Command execution flow |
| Automation | Trigger -> execute -> result flow |

### Section 9 Format

```markdown
## 9. Requirements

### 9-1. Functional Requirements

| ID | Feature | Description | Input | Output | Priority | Acceptance Criteria |
|---|---|---|---|---|---|---|
| FR-001 | ... | ... | ... | ... | Mandatory | ... |

### 9-2. Non-Functional Requirements

| ID | Category | Requirement | Criteria |
|---|---|---|---|
| NFR-001 | Performance | ... | ... |

### 9-3. User Flows

#### Flow 1: [Scenario Name]
[Format matching project type]

### 9-4. Constraints and Assumptions
```

---

## 2. design-architecture

### Prerequisites

1. Kickoff document section 9 (requirements) exists
2. YAML frontmatter `last_skill` = `design-requirements`

### STEP Structure

| STEP | Description | Output |
|---|---|---|
| STEP 1 | Analyze kickoff doc (sections 1-9) | Architecture decision input |
| STEP 2 | System diagram (text) | System structure draft |
| STEP 3 | Tech selection rationale per layer | Tech decision table |
| STEP 4 | Deployment structure (conditional by purpose) | Deployment plan |
| STEP 5 | Additional interview (gaps only) | Supplemented architecture |
| STEP 6 | Present + confirm -> add section 10 to kickoff doc | `last_skill` updated |

### STEP 2 — System Diagram

```
[User] -> [Frontend] -> [API Server] -> [DB]
                                    \-> [External API]
```

### STEP 3 — Tech Selection Rationale

- If rationale already exists from kickoff interview, inherit as-is
- If missing, AI provides rationale based on type/scale/NFR

### STEP 4 — Deployment Structure (Conditional)

| Condition | Included Content |
|---|---|
| Production | Deployment environment, CI/CD, monitoring, logging |
| Portfolio | Deployment method (brief), demo environment |
| Study | Local execution environment only |

### Type Overrides

| Project Type | Architecture Pattern | Key Components |
|---|---|---|
| WebApp | Frontend/backend split | Router, state management, API layer, auth |
| Data Pipeline | DAG-based, ETL/ELT | Connectors, transformers, scheduler, storage |
| AI Project | Serving/training split | Preprocessing, model server, postprocessing, feedback loop |
| CLI Tool | Modular command pattern | Parser, handlers, output formatter, config loader |
| Automation | Event-driven / scheduled | Trigger, task runner, notification, logger |
| BI Dashboard | Data source -> visualization | Connector, cache, chart engine, filters |

### Section 10 Format

```markdown
## 10. System Architecture

### 10-1. System Structure
[Text diagram]

#### Component Description
| Component | Role | Technology | Communication |
|---|---|---|---|

### 10-2. Tech Selection
| Layer | Technology | Rationale | Alternatives & Rejection Reason |
|---|---|---|---|

### 10-3. Deployment Structure (if applicable)

### 10-4. Cross-cutting Concerns
- Auth, error handling, logging, config management

### 10-5. Architecture Decision Records (ADR)
| # | Decision | Rationale | Alternatives |
|---|---|---|---|
```

---

## Cross-Section Edit Rule

If architecture reveals a requirements gap:

1. Ask user: "Section 9 [item] needs modification. Proceed?"
2. **Agree** -> Edit section 9 + record in Revision History
3. **Decline** -> Note in section 10: "Note: Section 9 [item] requires review regarding [content]"

---

## Common Design Principles

- **Gap-only interviews**: Only ask about what is missing from kickoff (bundled questions, "don't know/recommend" allowed, no re-asking)
- **80/20 type adaptation**: 80% common template + 20% type override — complex types get primary type + secondary type sections
- **Scale-proportionate**: No heavy NFR/infrastructure for study-level projects
- **Extend kickoff data**: Inherit feature classification (mandatory/optional), tech stack, existing architecture — do not recreate
- **"Undecided" resolution**: Handled only in design-requirements prerequisites (not needed in later skills)

---

## Verification

1. Completed kickoff project -> sections 9 + 10 correctly added
2. "Undecided" tech stack -> forced resolution before proceeding
3. WebApp -> security NFR + frontend/backend structure included
4. Study project -> no heavy infrastructure/NFR
5. Re-run -> existing section edited (not duplicated) + Revision History recorded
6. Architecture reveals requirements gap -> user confirmation flow works

---

## Implementation Files

### design-requirements skill
- `.claude/skills/design-requirements/SKILL.md` — 7 STEP skill (analyze → FR → NFR → flows → gap interview → confirm → file update)
- `.claude/skills/design-requirements/references/requirements-template.md` — FR/NFR/flow generation guide with 7 type overrides
- `.claude/skills/design-requirements/references/nfr-checklist.md` — 7 NFR categories with conditional activation rules

### design-architecture skill
- `.claude/skills/design-architecture/SKILL.md` — 7 STEP skill (analyze → system diagram → tech rationale → deployment → interview → confirm → file update)
- `.claude/skills/design-architecture/references/architecture-template.md` — Section 10 structure guide, deployment activation rules
- `.claude/skills/design-architecture/references/architecture-patterns.md` — Type-specific architecture patterns catalog + ADR template

### Modified files
- `.claude/skills/kickoff-profile/references/profile-template.md` — Added section 9-13 placeholders + Revision History table + writing rule 9
- `.claude/skills/kickoff-skills/SKILL.md` — Added v2 design transition prompt (5 design skills table + proceed/skip choice) in STEP 4

---

## Change Log

| Date | Description |
|---|---|
| 2026-05-12 | Initial creation |
| 2026-05-12 | All 8 deliverables completed (6 new + 2 modified) |

---
---

# Phase 11 — DesignRequirementsArchitecture `완료`

> 킥오프 문서에 요구사항 명세(섹션 9)와 시스템 아키텍처(섹션 10)를 추가하는 스킬 2종 개발

**완료일**: 2026-05-12
**상태**: ✅ 완료
**선행 조건**: Phase 10 완료
**버전**: v2

---

## 개요

킥오프 문서(What+Why)에서 설계(How)로 전환하는 상위 설계 단계. 두 스킬이 킥오프 문서(`_kickoff.md`)에 섹션을 이어서 추가한다:
- **design-requirements** (섹션 9): 핵심 기능을 상세 분해하고, 비기능 요구사항과 사용자 플로우를 정의
- **design-architecture** (섹션 10): 요구사항을 구현할 시스템 구조, 기술 선택 이유, 컴포넌트 구성을 정의

design-requirements는 v2 설계 체인의 진입점이므로, "미정" 기술 스택 강제 해소와 킥오프 완료 여부 검증을 이 스킬에서 처리한다.

---

## 산출물 규칙 (v2 공통)

| 항목 | 결정 |
|---|---|
| 산출물 위치 | `_kickoff.md`에 섹션 추가 (별도 파일 없음) |
| 생성 방식 | 첫 실행 시 섹션 추가, 재실행 시 기존 섹션 Edit |
| 변경 이력 | 문서 하단 Revision History 테이블 |
| 후속 스킬의 이전 섹션 수정 | 사용자 확인 후 Edit, 또는 현재 섹션에 명시만 |
| 진행 추적 | YAML frontmatter `last_skill` 갱신 |

---

## 완료 예정 항목

| # | Skill / 모듈 | 상태 | 비고 |
|---|---|---|---|
| 1 | `design-requirements` SKILL.md | ✅ | 7 STEP, depends_on: kickoff-done |
| 2 | `references/requirements-template.md` | ✅ | FR/NFR/흐름 규칙, 7개 유형 오버라이드 |
| 3 | `references/nfr-checklist.md` | ✅ | 7개 NFR 카테고리, 조건부 활성화 |
| 4 | `design-architecture` SKILL.md | ✅ | 7 STEP, depends_on: design-requirements |
| 5 | `references/architecture-template.md` | ✅ | 섹션 10 구조, 배포 활성화 규칙 |
| 6 | `references/architecture-patterns.md` | ✅ | 유형별 아키텍처 패턴, ADR 템플릿 |
| 7 | `profile-template.md` (수정) | ✅ | 섹션 9-13 플레이스홀더 + Revision History |
| 8 | `kickoff-skills/SKILL.md` (수정) | ✅ | STEP 4에 v2 설계 전환 프롬프트 |

---

## 1. design-requirements 설계

### 사전 조건

1. 킥오프 문서 존재 (`**/*_kickoff.md` Glob)
2. YAML frontmatter `last_skill` >= `kickoff-done`
3. **"미정" 기술 스택 강제 해소**: `### 기술 스택`에 "미정"이 있으면 확정 요청
   - "모름/추천해줘" 허용 -> AI가 유형+목적 기반 추천 + 사유 제시
   - 확정 후 킥오프 문서에 반영(Edit) -> STEP 1 진행

### STEP 구조

| STEP | 내용 | 산출물 |
|---|---|---|
| STEP 1 | 킥오프 문서 분석 + 프로젝트 유형 확인 | 요구사항 추출 입력 |
| STEP 2 | 기능 요구사항 정리 (핵심 기능 -> 상세 분해) | 기능 목록 초안 (FR-001...) |
| STEP 3 | 비기능 요구사항 도출 (유형+목적 기반) | NFR 목록 |
| STEP 4 | 사용자 플로우 작성 (핵심 시나리오 2~5개) | 사용자 플로우 |
| STEP 5 | 추가 인터뷰 (부족한 부분만) | 보완된 요구사항 |
| STEP 6 | 결과 제시 + 사용자 확인 -> 킥오프 문서 섹션 9 추가 | `last_skill` 갱신 |

### STEP 1 — 킥오프 문서 분석

| 읽을 섹션 | 추출 대상 |
|---|---|
| 기본 정보 -> 유형 | 유형별 템플릿 선택 |
| 핵심 기능 테이블 | 기능 목록 + 필수/선택 분류 |
| 기술 스택 | 구현 제약사항 |
| 제약사항/리스크 | NFR 후보 |
| 프로젝트 배경 (context) | 목적, 수준, 시간 예산 |
| 채택된 AI 제안 | 추가 기능 후보 |
| 완료 조건 (done) | 수용 기준 연계 |

### STEP 2 — 기능 요구사항 정리

| 항목 | 설명 |
|---|---|
| 기능 ID | FR-001, FR-002, ... |
| 기능명 | 킥오프 문서의 기능명 계승 |
| 상세 설명 | 1~2문장 |
| 입력 / 출력 | 데이터 흐름 |
| 우선순위 | 필수(MVP) / 선택(v2+) — 킥오프 분류 계승 |
| 수용 기준 | done 조건과 연계 |

### STEP 3 — 비기능 요구사항 (NFR)

| NFR 카테고리 | 적용 조건 |
|---|---|
| 성능 | 항상 |
| 보안 | 웹/앱 + 외부 사용자 |
| 확장성 / 가용성 | 실무 투입 |
| 사용성 | UI가 있는 경우 |
| 유지보수성 | 항상 |

### STEP 4 — 사용자 플로우

| 프로젝트 유형 | 플로우 형식 |
|---|---|
| 웹앱 | 페이지 이동 흐름 |
| 데이터 파이프라인 | 데이터 흐름 (소스 -> 변환 -> 적재) |
| AI 프로젝트 | 추론 흐름 (입력 -> 모델 -> 출력) |
| CLI 도구 | 커맨드 실행 흐름 |
| 자동화 | 트리거 -> 실행 -> 결과 흐름 |

### 킥오프 문서 섹션 9 형식

```markdown
## 9. 요구사항 명세 (Requirements)

### 9-1. 기능 요구사항

| ID | 기능명 | 상세 설명 | 입력 | 출력 | 우선순위 | 수용 기준 |
|---|---|---|---|---|---|---|
| FR-001 | ... | ... | ... | ... | 필수 | ... |

### 9-2. 비기능 요구사항

| ID | 카테고리 | 요구사항 | 기준 |
|---|---|---|---|
| NFR-001 | 성능 | ... | ... |

### 9-3. 사용자 플로우

#### 플로우 1: [시나리오명]
[유형에 맞는 형식]

### 9-4. 제약사항 및 전제조건
```

---

## 2. design-architecture 설계

### 사전 조건

1. 킥오프 문서 섹션 9(요구사항) 존재 확인
2. YAML frontmatter `last_skill` = `design-requirements`

### STEP 구조

| STEP | 내용 | 산출물 |
|---|---|---|
| STEP 1 | 킥오프 문서 전체 분석 (섹션 1~9) | 아키텍처 결정 입력 |
| STEP 2 | 시스템 구조도 작성 (텍스트 다이어그램) | 시스템 구조 초안 |
| STEP 3 | 기술 선택 이유 정리 (레이어별) | 기술 결정 표 |
| STEP 4 | 배포/인프라 구조 (목적에 따라 상세도 조절) | 배포 구조 |
| STEP 5 | 추가 인터뷰 (부족한 부분만) | 보완된 아키텍처 |
| STEP 6 | 결과 제시 + 사용자 확인 -> 킥오프 문서 섹션 10 추가 | `last_skill` 갱신 |

### STEP 2 — 시스템 구조도

```
[사용자] -> [프론트엔드] -> [API 서버] -> [DB]
                                    \-> [외부 API]
```

### STEP 3 — 기술 선택 이유

- 킥오프 인터뷰에서 이미 사유가 있으면 그대로 가져옴
- 없으면 유형/규모/NFR 기반으로 AI가 사유 제시

### STEP 4 — 배포 구조 (조건부)

| 조건 | 포함 내용 |
|---|---|
| 실무 투입 | 배포 환경, CI/CD, 모니터링, 로깅 |
| 포트폴리오 | 배포 방법 (간단히), 데모 환경 |
| 학습용 | 로컬 실행 환경만 |

### 유형별 오버라이드

| 프로젝트 유형 | 아키텍처 패턴 | 핵심 컴포넌트 |
|---|---|---|
| 웹앱 | 프론트/백엔드 분리 | 라우터, 상태관리, API 레이어, 인증 |
| 데이터 파이프라인 | DAG 기반, ETL/ELT | 커넥터, 트랜스포머, 스케줄러, 저장소 |
| AI 프로젝트 | 서빙/학습 분리 | 전처리, 모델 서버, 후처리, 피드백 루프 |
| CLI 도구 | 모듈러 커맨드 패턴 | 파서, 핸들러, 출력 포매터, 설정 로더 |
| 자동화 | 이벤트 드리븐 / 스케줄 | 트리거, 태스크 러너, 알림, 로거 |
| BI 대시보드 | 데이터 소스 -> 시각화 | 커넥터, 캐시, 차트 엔진, 필터 |

### 킥오프 문서 섹션 10 형식

```markdown
## 10. 시스템 아키텍처 (Architecture)

### 10-1. 시스템 구조
[텍스트 다이어그램]

#### 컴포넌트 설명
| 컴포넌트 | 역할 | 기술 | 통신 방식 |
|---|---|---|---|

### 10-2. 기술 선택
| 레이어 | 기술 | 선택 이유 | 대안 및 기각 사유 |
|---|---|---|---|

### 10-3. 배포 구조 (해당 시)

### 10-4. 횡단 관심사
- 인증/인가, 에러 핸들링, 로깅, 설정 관리

### 10-5. 아키텍처 결정 기록 (ADR)
| # | 결정 | 이유 | 대안 |
|---|---|---|---|
```

---

## 후속 스킬의 이전 섹션 수정 규칙

architecture 작성 중 requirements에 누락/수정이 필요한 경우:

1. 사용자에게 "섹션 9의 [항목]을 수정해야 합니다. 수정할까요?" 확인
2. **동의** -> 섹션 9 해당 부분 Edit + Revision History에 기록
3. **거부** -> 섹션 10에 "참고: 섹션 9의 [항목]에 대해 [내용] 검토 필요" 명시

---

## 공통 설계 원칙

- **추가 인터뷰**: 킥오프에서 부족한 부분만 (묶음 질문, "모름/추천" 허용, 재질문 금지)
- **유형 적응**: 공통 템플릿 80% + 유형별 오버라이드 20% — 복합 유형은 주 유형 + 부가 유형 섹션
- **규모 비례**: 학습용 소규모 프로젝트에 과도한 NFR/인프라 부과 금지
- **킥오프 계승**: 기능 분류(필수/선택), 기술 스택, 기존 아키텍처를 확장 — 새로 만들지 않음
- **"미정" 해소**: design-requirements 사전 조건에서만 처리 (이후 스킬 불필요)

---

## 검증 방법

1. 킥오프 완료 프로젝트 -> 섹션 9, 10 정상 추가 확인
2. "미정" 기술 스택 -> 확정 요청 후 진행 확인
3. 웹앱 -> 보안 NFR + 프론트/백엔드 구조 포함 확인
4. 학습용 -> 과도한 인프라/NFR 미포함 확인
5. 재실행 -> 기존 섹션 Edit + Revision History 기록 확인
6. architecture에서 requirements 수정 필요 시 -> 사용자 확인 흐름 확인

---

## 구현 파일

### design-requirements 스킬
- `.claude/skills/design-requirements/SKILL.md` — 7 STEP (분석 → FR → NFR → 흐름 → 갭 인터뷰 → 확인 → 파일 갱신)
- `.claude/skills/design-requirements/references/requirements-template.md` — FR/NFR/흐름 생성 가이드, 7개 유형 오버라이드
- `.claude/skills/design-requirements/references/nfr-checklist.md` — 7개 NFR 카테고리, 조건부 활성화 규칙

### design-architecture 스킬
- `.claude/skills/design-architecture/SKILL.md` — 7 STEP (분석 → 시스템 구조 → 기술 근거 → 배포 → 인터뷰 → 확인 → 파일 갱신)
- `.claude/skills/design-architecture/references/architecture-template.md` — 섹션 10 구조 가이드, 배포 활성화 규칙
- `.claude/skills/design-architecture/references/architecture-patterns.md` — 유형별 아키텍처 패턴 카탈로그 + ADR 템플릿

### 수정 파일
- `.claude/skills/kickoff-profile/references/profile-template.md` — 섹션 9-13 플레이스홀더 + Revision History 테이블 + 작성 규칙 9 추가
- `.claude/skills/kickoff-skills/SKILL.md` — STEP 4에 v2 설계 전환 프롬프트 (설계 스킬 5종 테이블 + 진행/스킵 선택)

---

## 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026-05-12 | 최초 작성 |
| 2026-05-12 | 전체 산출물 완료 (신규 6개 + 수정 2개) |
