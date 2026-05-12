# Phase 10 — KickoffDone `Done`

> Definition of Done -- measurable project completion criteria generation (3+4 categories)

**Status**: Done
**Prerequisites**: Phase 9
**Version**: v1.5

---

## Overview

If checklist defines "can we start?", this skill defines "can we call it done?". Categories are dynamically determined based on project purpose and type. Items rated Conditional or Review-needed by evaluate must have matching completion criteria.

---

## Deliverables

| # | Skill / Module | Status | Skill Type |
|---|---|---|---|
| 1 | `kickoff-done` SKILL.md | Done | project-specific |
| 2 | `references/done-criteria-templates.md` | Done | - |
| 3 | `kickoff-checklist` SKILL.md modification (next step guidance) | Done | evaluate->done connection completed in Phase 9 |
| 4 | `profile-template.md` modification (section 8 placeholder) | Done | Already reflected in Phase 8 |
| 5 | Portfolio project test (demo criteria activation) | Deferred | Integration test |
| 6 | Web/app project test (security + operational criteria activation) | Deferred | Integration test |

---

## kickoff-done SKILL.md Design

### STEP Structure

| STEP | Content | Output |
|---|---|---|
| STEP 1 | Read kickoff document + context + evaluate results | Completion criteria generation input |
| STEP 2 | Generate criteria by category (5-10 total) | Draft criteria |
| STEP 3 | Present results and collect user confirmation (add/remove/edit) | Confirmed criteria |
| STEP 4 | Update file and save state | Kickoff document section 8 + state updated |

### Categories (Including Conditional)

**Always-on (3)**:

| Category | Applies | Example |
|---|---|---|
| Functional | Always | "API->Snowflake ingestion completes without errors" |
| Quality | Always | "Full pipeline completes within 5 minutes" |
| Documentation | Always | "README includes execution guide" |

**Conditional (4)**:

| Category | Activation Condition | Example |
|---|---|---|
| Demo-ready | **Portfolio purpose** | "A demo scenario under 3 minutes exists" |
| Operational | **Production deployment** | "Production deploy complete + health check 200" |
| Security | **Web/app + external users** | "OWASP Top 10 basic items addressed" |
| Learning Evidence | **Learning purpose** | "At least 1 blog post on learned content" |

### Writing Rules

- Verifiable statements ("X completes", "X exists", "X returns Y")
- No subjective terms ("good", "appropriate" -> use specific metrics/states)
- 5-10 criteria total (too few = vague, too many = burdensome)
- MVP scope only -- exclude "future expansion" features
- Conditional/Review-needed items from evaluate MUST have matching criteria

### Type-Specific Examples

| Project Type | Functional Example | Quality Example |
|---|---|---|
| Data pipeline | "Source->sink data flow operates normally" | "Data integrity check passes" |
| AI project | "Model inference returns expected results" | "Accuracy/recall meets threshold" |
| Web app | "Core user flow works end-to-end" | "Page load under 3 seconds" |
| Automation | "Scheduled execution runs normally" | "Failure alert sent on error" |
| BI dashboard | "All charts display data" | "Data refreshes per defined cycle" |

---

## done-criteria-templates.md Key Content

### Purpose-Specific Additional Criteria Examples

| Purpose | Category | Criteria Example |
|---|---|---|
| Portfolio | Demo | "Screenshots/GIF in README", "Run instructions in 3 steps or fewer" |
| Production | Operational | "Monitoring dashboard configured", "Rollback procedure documented" |
| Web/app | Security | "No access without auth confirmed", "SQL injection test passed" |
| Learning | Learning Evidence | "Can explain 3+ core concepts", "TIL records exist" |

---

## Existing Skill Modifications

| Skill | Modification |
|---|---|
| kickoff-checklist | Changed "next step" in output guidance to `/kickoff-done` |
| profile-template.md | Added section 8 placeholder: `## 8. Definition of Done\n> This section is added when /kickoff-done runs.` |

---

## Prerequisites & Dependencies

- Phase 9 complete (uses evaluate results)
- kickoff-checklist must be in complete state
- With kickoff-context data: purpose-specific categories activated. Without: only base 3 (Functional / Quality / Documentation)

---

## Development Notes

- Do NOT confuse with checklist: done = "end" definition, checklist = "start" definition
- Criteria too high = frustration, too low = meaningless -- match to user level
- Works without evaluate (base 3 categories only)
- Exclude "future expansion" features from criteria -- MVP scope only

---

## Change Log

| Date | Description |
|---|---|
| 2026-05-06 | Initial creation |
| 2026-05-06 | Implementation complete. SKILL.md + done-criteria-templates.md written. checklist->evaluate->done flow connection completed |

---
---

# Phase 10 — 완료 조건 생성 `완료`

> 측정 가능한 프로젝트 완료 조건(Definition of Done) 5~10개를 생성하는 스킬 개발

**상태**: 완료
**선행 조건**: Phase 9 완료
**버전**: v1.5

---

## 개요

체크리스트가 "개발을 시작할 수 있는 조건"이라면, 이 스킬은 "개발이 끝났다고 할 수 있는 조건"을 정의한다. 프로젝트 목적/유형에 따라 카테고리가 동적으로 결정되며, evaluate에서 조건부/재검토로 지적된 항목은 반드시 대응하는 완료 조건이 포함된다.

---

## 완료 예정 / 완료 항목

