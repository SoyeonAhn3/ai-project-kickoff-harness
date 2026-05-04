---
name: kickoff-profile
type: project-specific
version: 1.0
description: 인터뷰 답변과 채택된 아이디어를 구조화하여 project_kickoff.md를 생성한다. "/kickoff-profile", "킥오프 문서 만들어줘", "프로필 생성해줘" 등의 요청 시 트리거한다.
required_environment: []
depends_on:
  - kickoff-suggest
produces:
  - pre-requirement/project_kickoff.md
references:
  - references/profile-template.md   # project_kickoff.md 표준 구조 가이드
---

# kickoff-profile Skill

대화 컨텍스트에 쌓인 인터뷰 답변 + 채택된 아이디어를 구조화하여 project_kickoff.md 파일을 생성하는 스킬. 이 파일은 이후 모든 단계의 Single Source of Truth.

---

## 사전 조건

- `kickoff-suggest` 완료 (또는 전부 패스)
- 기획 인터뷰 답변이 대화 컨텍스트에 있어야 함
- 없으면 `/kickoff-interview`를 먼저 실행하도록 안내

---

## STEP 1 — 컨텍스트 수집

대화 컨텍스트에서 아래 정보를 수집한다:

| 출처 | 수집 항목 |
|---|---|
| kickoff-start | 프로젝트 유형, 아이디어 요약 |
| kickoff-interview (기획) | P1~P7 답변 (사용자, 목적, 데이터소스, 결과형태, 핵심기능, MVP, 제약사항) |
| kickoff-interview (설계) | D1~D4 답변 (아키텍처, 데이터구조, 볼륨, 실패시나리오) — 패스 시 없음 |
| kickoff-suggest | 채택된 아이디어 목록 + MVP/확장 분류 — 전부 패스 시 없음 |

---

## STEP 2 — 파일 생성

### 동작

1. `pre-requirement/` 폴더 존재 확인 (없으면 생성)
2. `references/profile-template.md` 참조하여 구조 결정
3. project_kickoff.md 작성

### 분기: 설계 인터뷰 진행 여부

**설계 인터뷰 진행한 경우** → 섹션 1~4 + 섹션 5, 6 플레이스홀더

**설계 인터뷰 패스한 경우** → 섹션 1 + 섹션 5, 6 플레이스홀더 (섹션 2, 3, 4 생략)

### 작성 규칙

- 프로젝트명: 사용자가 명시하지 않으면 AI가 아이디어에서 적절한 이름 생성
- AI 추천 표기: "추천해줘"로 답한 항목은 값 뒤에 `(AI 추천)` 표기
- 빈 항목: "미정" 표기 (빈칸 금지)
- 섹션 5, 6: 헤더 + 안내 문구만 (이후 스킬이 내용 추가)
- 언어: 사용자가 사용한 언어로 작성

---

## STEP 3 — 사용자 확인

파일 생성 후 내용을 요약하여 사용자에게 확인을 받는다.

### 출력 형식

```
## 📄 project_kickoff.md 생성 완료

**저장 위치**: `pre-requirement/project_kickoff.md`

### 포함된 내용:

| 섹션 | 상태 |
|---|---|
| 1. 프로젝트 프로필 | ✅ 작성됨 |
| 2. 시스템 아키텍처 | ✅ 작성됨 / ⏭️ 생략 (설계 패스) |
| 3. 데이터 구조 | ✅ 작성됨 / ⏭️ 생략 (설계 패스) |
| 4. 실패 시나리오 | ✅ 작성됨 / ⏭️ 생략 (설계 패스) |
| 5. 누락/모순 점검 | ⏳ 대기 (/kickoff-gap에서 추가) |
| 6. 개발 착수 체크리스트 | ⏳ 대기 (/kickoff-checklist에서 추가) |

수정할 부분이 있으면 말씀해주세요.
없으면 `/kickoff-gap`을 실행하여 누락/모순을 점검합니다.
```

### 사용자 수정 요청 시

- 해당 부분을 수정하고 파일을 다시 저장
- 수정 완료 후 다시 확인 요청

---

## STEP 4 — 완료 안내

사용자가 확인하면:

```
## ✅ 프로젝트 킥오프 문서 확정

**파일**: `pre-requirement/project_kickoff.md`

다음 단계로 `/kickoff-gap`을 실행하면 누락/모순 점검이 시작됩니다.
```

---

## 출력 형식

이 스킬은 **파일을 생성**한다:
- 경로: `{프로젝트 루트}/pre-requirement/project_kickoff.md`
- 이후 `kickoff-gap`과 `kickoff-checklist`가 이 파일을 읽고 섹션 5, 6을 추가

---

## 실패 처리

| 실패 유형 | 처리 방법 |
|---|---|
| 인터뷰 답변 없이 실행 | `/kickoff-interview`를 먼저 실행하도록 안내 |
| pre-requirement/ 폴더 생성 실패 | 에러 메시지 출력 + 수동 생성 안내 |
| 기존 project_kickoff.md 존재 | "덮어쓰기 / 다른 이름 / 취소" 선택지 제시 |
| 사용자가 대폭 수정 요청 | 수정 반영 후 파일 재저장 + 재확인 |

---

## 주의사항

- 섹션 헤더 포맷(## 1. / ## 2. 등)을 정확히 유지 — 이후 스킬이 파싱에 의존
- 섹션 5, 6 플레이스홀더를 반드시 포함 — 이후 스킬이 이 위치에 내용 추가
- 기존 파일이 있을 때 무조건 덮어쓰지 않음 — 사용자 확인 필수
- AI가 생성한 내용은 사용자 확인 후에만 확정
