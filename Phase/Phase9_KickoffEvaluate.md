# Phase 9 — KickoffEvaluate `Done`

> Honest Evaluation Layer -- 4+2 dimension project value and feasibility assessment

**Status**: Done
**Prerequisites**: Phase 8
**Version**: v1.5

---

## Overview

After the kickoff document (profile) is complete, this skill evaluates "is this project really fit for purpose?" across 4+2 dimensions. While gap analysis catches contradictions and omissions within the document, evaluate judges the project's viability itself. This is the harness's key differentiator.

---

## Deliverables

| # | Skill / Module | Status | Skill Type |
|---|---|---|---|
| 1 | `kickoff-evaluate` SKILL.md | Done | project-specific |
| 2 | `references/evaluation-criteria.md` | Done | - |
| 3 | `kickoff-gap` SKILL.md + gap-rules.md modification (category 6 added) | Done | - |
| 4 | `profile-template.md` modification (section 7 placeholder) | Done | Already reflected in Phase 8 |
| 5 | `kickoff-checklist` SKILL.md modification (next step -> evaluate) | Done | - |
| 6 | Portfolio project test | Deferred | Integration test |
| 7 | Web/app project test (security dimension activation) | Deferred | Integration test |

---

## kickoff-evaluate SKILL.md Design

### STEP Structure

| STEP | Content | Output |
|---|---|---|
| STEP 1 | Read kickoff document + user context | Evaluation input collected |
| STEP 2 | Evaluate across 4+2 dimensions (includes conditional activation logic) | Per-dimension rating |
| STEP 3 | Present results and collect user reaction | User choice (keep / adjust / pivot) |
| STEP 4 | (Optional) Reflect scope adjustment | Kickoff document modified |
| STEP 5 | Update file and save state | Kickoff document section 7 + state updated |

### Evaluation Dimensions (4+2 Structure)

**Always-on (4)**:

| # | Dimension | Core Question |
|---|---|---|
| 1 | Differentiation | Does this project stand out for its stated purpose? |
| 2 | AI Appropriateness | Is calling this "AI" justified? Could rules replace it? |
| 3 | Market Validity | Will this still be relevant in 6 months? Oversaturated? |
| 4 | Completion Expectation | Can a working demo actually be produced? |

**Conditional (2)**:

| # | Dimension | Core Question | Activation Condition |
|---|---|---|---|
| 5 | Learning Cost | Is there too much to learn for the user's level? Achievable in time? | **Portfolio or learning purpose only** |
| 6 | Security Appropriateness | Are auth, sensitive data, and input validation addressed? | **Web/app + external users only** |

**Conditional Dimension Deactivation Reasons**:

| Dimension | Deactivation Condition | Reason |
|---|---|---|
| Learning Cost | Work automation, production | Known-tech based; learning is not the bottleneck. Time/resource issues covered by Completion Expectation |
| Security Appropriateness | Portfolio + dummy data, personal learning, CLI (local only) | No external exposure, security check unnecessary |

### Rating System

| Rating | Meaning | Follow-up |
|---|---|---|
| Fit | No issues | None |
| Conditional | Could be improved | Specific improvement suggestions presented |
| Review needed | Direction itself has issues | Alternatives presented + user decision requested |

### User Reactions

| Choice | Handling |
|---|---|
| 1. Keep | Record evaluation only, proceed to next step |
| 2. Adjust scope | Discuss adjustments with user -> modify relevant kickoff sections |
| 3. Pivot | Discuss direction change -> suggest re-running from interview if needed |

---

## evaluation-criteria.md Key Content

### Purpose-Specific Differentiation Standards

| Purpose | What "Differentiation" Means |
|---|---|
| Portfolio | Would a recruiter think "this is different"? |
| Work automation | Is there a clear improvement over the current manual process? |
| Learning | Does the user genuinely acquire new skills? |
| Production | Is business value measurable? |

### Learning Cost (Conditional Dimension)

**Activation**: Purpose is portfolio or learning

**Checklist**:
- Number of new technologies to learn vs. current level
- Whether learning + implementation is feasible within time budget
- Gap between skills needed for core features vs. skills already held

**Deactivation**: Work automation, production (known-tech based; time/resources covered by Completion Expectation)

### Security Appropriateness (Conditional Dimension)

**Activation**: Web/app project + external users confirmed

**Checklist**:
- Auth/authorization design present
- Sensitive data encryption/masking considered
- Input validation (XSS, SQL injection) mentioned
- HTTPS/TLS plan included