| # | Skill / 모듈 | 상태 | 스킬 타입 |
|---|---|---|---|
| 1 | `kickoff-done` SKILL.md 작성 | 완료 | project-specific |
| 2 | `references/done-criteria-templates.md` 작성 | 완료 | - |
| 3 | `kickoff-checklist` SKILL.md 수정 (다음 단계 안내) | 완료 | Phase 9에서 evaluate->done 연결 완료 |
| 4 | `profile-template.md` 수정 (섹션 8 플레이스홀더) | 완료 | Phase 8에서 이미 반영됨 |
| 5 | 포트폴리오 프로젝트 대상 테스트 (데모 기준 활성화) | 보류 | 통합 테스트에서 검증 |
| 6 | 웹/앱 프로젝트 대상 테스트 (보안+운영 기준 활성화) | 보류 | 통합 테스트에서 검증 |

---

## kickoff-done SKILL.md 설계

### STEP 구조

| STEP | 내용 | 산출물 |
|---|---|---|
| STEP 1 | 킥오프 문서 + 컨텍스트 + 평가 결과 읽기 | 완료 조건 생성 입력 |
| STEP 2 | 카테고리별 완료 조건 생성 (5~10개) | 초안 |
| STEP 3 | 결과 제시 및 사용자 확인 (추가/삭제/수정) | 확정된 조건 |
| STEP 4 | 파일 업데이트 및 상태 저장 | 킥오프 문서 섹션 8 + state 갱신 |

### 카테고리 (조건부 포함)

**항상 적용 (3개)**:

| 카테고리 | 적용 조건 | 예시 |
|---|---|---|
| 기능 동작 (Functional) | 항상 | "API->Snowflake 적재가 에러 없이 완료된다" |
| 품질 기준 (Quality) | 항상 | "전체 파이프라인이 5분 이내에 완료된다" |
| 문서화 (Documentation) | 항상 | "README에 실행 가이드가 포함되어 있다" |

**조건부 (4개)**:

| 카테고리 | 활성화 조건 | 예시 |
|---|---|---|
| 데모 기준 (Demo-ready) | **포트폴리오 목적 시** | "3분 이내 데모 시나리오가 존재한다" |
| 운영 기준 (Operational) | **실무 투입 시** | "프로덕션 배포 완료 + health check 200" |
| 보안 기준 (Security) | **웹/앱 + 외부 사용자 시** | "OWASP Top 10 기본 항목 대응 확인" |
| 학습 증거 (Learning) | **학습 목적 시** | "학습 내용 블로그 포스트 1개 이상" |

### 작성 규칙

- "~한다", "~있다" 형태 (검증 가능한 문장)
- 주관적 표현 금지 ("좋은", "적절한" X -> 구체적 수치/상태)
- 총 5~10개 (너무 적으면 모호, 너무 많으면 부담)
- MVP 범위에 맞게 -- "이후 확장" 기능은 포함하지 않음
- evaluate에서 조건부/재검토 지적 항목 -> 반드시 대응 조건 포함

### 유형별 기본 조건 예시

| 프로젝트 유형 | 기능 동작 예시 | 품질 예시 |
|---|---|---|
| 데이터 파이프라인 | "소스->싱크 데이터 흐름이 정상 동작" | "데이터 정합성 검증 통과" |
| AI 프로젝트 | "모델 추론이 기대 결과를 반환" | "정확도/재현율이 기준치 이상" |
| 웹앱 | "핵심 유저 플로우가 정상 동작" | "페이지 로드 3초 이내" |
| 자동화 | "스케줄 실행이 정상 동작" | "실패 시 알림 발송 확인" |
| BI 대시보드 | "모든 차트가 데이터를 표시" | "갱신 주기에 맞게 데이터 업데이트" |

---

## done-criteria-templates.md 핵심 내용

### 목적별 추가 조건 예시

| 목적 | 카테고리 | 조건 예시 |
|---|---|---|
| 포트폴리오 | 데모 | "스크린샷/GIF가 README에 포함", "실행 방법 3단계 이내" |
| 실무 투입 | 운영 | "모니터링 대시보드 설정 완료", "롤백 절차 문서화" |
| 웹/앱 | 보안 | "인증 없이 접근 불가 확인", "SQL injection 테스트 통과" |
| 학습 | 학습 증거 | "핵심 개념 3개 이상 설명 가능", "TIL 기록 존재" |

---

## 기존 스킬 수정 범위

| 스킬 | 수정 내용 |
|---|---|
| kickoff-checklist | 안내 출력의 "다음 단계"를 `/kickoff-done`으로 변경 |
| profile-template.md | 섹션 8 플레이스홀더 추가: `## 8. 완료 조건\n> 이 섹션은 /kickoff-done 실행 시 추가됩니다.` |

---

## 선행 조건 및 의존성

- Phase 9 완료 (evaluate 결과를 활용하므로)
- kickoff-checklist 완료 상태에서만 실행 가능
- kickoff-context 데이터가 있으면 목적별 카테고리 활성화, 없으면 기본 3개(기능/품질/문서화)만 생성

---

## 주의사항

- 체크리스트(착수 조건)와 혼동 금지 -- done은 "끝"의 정의, checklist는 "시작"의 정의
- 완료 조건이 너무 높으면 좌절, 너무 낮으면 무의미 -- 사용자 수준에 맞게 조정
- evaluate 없이 실행해도 동작 (기본 조건만 생성)
- "이후 확장"으로 분류된 기능은 완료 조건에 넣지 않음 (MVP 범위만)

---

## 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026-05-06 | 최초 작성 |
| 2026-05-06 | 구현 완료. SKILL.md + done-criteria-templates.md 작성. checklist->evaluate->done 흐름 연결 완료 |
