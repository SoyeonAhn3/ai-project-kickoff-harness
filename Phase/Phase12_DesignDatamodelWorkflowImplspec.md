# Phase 12 — DesignDatamodelWorkflowImplspec `Completed`

> Data model (section 11), AI workflow (section 12, conditional), and implementation spec (section 13) design skills

**Completed**: 2026-05-12
**Status**: ✅ Completed
**Prerequisites**: Phase 11 complete
**Version**: v2

---

## Overview

Detail design phase building on Phase 11's upper design. Three skills adding sections to `_kickoff.md`:
- **design-data-model** (section 11): Entities/schemas, relationships, integrity rules, API contracts
- **design-ai-workflow** (section 12): AI I/O, prompts, model selection, fallback — AI projects ONLY
- **design-impl-spec** (section 13): Implementation units, file structure, key components, Phase overview

All follow the same deliverable rules as Phase 11, adding sections to `_kickoff.md`.

---

## Deliverables

| # | Skill / Module | Status | Notes |
|---|---|---|---|
| 1 | `design-data-model` SKILL.md | ✅ | 8 STEPs, depends_on: design-architecture |
| 2 | `references/data-model-template.md` | ✅ | Entity/relationship/lifecycle rules, 7 type overrides |
| 3 | `design-ai-workflow` SKILL.md | ✅ | 9 STEPs (incl. STEP 0 activation check), conditional |
| 4 | `references/ai-workflow-template.md` | ✅ | 4 AI patterns (LLM/RAG/custom/agent), prompt principles |
| 5 | `design-impl-spec` SKILL.md | ✅ | 9 STEPs, v2 final skill with design summary |
| 6 | `references/impl-spec-template.md` | ✅ | Project structure + Phase planning rules, 7 type overrides |

---

## 1. design-data-model

### Prerequisites

1. Kickoff document section 10 (architecture) exists
2. YAML frontmatter `last_skill` = `design-architecture`

### STEP Structure

| STEP | Description | Output |
|---|---|---|
| STEP 1 | Analyze kickoff doc (sections 1-10) | Data model input |
| STEP 2 | Define core entities/schemas | Data structure draft |
| STEP 3 | Define relationships + integrity rules | Relationship diagram + constraints |
| STEP 4 | API contracts / I/O spec (conditional) | Interface definitions |
| STEP 5 | Additional interview (gaps only) | Supplemented data model |
| STEP 6 | Present + confirm -> add section 11 to kickoff doc | `last_skill` updated |

### Type-Specific Data Model Formats

| Project Type | Definition Format | Key Inclusions |
|---|---|---|
| WebApp | DB table schemas | Columns, types, constraints, API contracts |
| Data Pipeline | Source -> transform -> output schemas | Lineage, transformation rules |
| AI Project | Training data + features + model I/O | Data quality criteria |
| CLI Tool | Config file format + I/O structure | YAML/JSON schemas |
| Automation | Event payload + state data | Log structure |
| BI Dashboard | Data source + aggregation tables | Cache structure, refresh rules |

### Section 11 Format

```markdown
## 11. Data Model

### 11-1. Entity/Schema Definition

#### [Entity Name]
| Field | Type | Constraints | Description |
|---|---|---|---|

### 11-2. Relationship Diagram
[Text ERD or relationship description]

### 11-3. Integrity Rules
| Rule | Target | Description |
|---|---|---|

### 11-4. API Contract / I/O Spec (if applicable)

### 11-5. Data Flow (if applicable)
[Source -> Transform -> Output lineage]
```

---

## 2. design-ai-workflow

### Conditional Activation

| Type | Behavior |
|---|---|
| AI as primary type | Full generation (section 12) |
| AI as secondary type | Reduced generation (core only) |
| No AI type | **SKIP** -> proceed to design-impl-spec |

### Prerequisites

1. Kickoff document section 11 (data model) exists
2. YAML frontmatter `last_skill` = `design-data-model`
3. Project type includes "AI"

### STEP Structure

| STEP | Description | Output |
|---|---|---|
| STEP 1 | Analyze kickoff doc (focus on AI-related sections) | AI workflow input |
| STEP 2 | Define AI pipeline (input -> preprocess -> model -> postprocess -> output) | Pipeline draft |
| STEP 3 | Prompt/model design (LLM) or training design (ML) | Model design |
| STEP 4 | Fallback + error handling | Failure scenarios |
| STEP 5 | Additional interview (gaps only) | Supplemented workflow |
| STEP 6 | Present + confirm -> add section 12 to kickoff doc | `last_skill` updated |

