---
name: kickoff-skills
type: project-specific
version: 1.0
description: GitHub Skill_package에서 기본 개발 스킬 7개를 가져와 프로젝트에 설치한다. "/kickoff-skills", "스킬 설치해줘", "기본 스킬 가져와" 등의 요청 시 트리거한다.
required_environment:
  - gh CLI 설치 및 인증
depends_on:
  - kickoff-checklist
produces:
  - .claude/skills/* (기본 7개 스킬)
references: []
---

# kickoff-skills Skill

GitHub Skill_package 레포에서 기본 개발 스킬 7개를 가져와 프로젝트의 `.claude/skills/`에 배치하는 스킬. 프로젝트 유형에 따라 선택적 스킬 추가도 안내.

---

## 사전 조건

- gh CLI 설치 및 인증 (`gh auth status`로 확인)
- 인터넷 접근 가능
- `.claude/skills/` 디렉토리 쓰기 권한

---

## STEP 1 — gh CLI 확인

```bash
gh --version
gh auth status
```

### 분기

- **gh 설치됨 + 인증됨** → STEP 2로 진행
- **gh 미설치** → 안내 메시지 출력:

```
## ⚠️ gh CLI가 설치되어 있지 않습니다

스킬 설치에 gh CLI가 필요합니다.
- 설치: https://cli.github.com/
- 설치 후: `gh auth login`

**선택:**
1. 설치 후 다시 실행
2. 스킬 설치 패스 (나중에 수동으로 가능)
```

- **gh 인증 실패** → `gh auth login` 안내 후 재시도 요청

---

## STEP 2 — 기본 스킬 가져오기

### 소스 레포

```
https://github.com/SoyeonAhn3/Skill_package.git
경로: .claude/skills/
```

### 기본 7개 스킬 (무조건 설치)

| # | 스킬명 | 역할 |
|---|---|---|
| 1 | dev-log | 개발 중 에러/변경 기록 (JSONL) |
| 2 | github-push | 커밋 & 푸시 자동화 |
| 3 | phase-doc | Phase 문서 관리 및 갱신 |
| 4 | readme-gen | README.md/README_ko.md 자동 생성 |
| 5 | gen-manual | 매뉴얼 생성 |
| 6 | skill-template | 새 스킬 추가 시 템플릿 |
| 7 | test-scenario | 테스트 시나리오 자동 생성 및 결과 기록 |

### 복사 방식

gh CLI로 특정 폴더만 sparse checkout:

```bash
# 임시 디렉토리에 sparse clone
gh repo clone SoyeonAhn3/Skill_package -- --depth 1 --filter=blob:none --sparse
cd Skill_package
git sparse-checkout set .claude/skills/dev-log .claude/skills/github-push .claude/skills/phase-doc .claude/skills/readme-gen .claude/skills/gen-manual .claude/skills/skill-template .claude/skills/test-scenario
# 복사 후 임시 디렉토리 삭제
```

### 충돌 처리

이미 같은 이름의 스킬이 `.claude/skills/`에 존재하는 경우:

```
[스킬명]이 이미 존재합니다. 어떻게 할까요?
1. 덮어쓰기 (최신 버전으로 교체)
2. 건너뛰기 (현재 버전 유지)
3. 전체에 대해 건너뛰기
```

---

## STEP 3 — 선택적 스킬 확인

프로젝트 유형에 따라 추가 스킬을 제안한다.

| 스킬 | 추가 조건 |
|---|---|
| ai-multi-discussion | AI 프로젝트, 복수 AI 비교 필요 |
| interview-prep | 사용자 인터뷰가 추가로 필요한 경우 |
| readme-update | 장기 프로젝트, README 지속 갱신 |

### 출력 형식

```
## 📦 선택적 스킬

프로젝트 유형([유형명])에 맞는 추가 스킬이 있습니다:

| # | 스킬 | 역할 | 추천 이유 |
|---|---|---|---|
| 1 | [스킬명] | [역할] | [이유] |

설치할 번호를 말씀해주세요. (예: "1 설치" / "전부 패스")
```

---

## STEP 4 — 완료 보고 및 상태 저장

### 상태 파일 갱신

Glob으로 `**/kickoff_state.md`를 검색하여 상태 파일을 Read한 후 Edit으로 아래 내용을 추가/갱신한다:

1. `마지막 완료`를 `kickoff-skills`로 변경
2. `마지막 갱신`을 현재 시각으로 변경
3. 섹션 8을 추가:

```markdown
## 8. 스킬 세팅 (kickoff-skills)

상태: 완료
설치된 스킬: [N]개
```

### 안내 출력

```
## ✅ 스킬 설치 완료

### 설치된 스킬

| # | 스킬 | 상태 |
|---|---|---|
| 1 | dev-log | ✅ 설치됨 |
| 2 | github-push | ✅ 설치됨 |
| 3 | phase-doc | ✅ 설치됨 |
| 4 | readme-gen | ✅ 설치됨 |
| 5 | gen-manual | ✅ 설치됨 |
| 6 | skill-template | ✅ 설치됨 |
| 7 | test-scenario | ✅ 설치됨 |
| (선택) | [스킬명] | ✅ / ⏭️ 패스 |

---

🎉 **킥오프 완료!**

프로젝트 착수에 필요한 모든 준비가 끝났습니다:
- `{산출물 경로}/{프로젝트명}_kickoff.md` — 프로젝트 기준 문서
- `{산출물 경로}/kickoff_state.md` — 킥오프 진행 이력
- `.claude/skills/*` — 개발 스킬 세트

이제 체크리스트(섹션 6)를 확인하면서 개발을 시작하시면 됩니다.
```

---

## 실패 처리

| 실패 유형 | 처리 방법 |
|---|---|
| gh CLI 미설치 | 설치 안내 + 패스 허용 |
| gh 인증 실패 | `gh auth login` 안내 |
| 레포 접근 불가 (private/삭제) | 에러 메시지 + 수동 복사 안내 |
| 네트워크 오류 | 재시도 안내 + 패스 허용 |
| 디스크 쓰기 실패 | 권한 확인 안내 |

---

## 주의사항

- 기존 kickoff-* 스킬은 절대 덮어쓰지 않음 (이 프로젝트의 핵심 스킬)
- 기본 7개 복사 시 kickoff-* 폴더는 제외
- gh 패스 시에도 킥오프 자체는 완료로 처리 (스킬은 나중에 수동 설치 가능)
- 임시 클론 디렉토리는 반드시 정리
