# Phase 8 — kickoff-context 개발 `✅ 완료`

> 사용자 메타 정보(목적, 수준, 직무 목표)를 수집하여 이후 모든 스킬에 전파하는 컨텍스트 스킬 개발

**상태**: ✅ 완료
**선행 조건**: Phase 7 완료

---

## 개요

킥오프 흐름의 맨 앞에 삽입되는 신규 스킬. "너는 누구고, 왜 이걸 만들어?"를 먼저 파악하여 이후 인터뷰, 제안, 평가, 체크리스트가 사용자 맥락에 맞게 동작하도록 한다. 이 스킬이 없으면 Feature 2(정직한 평가)가 동작할 수 없으므로 1순위로 개발.

---

## 완료 예정 / 완료 항목

| # | Skill / 모듈 | 상태 | 스킬 타입 |
|---|---|---|---|
| 1 | `kickoff-context` SKILL.md 작성 | ✅ | project-specific |
| 2 | `references/context-questions.md` 작성 | ✅ | - |
| 3 | `references/propagation-guide.md` 작성 | ✅ | - |
| 4 | `kickoff-start` SKILL.md 수정 (사전조건 + 섹션 0-1 추가) | ✅ | - |
| 5 | `kickoff-interview` SKILL.md 수정 (컨텍스트 활용 규칙) | ✅ | - |
| 6 | `kickoff-suggest` SKILL.md 수정 (수준/시간 필터링) | ✅ | - |
| 7 | `kickoff-checklist` SKILL.md 수정 (목적별 항목) | ✅ | - |
| 8 | `profile-template.md` 수정 (배경 서브섹션 + 섹션 7,8 플레이스홀더) | ✅ | - |
| 9 | 동작 테스트 (context → start 연속 실행) | ⏭️ Phase 11 통합 테스트에서 검증 | - |

---

## kickoff-context SKILL.md 설계

### STEP 구조

| STEP | 내용 | 산출물 |
|---|---|---|
| STEP 1 | 목적 확인 (선택지 제시) | 프로젝트 목적 확정 |
| STEP 2 | 수준/역량/시간 파악 (선택지 + 자유 입력) | 기술 수준, 시간 예산 |
| STEP 3 | 목표/차별화 파악 | 직무 목표, 강점 키워드 |
| STEP 4 | 확인 및 상태 저장 | kickoff_state.md 섹션 0-1 생성 |

### 수집 항목

| # | 질문 | 수집 목적 |
|---|---|---|
| 1 | 프로젝트 주된 목적 (포트폴리오/업무 자동화/학습/실무 투입) | 전체 톤 결정 |
| 2 | 주요 독자/평가자 (채용 담당자/팀장/교수/본인) | 산출물 수준 결정 |
| 3 | 현재 기술 수준 (초급/중급/고급 + 구체 역량) | 난이도 필터링 |
| 4 | 목표 직무 (데이터 엔지니어/백엔드/ML 등) | 차별화 방향 |
| 5 | 시간 예산 (1~2주/1개월/2~3개월) | 범위 제한 |
| 6 | 보여주고 싶은 역량 키워드 | suggest/evaluate 기준 |

### 상태 파일 저장 형식

```markdown
## 0-1. 사용자 컨텍스트 (kickoff-context)

| 항목 | 내용 |
|---|---|
| 프로젝트 목적 | [포트폴리오/업무 자동화/학습/실무 투입] |
| 대상 독자/평가자 | [채용 담당자/팀장/교수/본인] |
| 현재 기술 수준 | [초급/중급/고급] + [구체 역량] |
| 목표 직무 | [직무명] |
| 시간 예산 | [기간] |
| 차별화 방향 | [키워드] |
```

---

## propagation-guide.md 핵심 내용

| 하위 스킬 | 활용 방식 |
|---|---|
| kickoff-interview | 목적별 추가 질문 삽입 (포폴이면 "뭘 보여줘야?", 실무면 "SLA는?") |
| kickoff-suggest | 수준/시간에 맞지 않는 제안 필터링 (초급+2주면 난이도 높은 건 제외) |
| kickoff-evaluate | 평가의 기준축 — 목적/수준/시간 대비 프로젝트 적절성 판단 |
| kickoff-gap | "목적 대비 적합성" 점검 카테고리 추가 |
| kickoff-checklist | 목적별 항목 추가 (포폴: README/데모, 실무: 배포/모니터링/보안) |
| kickoff-done | 목적 정렬된 완료 조건 생성 |

---

## 기존 스킬 수정 범위

| 스킬 | 수정 내용 |
|---|---|
| kickoff-start | 사전조건에 "kickoff-context 완료 권장 (미완료 시에도 동작)" 추가 |
| kickoff-interview | "컨텍스트 활용" 서브섹션 추가 — 목적별 추가 질문 규칙 |
| kickoff-suggest | "필터링 규칙" 추가 — 수준/시간 초과 제안에 경고 표시 |
| kickoff-checklist | "목적별 항목" 서브섹션 추가 |
| profile-template.md | 섹션 1에 "### 프로젝트 배경" 서브섹션 추가 |

---

## 선행 조건 및 의존성

- Phase 7 완료 (통합 테스트 통과)
- 기존 스킬 SKILL.md 구조 파악 완료 (Phase 7에서 검증됨)

---

## 개발 시 주의사항

- kickoff-context는 **선택적** — "패스" 시 이후 스킬이 context 없이도 정상 동작해야 함
- 기존 스킬 수정 시 기존 동작을 깨뜨리지 않아야 함 (하위 호환)
- propagation-guide.md는 모든 하위 스킬이 참조하는 단일 규칙 파일

---

## 검증 방법

1. kickoff-context 실행 후 kickoff_state.md에 섹션 0-1이 정확히 기록되는지 확인
2. kickoff-context → kickoff-start 연속 실행 시 context가 start에 영향 주는지 확인
3. "패스" 시 kickoff-start가 독립적으로 동작하는지 확인

---

## 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026-05-06 | 최초 작성 |
| 2026-05-06 | 구현 완료. BL-001(state 슬림화) 반영 — context는 파일 미생성, start가 섹션 0-1로 영속화 |