### Section 12 Format

```markdown
## 12. AI Workflow

### 12-1. AI Pipeline
[Input -> Preprocessing -> Model -> Postprocessing -> Output]

### 12-2. Model/Prompt Design
| Item | Content |
|---|---|
| Model | [Model name/type] |
| Input Format | ... |
| Output Format | ... |
| Prompt Strategy (LLM) | ... |
| Training Data (ML) | ... |

### 12-3. Cost/Performance Estimate
| Item | Estimate |
|---|---|

### 12-4. Fallback and Error Handling
| Failure Type | Fallback Strategy |
|---|---|
```

---

## 3. design-impl-spec

### Prerequisites

1. Previous skill completion check:
   - AI project: `last_skill` = `design-ai-workflow`
   - Non-AI project: `last_skill` = `design-data-model`
2. Kickoff document sections 9-11 (+12 if AI) exist

### STEP Structure

| STEP | Description | Output |
|---|---|---|
| STEP 1 | Analyze full kickoff doc (sections 1-12) | Implementation spec input |
| STEP 2 | Define file/module structure | Directory tree |
| STEP 3 | Key component details (props/behavior level) | Component specs |
| STEP 4 | Phase overview (implementation order + dependencies) | Phase plan |
| STEP 5 | Additional interview (gaps only) | Supplemented spec |
| STEP 6 | Present + confirm -> add section 13 to kickoff doc | `last_skill` updated |

### STEP 3 — Component Detail Levels

| Category | Detail Level |
|---|---|
| Core components | Props/interface, behavior flow, dependencies — full detail |
| Supporting components | Role and interface only |

### STEP 4 — impl-spec vs phase-doc Role Separation

| | impl-spec (this skill) | phase-doc (skill package) |
|---|---|---|
| Scope | Per-Phase implementation scope + dependency overview | Per-Phase detailed tasks, checklist, tests |
| Timing | Design stage | Development stage |
| Role | "What to build in what order" (design -> code bridge) | "Exactly what to do this Phase" (code -> execution bridge) |

### Type-Specific Implementation Units

| Project Type | Decomposition Basis |
|---|---|
| WebApp | Components / pages |
| Data Pipeline | Jobs / connectors |
| AI Project | Training / inference / evaluation |
| CLI Tool | Commands / handlers |
| Automation | Tasks / triggers |

### Section 13 Format

```markdown
## 13. Implementation Spec

### 13-1. File/Module Structure
```
{project-name}/
├── src/
│   ├── ...
├── tests/
└── ...
```

### 13-2. Key Component Details

#### [Component Name]
- Role: ...
- Interface: ...
- Behavior Flow: ...
- Dependencies: ...

### 13-3. Phase Overview

| Phase | Implementation Scope | Dependencies | Deliverables |
|---|---|---|---|
| 1 | ... | - | ... |
| 2 | ... | Phase 1 | ... |
```

---

## Cross-Section Edit Rule

Same as Phase 11:
1. Ask user: "Section N [item] needs modification. Proceed?"
2. **Agree** -> Edit target section + record in Revision History
3. **Decline** -> Note in current section: "Note: Section N [item] requires review regarding [content]"

---

## last_skill Chaining

```
AI projects:     requirements -> architecture -> data-model -> ai-workflow -> impl-spec
Non-AI projects: requirements -> architecture -> data-model -> impl-spec (skip ai-workflow)
```

impl-spec prerequisites:
- Always `last_skill` = `design-ai-workflow` (non-AI projects auto-skip with frontmatter updated)

---

## Verification

1. WebApp project -> section 11 (DB schema + API contract) + section 13 (component/page-based) confirmed
2. AI project -> section 12 (AI workflow) automatically included
3. Non-AI project -> section 12 skipped + impl-spec follows directly after data-model
4. AI as secondary type -> section 12 reduced generation
5. Re-run -> existing section edited (not duplicated) + Revision History recorded
6. Cross-section edit needed -> user confirmation flow works

---

## Implementation Files

### design-data-model skill
- `.claude/skills/design-data-model/SKILL.md` — 8 STEP skill (analyze → entities → relationships → lifecycle → migration → interview → confirm → file update)
- `.claude/skills/design-data-model/references/data-model-template.md` — Entity/relationship/lifecycle/migration rules, 7 type overrides