**Deactivation**: Portfolio + dummy data, personal learning, CLI (local only)

---

## Existing Skill Modifications

| Skill | Modification |
|---|---|
| kickoff-gap | Add "re-check items flagged by evaluate" category to gap-rules.md |
| profile-template.md | Add section 7 placeholder: `## 7. Honest Evaluation\n> This section is added when /kickoff-evaluate runs.` |

---

## Prerequisites & Dependencies

- Phase 8 complete (kickoff-context needed for purpose/level-based evaluation)
- kickoff-profile must be complete (kickoff document required)

---

## Development Notes

- Evaluation must NOT discourage users -- frame as "knowing before dev > knowing after dev"
- Review-needed rating means "try this alternative" NOT "stop"
- Without context (Phase 8 skipped) -> general evaluation only (no purpose-specific assessment)
- Security dimension is conditional -- do not force security checks on projects that don't need them

---

## Change Log

| Date | Description |
|---|---|
| 2026-05-06 | Initial creation |
| 2026-05-06 | Changed dimension structure from 5+1 to 4+2. Learning Cost moved to conditional (active for portfolio/learning only) |
| 2026-05-06 | Implementation complete. SKILL.md + evaluation-criteria.md written, gap-rules.md category 6 added, checklist next-step modified |

---
---

# Phase 9 — 정직한 평가 레이어 `완료`

> 프로젝트의 가치와 실현가능성을 솔직하게 평가하는 Honest Evaluation Layer 개발

**상태**: 완료
**선행 조건**: Phase 8 완료
**버전**: v1.5

---

## 개요

킥오프 문서(profile)가 완성된 후, "이 프로젝트가 정말 목적에 맞는가?"를 4+2개 차원으로 평가하는 스킬. gap 분석이 "문서 내 모순/누락"을 잡는다면, evaluate는 "프로젝트 자체의 가치와 실현가능성"을 판단한다. 하네스의 핵심 차별점.

---

## 완료 예정 / 완료 항목

| # | Skill / 모듈 | 상태 | 스킬 타입 |
|---|---|---|---|
| 1 | `kickoff-evaluate` SKILL.md 작성 | 완료 | project-specific |
| 2 | `references/evaluation-criteria.md` 작성 | 완료 | - |
| 3 | `kickoff-gap` SKILL.md + gap-rules.md 수정 (평가 연동, 카테고리 6 추가) | 완료 | - |
| 4 | `profile-template.md` 수정 (섹션 7 플레이스홀더) | 완료 | Phase 8에서 이미 반영됨 |
| 5 | `kickoff-checklist` SKILL.md 수정 (다음 단계 -> evaluate) | 완료 | - |
| 6 | 포트폴리오 프로젝트 대상 테스트 | 보류 | 통합 테스트에서 검증 |
| 7 | 웹/앱 프로젝트 대상 테스트 (보안 차원 활성화 확인) | 보류 | 통합 테스트에서 검증 |

---

## kickoff-evaluate SKILL.md 설계

### STEP 구조

| STEP | 내용 | 산출물 |
|---|---|---|
| STEP 1 | 킥오프 문서 + 사용자 컨텍스트 읽기 | 평가 입력 수집 |
| STEP 2 | 4+2개 차원별 평가 수행 (조건부 차원 활성화 판단 포함) | 차원별 판정 |
| STEP 3 | 결과 제시 및 사용자 반응 수집 | 사용자 선택 (유지/조정/전환) |
| STEP 4 | (선택) 범위 조정 반영 | 킥오프 문서 수정 |
| STEP 5 | 파일 업데이트 및 상태 저장 | 킥오프 문서 섹션 7 + state 갱신 |

### 평가 차원 (4+2 구조)

**항상 적용 (4개)**:

| # | 차원 | 핵심 질문 |
|---|---|---|
| 1 | 차별화 | 이 프로젝트가 목적에 맞게 눈에 띄는가? |
| 2 | AI 적절성 | AI라 부르기 적절한가? 규칙 기반으로 대체 가능한가? |
| 3 | 시장 유효성 | 6개월 뒤에도 유효한가? 유사 프로젝트 범람하지 않는가? |
| 4 | 완성도 기대치 | 실제 동작하는 데모가 나올 수 있는가? |

**조건부 적용 (2개)**:

| # | 차원 | 핵심 질문 | 활성화 조건 |
|---|---|---|---|
| 5 | 학습 비용 | 수준 대비 배울 게 과다하지 않은가? 시간 내 가능한가? | **포트폴리오 또는 학습 목적 시** |
| 6 | 보안 적절성 | 인증/인가, 민감 데이터, 입력 검증이 고려되었는가? | **웹/앱 + 외부 사용자 시** |

