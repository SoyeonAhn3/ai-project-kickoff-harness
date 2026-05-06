# Phase 6 — kickoff-checklist + kickoff-skills 개발 `✅ 완료`

> 체크리스트 생성 스킬과 GitHub 스킬 가져오기 스킬 개발

**상태**: ✅ 완료
**선행 조건**: Phase 5 완료

---

## 개요

두 개의 마무리 스킬을 개발한다:
- kickoff-checklist: project_kickoff.md에 개발 착수 체크리스트(섹션 6) 추가
- kickoff-skills: GitHub Skill_package에서 기본 7개 스킬을 가져와 .claude/skills/에 배치

---

## 완료 예정 / 완료 항목

| # | Skill / 모듈 | 상태 | 스킬 타입 |
|---|---|---|---|
| 1 | `kickoff-checklist` SKILL.md 작성 | ✅ | project-specific |
| 2 | `kickoff-skills` SKILL.md 작성 | ✅ | project-specific |
| 3 | gh CLI 스킬 복사 로직 구현 | ✅ | - |
| 4 | gh 미설치/미인증 시 대응 로직 | ✅ | - |
| 5 | 동작 테스트 | ✅ | Phase 7 통합 테스트에서 검증 |

---

## kickoff-checklist

### 목적

project_kickoff.md의 프로필/아키텍처 내용을 기반으로 개발 착수 전 확인 항목을 자동 생성한다.

### 구현 파일

```
.claude/skills/kickoff-checklist/
└── SKILL.md
```

references 불필요 (체크리스트는 프로필 내용에서 동적 생성)

### 핵심 동작

1. pre-requirement/project_kickoff.md를 Read
2. 프로필 내용에서 체크리스트 항목 추출:
   - 기술 스택 → 설치/환경 확인 항목
   - 데이터 소스 → 접근/API 키 확인 항목
   - 외부 서비스 → 계정/인증 확인 항목
   - 설계 구조 → 스키마/설정 확정 항목
3. project_kickoff.md 하단에 "## 6. 개발 착수 체크리스트" 섹션 추가

---

## kickoff-skills

### 목적

개발에 필요한 기본 Claude 스킬 세트를 GitHub Skill_package에서 가져와 프로젝트에 배치한다.

### 구현 파일

```
.claude/skills/kickoff-skills/
└── SKILL.md
```

### 핵심 동작

1. gh CLI 설치 확인
   - 미설치 시: 안내 메시지 → 사용자가 "설치" 또는 "패스" 선택
   - 패스 시: 스킬 세팅 건너뜀 안내 후 종료
2. GitHub Skill_package 접근 확인 (https://github.com/SoyeonAhn3/Skill_package.git)
3. 기본 7개 스킬 폴더를 복사:
   - dev-log, github-push, phase-doc, readme-gen, gen-manual, skill-template, test-scenario
4. .claude/skills/에 배치
5. 프로젝트 유형에 따라 선택적 스킬 추가 여부 확인:
   - ai-multi-discussion, interview-prep, readme-update
6. 완료 보고

### 설계 결정 사항

| 결정 | 내용 | 이유 |
|---|---|---|
| 복사 방식 | gh CLI로 특정 폴더만 가져오기 | 심링크는 다른 환경에서 깨짐 |
| gh 미설치 대응 | 안내 + 패스 허용 | 강제 설치 없이 사용자 결정 |
| 기본 7개 고정 | 모든 프로젝트에 무조건 | Plan.txt에서 확정 |
| 선택적 추가 | 유형에 따라 사용자 확인 | 불필요한 스킬 강제 방지 |

---

## 선행 조건 및 의존성

- Phase 5 완료 (kickoff-checklist: project_kickoff.md 필요)
- gh CLI 설치 (kickoff-skills: 없으면 패스 가능)
- skill-template 구조 참고

---

## 개발 시 주의사항

- kickoff-checklist: 기존 kickoff-* 스킬들이 이미 .claude/skills/에 있으므로, 기본 7개 복사 시 덮어쓰지 않도록 주의
- kickoff-skills: 이미 같은 이름의 스킬이 있으면 "덮어쓸까요?" 확인
- gh 인증 실패 시 명확한 에러 메시지 제공

---

## 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026-05-04 | 최초 작성 |
| 2026-05-06 | 상태 갱신: 구현 완료 반영 (Phase 7 통합 테스트 통과 확인) |