### design-ai-workflow skill
- `.claude/skills/design-ai-workflow/SKILL.md` — 9 STEP skill (STEP 0 activation → analyze → AI I/O → prompts → model selection → fallback → evaluation → interview → file update)
- `.claude/skills/design-ai-workflow/references/ai-workflow-template.md` — 4 AI workflow patterns (LLM, RAG, custom model, agent), prompt design principles, cost estimation guide

### design-impl-spec skill
- `.claude/skills/design-impl-spec/SKILL.md` — 9 STEP skill (analyze → project structure → components → dependencies → config → Phase plan → interview → confirm → file update)
- `.claude/skills/design-impl-spec/references/impl-spec-template.md` — Project structure templates (7 types), component detail rules, Phase planning rules

---

## Change Log

| Date | Description |
|---|---|
| 2026-05-12 | Initial creation |
| 2026-05-12 | All 6 deliverables completed (3 SKILL.md + 3 reference templates) |

---
---

# Phase 12 — DesignDatamodelWorkflowImplspec `완료`

> 킥오프 문서에 데이터 모델(섹션 11), AI 워크플로우(섹션 12, 조건부), 구현 명세(섹션 13)를 추가하는 스킬 3종 개발

**완료일**: 2026-05-12
**상태**: ✅ 완료
**선행 조건**: Phase 11 완료
**버전**: v2

---

## 개요

Phase 11의 상위 설계(요구사항+아키텍처)를 기반으로, 구현에 필요한 상세 설계를 정의하는 단계:
- **design-data-model** (섹션 11): 엔티티/스키마, 관계, 정합성 규칙, API 계약
- **design-ai-workflow** (섹션 12): AI 입출력, 프롬프트, 모델 선택, 폴백 — **AI 유형 프로젝트만 생성**
- **design-impl-spec** (섹션 13): 구현 단위 분해, 파일 구조, 핵심 컴포넌트 상세, Phase 개요

모두 `_kickoff.md`에 섹션을 이어서 추가하며, Phase 11과 동일한 산출물 규칙을 따른다.

---

## 완료 예정 항목

| # | Skill / 모듈 | 상태 | 비고 |
|---|---|---|---|
| 1 | `design-data-model` SKILL.md | ✅ | 8 STEP, depends_on: design-architecture |
| 2 | `references/data-model-template.md` | ✅ | 엔티티/관계/생명주기 규칙, 7개 유형 오버라이드 |
| 3 | `design-ai-workflow` SKILL.md | ✅ | 9 STEP (STEP 0 활성화 판정 포함), 조건부 |
| 4 | `references/ai-workflow-template.md` | ✅ | 4개 AI 패턴 (LLM/RAG/커스텀/에이전트), 프롬프트 원칙 |
| 5 | `design-impl-spec` SKILL.md | ✅ | 9 STEP, v2 마지막 스킬 (설계 요약 출력) |
| 6 | `references/impl-spec-template.md` | ✅ | 프로젝트 구조 + Phase 계획 규칙, 7개 유형 오버라이드 |

---

## 1. design-data-model 설계

### 사전 조건

1. 킥오프 문서 섹션 10(아키텍처) 존재 확인
2. YAML frontmatter `last_skill` = `design-architecture`

### STEP 구조

| STEP | 내용 | 산출물 |
|---|---|---|
| STEP 1 | 킥오프 문서 분석 (섹션 1~10) | 데이터 모델 입력 |
| STEP 2 | 핵심 엔티티/스키마 정의 | 데이터 구조 초안 |
| STEP 3 | 관계 및 정합성 규칙 정의 | 관계도 + 제약조건 |
| STEP 4 | API 계약 / I/O 명세 (해당 시) | 인터페이스 정의 |
| STEP 5 | 추가 인터뷰 (부족한 부분만) | 보완된 데이터 모델 |
| STEP 6 | 결과 제시 + 사용자 확인 -> 킥오프 문서 섹션 11 추가 | `last_skill` 갱신 |

### 유형별 데이터 모델 형식

| 프로젝트 유형 | 정의 형식 | 핵심 포함 사항 |
|---|---|---|
| 웹앱 | DB 테이블 스키마 | 컬럼, 타입, 제약조건, API 계약 |
| 데이터 파이프라인 | 소스 -> 변환 -> 출력 스키마 | 리니지, 변환 규칙 |
| AI 프로젝트 | 학습 데이터 + 피처 + 모델 I/O | 데이터 품질 기준 |
| CLI 도구 | 설정 파일 포맷 + I/O 구조 | YAML/JSON 스키마 |
| 자동화 | 이벤트 페이로드 + 상태 데이터 | 로그 구조 |
| BI 대시보드 | 데이터 소스 + 집계 테이블 | 캐시 구조, 갱신 규칙 |