**조건부 차원 비활성 사유**:

| 차원 | 비활성 조건 | 이유 |
|---|---|---|
| 학습 비용 | 업무 자동화, 실무 투입 | 이미 아는 기술 기반이므로 학습량이 병목이 아님. 시간/리소스 문제는 "완성도 기대치"에서 커버 |
| 보안 적절성 | 포트폴리오 + 더미 데이터, 개인 학습용, CLI 도구 (로컬 전용) | 외부 노출이 없으므로 보안 점검 불필요 |

### 판정 체계

| 판정 | 의미 | 후속 조치 |
|---|---|---|
| 적합 | 문제 없음 | 없음 |
| 조건부 | 개선하면 더 좋음 | 구체적 개선 제안 제시 |
| 재검토 | 방향 자체에 문제 | 대안 제시 + 사용자 결정 요청 |

### 사용자 반응별 처리

| 선택 | 처리 |
|---|---|
| 1. 유지 | 평가 결과만 기록, 다음 단계 진행 |
| 2. 조정 | 사용자와 조정 논의 -> 킥오프 문서 해당 섹션 수정 |
| 3. 전환 | 방향 전환 논의 -> 필요 시 interview부터 재실행 안내 |

---

## evaluation-criteria.md 핵심 내용

### 목적별 차별화 기준

| 목적 | "차별화"의 의미 |
|---|---|
| 포트폴리오 | 채용 담당자가 "이건 다르다"고 느끼는가? |
| 업무 자동화 | 현재 수동 프로세스 대비 명확한 개선이 있는가? |
| 학습 | 새로운 스킬을 실질적으로 습득하는가? |
| 실무 투입 | 비즈니스 가치가 측정 가능한가? |

### 학습 비용 (조건부 차원)

**활성화 조건**: 사용자 컨텍스트에서 목적이 포트폴리오 또는 학습인 경우

**점검 항목**:
- 현재 기술 수준 대비 새로 배워야 할 기술 수
- 시간 예산 내 학습 + 구현이 가능한지
- 핵심 기능에 필요한 기술 vs 이미 보유한 기술 격차

**비활성 조건**: 업무 자동화, 실무 투입 (이미 아는 기술 기반, 시간/리소스는 "완성도 기대치"에서 커버)

### 보안 적절성 (조건부 차원)

**활성화 조건**: 사용자 컨텍스트에서 웹/앱 프로젝트 + 외부 사용자 존재 확인 시

**점검 항목**:
- 인증/인가 설계 여부
- 민감 데이터 암호화/마스킹 고려
- 입력 검증 (XSS, SQL injection) 언급
- HTTPS/TLS 적용 계획

**비활성 조건**: 포트폴리오 + 더미 데이터, 개인 학습용, CLI 도구 (로컬 전용)

---

## 기존 스킬 수정 범위

| 스킬 | 수정 내용 |
|---|---|
| kickoff-gap | gap-rules.md에 "평가에서 지적된 항목 재확인" 카테고리 추가 |
| profile-template.md | 섹션 7 플레이스홀더 추가: `## 7. 정직한 평가\n> 이 섹션은 /kickoff-evaluate 실행 시 추가됩니다.` |

---

## 선행 조건 및 의존성

- Phase 8 완료 (kickoff-context가 있어야 목적/수준 기반 평가 가능)
- kickoff-profile 완료 상태에서만 실행 가능 (킥오프 문서 필요)

---

## 주의사항

- 평가가 사용자를 **낙담시키면 안 됨** -- "개발 전에 아는 것이 개발 후에 아는 것보다 낫다" 프레임
- 재검토 판정도 "그만둬라"가 아니라 "이렇게 바꾸면 된다" 대안 필수
- context 없이 실행 시 (Phase 8 스킵) -> 일반적 평가만 수행 (목적 특화 불가)
- 보안 차원은 조건부 -- 불필요한 프로젝트에 보안 강요하지 않음

---

## 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026-05-06 | 최초 작성 |
| 2026-05-06 | 평가 차원 5+1 -> 4+2 구조로 변경. 학습 비용을 조건부 차원으로 이동 (포트폴리오/학습 목적 시에만 활성화) |
| 2026-05-06 | 구현 완료. SKILL.md + evaluation-criteria.md 작성, gap-rules.md 카테고리 6 추가, checklist 다음 단계 수정 |
