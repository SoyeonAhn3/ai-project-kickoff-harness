# Phase 4 — kickoff-profile 스킬 개발 `🔲 미시작`

> 인터뷰 답변과 채택 아이디어를 구조화하여 project_kickoff.md를 생성하는 스킬 개발

**상태**: 🔲 미시작
**선행 조건**: Phase 3 완료

---

## 개요

대화 컨텍스트에 쌓인 인터뷰 답변 + 채택된 아이디어를 구조화하여 project_kickoff.md 파일을 생성한다. 이 파일은 이후 kickoff-gap, kickoff-checklist가 읽고 섹션을 추가하는 기준 문서.

---

## 완료 예정 / 완료 항목

| # | Skill / 모듈 | 상태 | 스킬 타입 |
|---|---|---|---|
| 1 | `kickoff-profile` SKILL.md 작성 | 🔲 | project-specific |
| 2 | `references/profile-template.md` 작성 | 🔲 | - |
| 3 | 섹션 1~4 구조 정의 | 🔲 | - |
| 4 | 설계 인터뷰 패스 시 섹션 생략 로직 | 🔲 | - |
| 5 | 동작 테스트 | 🔲 | - |

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
2. pre-requirement/ 폴더 확인 (없으면 생성)
3. profile-template.md 참조하여 project_kickoff.md 작성:
   - 섹션 1: 프로젝트 프로필 (기본정보, 목적, 사용자, 핵심기능, 기술스택, 제약사항)
   - 섹션 2: 시스템 아키텍처 (파이프라인 흐름, 컴포넌트 구성)
   - 섹션 3: 데이터 구조 (레이어별 테이블, 컬럼, 볼륨, 갱신주기)
   - 섹션 4: 실패 시나리오 / 엣지케이스
4. 설계 인터뷰(3-2)를 패스한 경우 섹션 2, 3, 4 생략
5. 파일 저장 후 사용자에게 확인

### 설계 결정 사항

| 결정 | 내용 | 이유 |
|---|---|---|
| 저장 위치 | pre-requirement/project_kickoff.md | Plan.txt에서 확정 |
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