### 킥오프 문서 섹션 11 형식

```markdown
## 11. 데이터 모델 (Data Model)

### 11-1. 엔티티/스키마 정의

#### [엔티티명]
| 필드 | 타입 | 제약조건 | 설명 |
|---|---|---|---|

### 11-2. 관계도
[텍스트 ERD 또는 관계 설명]

### 11-3. 정합성 규칙
| 규칙 | 대상 | 설명 |
|---|---|---|

### 11-4. API 계약 / I/O 명세 (해당 시)

### 11-5. 데이터 흐름 (해당 시)
[소스 -> 변환 -> 출력 리니지]
```

---

## 2. design-ai-workflow 설계

### 조건부 활성화

| 유형 | 동작 |
|---|---|
| AI가 주 유형 | 전체 생성 (섹션 12) |
| AI가 부가 유형 | 축소 생성 (핵심만) |
| AI 유형 아님 | **건너뜀** -> design-impl-spec으로 직행 |

### 사전 조건

1. 킥오프 문서 섹션 11(데이터 모델) 존재 확인
2. YAML frontmatter `last_skill` = `design-data-model`
3. 프로젝트 유형에 "AI" 포함 여부 확인

### STEP 구조

| STEP | 내용 | 산출물 |
|---|---|---|
| STEP 1 | 킥오프 문서 분석 (AI 관련 섹션 집중) | AI 워크플로우 입력 |
| STEP 2 | AI 파이프라인 정의 (입력 -> 전처리 -> 모델 -> 후처리 -> 출력) | 파이프라인 초안 |
| STEP 3 | 프롬프트/모델 설계 (LLM) 또는 학습 설계 (ML) | 모델 설계 |
| STEP 4 | 폴백 및 에러 처리 | 실패 시나리오 |
| STEP 5 | 추가 인터뷰 (부족한 부분만) | 보완된 워크플로우 |
| STEP 6 | 결과 제시 + 사용자 확인 -> 킥오프 문서 섹션 12 추가 | `last_skill` 갱신 |

### 킥오프 문서 섹션 12 형식

```markdown
## 12. AI 워크플로우 (AI Workflow)

### 12-1. AI 파이프라인
[입력 -> 전처리 -> 모델 -> 후처리 -> 출력]

### 12-2. 모델/프롬프트 설계
| 항목 | 내용 |
|---|---|
| 모델 | [모델명/종류] |
| 입력 형식 | ... |
| 출력 형식 | ... |
| 프롬프트 전략 (LLM) | ... |
| 학습 데이터 (ML) | ... |

### 12-3. 비용/성능 추정
| 항목 | 추정치 |
|---|---|

### 12-4. 폴백 및 에러 처리
| 실패 유형 | 폴백 전략 |
|---|---|
```

---

## 3. design-impl-spec 설계

### 사전 조건

1. 이전 스킬 완료 확인:
   - AI 프로젝트: `last_skill` = `design-ai-workflow`
   - 비AI 프로젝트: `last_skill` = `design-data-model`
2. 킥오프 문서 섹션 9~11(+12) 존재 확인

### STEP 구조

| STEP | 내용 | 산출물 |
|---|---|---|
| STEP 1 | 킥오프 문서 전체 분석 (섹션 1~12) | 구현 명세 입력 |
| STEP 2 | 파일/모듈 구조 정의 | 디렉토리 트리 |
| STEP 3 | 핵심 컴포넌트 상세 (props/동작 수준) | 컴포넌트 명세 |
| STEP 4 | Phase 개요 (구현 순서 + 의존성) | Phase 계획 |
| STEP 5 | 추가 인터뷰 (부족한 부분만) | 보완된 명세 |
| STEP 6 | 결과 제시 + 사용자 확인 -> 킥오프 문서 섹션 13 추가 | `last_skill` 갱신 |

### STEP 3 — 컴포넌트 상세 구분

| 구분 | 상세 수준 |
|---|---|
| 핵심 컴포넌트 | props/인터페이스, 동작 흐름, 의존성까지 상세 |
| 보조 컴포넌트 | 역할과 인터페이스만 정의 |

### STEP 4 — impl-spec과 phase-doc 역할 분리

