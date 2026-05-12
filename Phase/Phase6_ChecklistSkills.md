# Phase 6 — ChecklistSkills `Done`

> Dev checklist generation skill + GitHub skill fetch skill

**Status**: Done
**Prerequisites**: Phase 5

---

## Overview

Two finishing skills for the kickoff flow:
- **kickoff-checklist**: Reads the kickoff document and auto-generates a development readiness checklist (section 6).
- **kickoff-skills**: After user confirmation, copies 7 base dev skills from GitHub Skill_package to the project folder.

---

## Deliverables

| # | Skill / Module | Status | Skill Type |
|---|---|---|---|
| 1 | `kickoff-checklist` SKILL.md | Done | project-specific |
| 2 | `kickoff-skills` SKILL.md | Done | project-specific |
| 3 | gh CLI copy logic | Done | - |
| 4 | gh not-installed handling | Done | - |
| 5 | Functional test | Done | Verified in Phase 7 integration test |

---

## kickoff-checklist

### Purpose

Auto-generate a pre-development checklist from the kickoff profile, so nothing is forgotten before coding begins.

### Implementation Files

```
.claude/skills/kickoff-checklist/
└── SKILL.md
```

No references needed (checklist is dynamically generated from profile content).

### Core Behavior

1. Read `pre-requirement/project_kickoff.md`
2. Extract checklist items from profile content:
   - Tech stack -> installation / environment verification items
   - Data sources -> access / API key verification items
   - External services -> account / auth verification items
   - Design structure -> schema / config finalization items
3. Append "## 6. Dev Checklist" section to project_kickoff.md

---

## kickoff-skills

### Purpose

Copy 7 base Claude skills from the GitHub Skill_package repository to the newly created project folder after kickoff completion.

### Implementation Files

```
.claude/skills/kickoff-skills/
└── SKILL.md
```

### Core Behavior

1. Ask user: "Copy skills to your project?" (all / select / pass)
2. Check gh CLI installation
   - Not installed: show guidance -> user chooses "install" or "pass"
3. Verify GitHub Skill_package access (`https://github.com/SoyeonAhn3/Skill_package.git`)
4. Sparse clone and copy 7 base skills:
   - dev-log, github-push, phase-doc, readme-gen, gen-manual, skill-template, test-scenario
5. Place in project folder (`../{project-name}/.claude/skills/`)
6. Suggest optional skills based on project type
7. Report results

### Design Decisions

| Decision | Detail | Reason |
|---|---|---|
| Install location | Project folder (`../{project-name}/.claude/skills/`) | Separate harness from project (BL-002) |
| User confirmation | "Copy skills?" prompt first | Prevent forced install, allow pass |
| Copy method | gh CLI sparse clone of specific folders | Symlinks break across environments |
| gh not-installed | Guidance + allow pass | No forced install, user decides |
| Base 7 fixed | Always for every project | Defined in Plan.txt |
| Optional extras | Suggested by project type, user confirms | Avoid forcing unnecessary skills |

---

## Prerequisites & Dependencies

- Phase 5 complete (kickoff-checklist needs project_kickoff.md)
- gh CLI installed (kickoff-skills; pass allowed if missing)
- skill-template structure reference

---

## Development Notes

- Do not overwrite existing skills when copying base 7 -- ask "overwrite?" on conflict
- User confirmation required before any file operations
- Provide clear error messages for gh auth failures

---

## Change Log

| Date | Description |
|---|---|
| 2026-05-04 | Initial creation |
| 2026-05-06 | Status update: implementation complete (Phase 7 integration test passed) |
| 2026-05-07 | BL-002 reflected: skill install location changed to project folder, "copy?" confirmation added |

---
---

# Phase 6 — 체크리스트 + 스킬 복사 `완료`

> 체크리스트 생성 스킬과 GitHub 스킬 가져오기 스킬 개발

**상태**: 완료
**선행 조건**: Phase 5 완료

---

## 개요

두 개의 마무리 스킬을 개발한다:
- **kickoff-checklist**: project_kickoff.md에 개발 착수 체크리스트(섹션 6) 추가
- **kickoff-skills**: 킥오프 완료 후 "스킬도 복사할까요?" 확인 후 프로젝트 폴더에 dev 스킬 복사

---

## 완료 예정 / 완료 항목

| # | Skill / 모듈 | 상태 | 스킬 타입 |
|---|---|---|---|
| 1 | `kickoff-checklist` SKILL.md 작성 | 완료 | project-specific |
| 2 | `kickoff-skills` SKILL.md 작성 | 완료 | project-specific |
| 3 | gh CLI 스킬 복사 로직 구현 | 완료 | - |
| 4 | gh 미설치/미인증 시 대응 로직 | 완료 | - |
| 5 | 동작 테스트 | 완료 | Phase 7 통합 테스트에서 검증 |

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

1. `pre-requirement/project_kickoff.md`를 Read
2. 프로필 내용에서 체크리스트 항목 추출:
   - 기술 스택 -> 설치/환경 확인 항목
   - 데이터 소스 -> 접근/API 키 확인 항목
   - 외부 서비스 -> 계정/인증 확인 항목
   - 설계 구조 -> 스키마/설정 확정 항목
3. project_kickoff.md 하단에 "## 6. 개발 착수 체크리스트" 섹션 추가

---

## kickoff-skills

### 목적

킥오프 완료 후, 개발에 필요한 기본 Claude 스킬 세트를 GitHub Skill_package에서 가져와 **새로 생성된 프로젝트 폴더**에 배치한다.

### 구현 파일

```
.claude/skills/kickoff-skills/
└── SKILL.md
```

### 핵심 동작

1. "스킬도 복사할까요?" 사용자 확인 (전체/선택/패스)
2. gh CLI 설치 확인
   - 미설치 시: 안내 메시지 -> 사용자가 "설치" 또는 "패스" 선택
3. GitHub Skill_package 접근 확인 (`https://github.com/SoyeonAhn3/Skill_package.git`)
4. 기본 7개 스킬 폴더를 복사:
   - dev-log, github-push, phase-doc, readme-gen, gen-manual, skill-template, test-scenario
5. **프로젝트 폴더**(`../{프로젝트명}/.claude/skills/`)에 배치
6. 프로젝트 유형에 따라 선택적 스킬 추가 여부 확인
7. 완료 보고

### 설계 결정 사항

| 결정 | 내용 | 이유 |
|---|---|---|
| 설치 위치 | 프로젝트 폴더(`../{프로젝트명}/.claude/skills/`) | 하네스와 프로젝트 분리 (BL-002) |
| 사용자 확인 | "스킬도 복사할까요?" 먼저 확인 | 강제 설치 방지, 패스 허용 |
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

## 주의사항

- kickoff-checklist: 기존 kickoff-* 스킬들이 이미 .claude/skills/에 있으므로 기본 7개 복사 시 덮어쓰지 않도록 주의
- kickoff-skills: 이미 같은 이름의 스킬이 있으면 "덮어쓸까요?" 확인
- gh 인증 실패 시 명확한 에러 메시지 제공

---

## 변경 이력

| 날짜 | 내용 |
|---|---|
| 2026-05-04 | 최초 작성 |
| 2026-05-06 | 상태 갱신: 구현 완료 반영 (Phase 7 통합 테스트 통과 확인) |
| 2026-05-07 | BL-002 반영: 스킬 설치 위치를 프로젝트 폴더로 변경, "복사할까요?" 확인 추가 |
