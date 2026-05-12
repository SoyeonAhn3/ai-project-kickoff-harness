---
name: kickoff-skills
type: project-specific
version: 2.0
description: 킥오프 완료 후 프로젝트 폴더에 기본 개발 스킬 7개를 복사한다. "/kickoff-skills", "스킬 설치해줘", "기본 스킬 가져와", "스킬 복사해줘" 등의 요청 시 트리거한다.
required_environment:
  - gh CLI 설치 및 인증
depends_on:
  - kickoff-checklist
produces:
  - "../{프로젝트명}/.claude/skills/* (기본 7개 스킬)"
references: []
---

# kickoff-skills Skill

킥오프 문서가 완성된 프로젝트 폴더에 GitHub Skill_package 레포의 기본 개발 스킬 7개를 복사하는 스킬. 스킬은 하네스가 아닌 **새로 생성된 프로젝트 폴더**에 설치된다.

---

## 사전 조건

- 킥오프 문서(`{프로젝트명}_kickoff.md`)가 존재해야 함
- 대화 컨텍스트에 경로가 없으면 Glob으로 `**/*_kickoff.md`를 검색
  - 0개 발견: `/kickoff-start`를 먼저 실행하도록 안내
  - 1개 발견: 해당 파일 Read → YAML frontmatter 확인
  - 2개 이상 발견: frontmatter에 `completed_skills` 필드가 있는 파일만 대상, 여러 개면 사용자에게 선택 요청
- YAML frontmatter `completed_skills`에 `kickoff-checklist`가 포함되어야 함
  - 아니면 `/kickoff-checklist`를 먼저 실행하도록 안내
- gh CLI 설치 및 인증 (`gh auth status`로 확인)

---

## STEP 1 — 스킬 복사 확인

킥오프 완료 후 사용자에게 스킬 복사 여부를 확인한다.

### 출력 형식

```
## 📦 개발 스킬 설치

킥오프가 완료되었습니다. 프로젝트 폴더에 기본 개발 스킬을 복사할까요?

**설치 위치**: `../{프로젝트명}/.claude/skills/`

| # | 스킬 | 역할 |
|---|---|---|
| 1 | dev-log | 개발 중 에러/변경 기록 (JSONL) |
| 2 | github-push | 커밋 & 푸시 자동화 |
| 3 | phase-doc | Phase 문서 관리 및 갱신 |
| 4 | readme-gen | README.md/README_ko.md 자동 생성 |
| 5 | gen-manual | 매뉴얼 생성 |
| 6 | skill-template | 새 스킬 추가 시 템플릿 |
| 7 | test-scenario | 테스트 시나리오 자동 생성 및 결과 기록 |

**선택:**
1. 전체 설치
2. 선택 설치 (번호로 지정)
3. 패스 (나중에 수동 설치)
```

### 분기

- **전체/선택 설치** → STEP 2로 진행
- **패스** → STEP 4로 이동 (스킬 설치 없이 완료 처리)

---

## STEP 2 — gh CLI 확인 및 스킬 복사

### gh CLI 확인

```bash
gh --version
gh auth status
```

- **gh 미설치** → 설치 안내 + 패스 허용
- **gh 인증 실패** → `gh auth login` 안내 후 재시도 요청

### 소스 레포

```
https://github.com/SoyeonAhn3/Skill_package.git
경로: .claude/skills/
```

### 복사 방식

gh CLI로 특정 폴더만 sparse checkout 후 프로젝트 폴더에 복사:

```bash
# 임시 디렉토리에 sparse clone
gh repo clone SoyeonAhn3/Skill_package -- --depth 1 --filter=blob:none --sparse
cd Skill_package
git sparse-checkout set .claude/skills/dev-log .claude/skills/github-push .claude/skills/phase-doc .claude/skills/readme-gen .claude/skills/gen-manual .claude/skills/skill-template .claude/skills/test-scenario
# ../{프로젝트명}/.claude/skills/에 복사 후 임시 디렉토리 삭제
```

### 설치 대상 경로

YAML frontmatter에서 확인한 프로젝트 폴더: `../{프로젝트명}/.claude/skills/`

### 충돌 처리

이미 같은 이름의 스킬이 프로젝트 폴더에 존재하는 경우:

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

## STEP 4 — 완료 및 안내

### YAML frontmatter 갱신

킥오프 문서의 YAML frontmatter `last_skill`을 `kickoff-skills`로 변경, `completed_skills`에 `kickoff-skills` 추가 (Edit 사용)

### 안내 출력

```
## ✅ 킥오프 완료!

### 프로젝트 폴더 구조

{프로젝트명}/
├── pre-requirement/
│   └── {프로젝트명}_kickoff.md    ← 프로젝트 기준 문서
└── .claude/skills/                ← 개발 스킬 세트
    ├── dev-log/
    ├── github-push/
    └── ...

### 설치된 스킬

| # | 스킬 | 상태 |
|---|---|---|
| 1 | dev-log | ✅ / ⏭️ |
| ... | ... | ... |

---

이제 프로젝트 폴더(`../{프로젝트명}/`)로 이동하여 개발을 시작하시면 됩니다.
체크리스트(킥오프 문서 섹션 6)를 확인하면서 진행하세요.

### 📐 설계 문서 작성 (선택)

킥오프 문서(섹션 1-8)가 완료되었습니다.
추가로 설계 문서(섹션 9-12)를 작성하면 개발 전에 요구사항과 아키텍처를 정리할 수 있습니다.

| # | 설계 스킬 | 추가 섹션 | 설명 |
|---|---|---|---|
| 1 | /design-requirements | 섹션 9 | 기능/비기능 요구사항, 사용자 흐름 |
| 2 | /design-architecture | 섹션 10 | 시스템 구조, 기술 선택 근거, 배포 |
| 3 | /design-data-model | 섹션 11 | 데이터 스키마, 타입 정의, 정합성 규칙 |
| 4 | /design-ai-workflow | 섹션 12 | AI I/O, 프롬프트, 모델, 폴백 (AI 프로젝트만) |

**선택:**
1. 설계 시작 → /design-requirements부터 순서대로
2. 바로 개발 시작 (설계 스킵)
```

---

## 실패 처리

| 실패 유형 | 처리 방법 |
|---|---|
| gh CLI 미설치 | 설치 안내 + 패스 허용 |
| gh 인증 실패 | `gh auth login` 안내 |
| 레포 접근 불가 (private/삭제) | 에러 메시지 + 수동 복사 안내 |
| 네트워크 오류 | 재시도 안내 + 패스 허용 |
| 프로젝트 폴더 없음 | `/kickoff-start`를 먼저 실행하도록 안내 (폴더는 start에서 생성) |

---

## 주의사항

- 스킬은 **프로젝트 폴더**에 설치, 하네스 폴더에 설치하지 않음
- 하네스의 kickoff-* 스킬은 복사 대상이 아님 (개발 스킬만 복사)
- 패스 시에도 킥오프 자체는 완료로 처리 (스킬은 나중에 수동 설치 가능)
- 임시 클론 디렉토리는 반드시 정리