| | impl-spec (이 스킬) | phase-doc (스킬 패키지) |
|---|---|---|
| 범위 | Phase별 구현 범위 + 의존성 개요 | Phase별 상세 작업, 체크리스트, 테스트 |
| 시점 | 설계 단계 | 개발 단계 |
| 역할 | "뭘 어떤 순서로 만들지" (설계 -> 코드 브릿지) | "이번 Phase에서 정확히 뭘 해야 하는지" (코드 -> 실행 브릿지) |

### 유형별 구현 단위

| 프로젝트 유형 | 분해 기준 |
|---|---|
| 웹앱 | 컴포넌트/페이지별 |
| 데이터 파이프라인 | 잡/커넥터별 |
| AI 프로젝트 | 학습/추론/평가별 |
| CLI 도구 | 커맨드/핸들러별 |
| 자동화 | 태스크/트리거별 |

### 킥오프 문서 섹션 13 형식

```markdown
## 13. 구현 명세 (Implementation Spec)

### 13-1. 파일/모듈 구조
```
{프로젝트명}/
├── src/
│   ├── ...
├── tests/
└── ...
```

### 13-2. 핵심 컴포넌트 상세

#### [컴포넌트명]
- 역할: ...
- 인터페이스: ...
- 동작 흐름: ...
- 의존성: ...

### 13-3. Phase 개요

| Phase | 구현 범위 | 의존성 | 산출물 |
|---|---|---|---|
| 1 | ... | - | ... |
| 2 | ... | Phase 1 | ... |
```

---

## 후속 스킬의 이전 섹션 수정 규칙

Phase 11과 동일:
1. 사용자에게 "섹션 N의 [항목]을 수정해야 합니다. 수정할까요?" 확인
2. **동의** -> 해당 섹션 Edit + Revision History에 기록
3. **거부** -> 현재 섹션에 "참고: 섹션 N의 [항목]에 대해 [내용] 검토 필요" 명시

---

## last_skill 체이닝 분기

```
AI 프로젝트:     requirements -> architecture -> data-model -> ai-workflow -> impl-spec
비AI 프로젝트:   requirements -> architecture -> data-model -> impl-spec (ai-workflow 건너뜀)
```

impl-spec의 사전 조건:
- 항상 `last_skill` = `design-ai-workflow` (비AI도 스킵 처리로 frontmatter 갱신됨)

---

## 검증 방법

1. 웹앱 프로젝트 -> 섹션 11(DB 스키마 + API 계약) + 섹션 13(컴포넌트/페이지별) 확인
2. AI 프로젝트 -> 섹션 12(AI 워크플로우) 자동 포함 확인
3. 비AI 프로젝트 -> 섹션 12 건너뜀 + impl-spec이 data-model 직후 확인
4. AI 부가 유형 -> 섹션 12 축소 생성 확인
5. 재실행 -> 기존 섹션 Edit + Revision History 기록 확인
6. 이전 섹션 수정 필요 시 -> 사용자 확인 흐름 확인

---

## 구현 파일

### design-data-model 스킬
- `.claude/skills/design-data-model/SKILL.md` — 8 STEP (분석 → 엔티티 → 관계 → 생명주기 → 마이그레이션 → 인터뷰 → 확인 → 파일 갱신)
- `.claude/skills/design-data-model/references/data-model-template.md` — 엔티티/관계/생명주기/마이그레이션 규칙, 7개 유형 오버라이드

### design-ai-workflow 스킬
- `.claude/skills/design-ai-workflow/SKILL.md` — 9 STEP (STEP 0 활성화 → 분석 → AI I/O → 프롬프트 → 모델 선택 → 폴백 → 평가 → 인터뷰 → 파일 갱신)
- `.claude/skills/design-ai-workflow/references/ai-workflow-template.md` — 4개 AI 워크플로우 패턴 (LLM, RAG, 커스텀, 에이전트), 프롬프트 설계 원칙, 비용 추정 가이드

### design-impl-spec 스킬
- `.claude/skills/design-impl-spec/SKILL.md` — 9 STEP (분석 → 프로젝트 구조 → 컴포넌트 → 의존성 → 설정 → Phase 계획 → 인터뷰 → 확인 → 파일 갱신)
- `.claude/skills/design-impl-spec/references/impl-spec-template.md` — 유형별 프로젝트 구조 템플릿 (7개), 컴포넌트 상세 규칙, Phase 계획 규칙

---

## 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026-05-12 | 최초 작성 |
| 2026-05-12 | 전체 산출물 완료 (SKILL.md 3개 + 참조 템플릿 3개) |
