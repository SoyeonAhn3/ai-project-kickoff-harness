# Project Profile

## 기본 정보

| 항목 | 내용 |
|---|---|
| 프로젝트명 | AI Project Kickoff Harness |
| 목적 | 막연한 아이디어를 구체적 기획으로 전환하고, 누락/모순을 잡아 개발 착수 가능한 상태를 만드는 자동화 시스템 |
| 유형 | CLI 도구 / 자동화 오케스트레이터 |
| 주요 사용자 | 본인 (+ GitHub 공개로 외부 사용자도 가능) |
| 실행 환경 | Claude CLI, Codex CLI, Gemini CLI, VS Code Terminal |

## 핵심 기능

| 기능 | 설명 |
|---|---|
| 아이디어 입력 | 자유 텍스트 형식, 한/영 지원. 사용자가 참고 문서를 언급하면 함께 참고 |
| 유형 판별 | 입력 기반으로 프로젝트 유형 자동 분류 |
| 요구사항 인터뷰 | 묶음 질문 + 부족 시 추가 질문. 사소한 것은 묻지 않음 |
| 프로필 생성 | 인터뷰 결과를 구조화된 Markdown 기준 문서로 생성 |
| 누락/모순 점검 | 명확한 모순/오류만 잡고, 애매한 건 사용자에게 결정 위임 |
| 체크리스트 생성 | 개발 착수 전 확인 항목 자동 생성 |
| 스킬 세팅 | GitHub Skill_package에서 기본 7개 스킬을 복사 방식으로 가져옴 |

## 기술 스택

| 기술 | 역할 |
|---|---|
| Claude Code Skill | 하네스 본체 (오케스트레이터) |
| Markdown | 산출물 포맷 |
| Git / GitHub | 스킬 배포, 프로젝트 공유 |
| gh CLI | Skill_package에서 스킬 가져오기 |

## 데이터 구조

| 입력 | 출력 |
|---|---|
| 사용자 자유 텍스트 (아이디어) | project_profile.md |
| 사용자 인터뷰 답변 | gap_report.md |
| (선택) 참고 문서 | dev_checklist.md |
| | README.md |
| | .claude/skills/* (기본 7개) |

## 산출물 저장 위치

- 경로: `{현재 디렉토리}/pre-requirement/`
- 폴더 없으면 자동 생성, 있으면 기존 폴더에 저장

## 스킬 세팅 방식

- 소스: GitHub Skill_package 저장소
- 방식: sparse-checkout 또는 gh CLI로 필요한 스킬 폴더만 복사
- 기본 7개: dev-log, github-push, phase-doc, readme-gen, gen-manual, skill-template, test-scenario
- 선택적 추가: ai-multi-discussion, interview-prep, readme-update (유형에 따라 사용자 확인)
- 버전: tag/commit 지정 (pinned) 또는 latest 중 사용자 선택

## 제약사항

| 항목 | 내용 |
|---|---|
| 오프라인 | 미지원 (GitHub 접근 필요) |
| 시간 | 1시간 이내 완료 목표 |
| 외부 API | 사용자 요구 시에만 (웹검색, 기술스택 추천 등) |
| 인터뷰 상한 | 없음. 단, 사소한 디테일은 묻지 않음 |

## 리스크

| 리스크 | 대응 |
|---|---|
| Skill_package 구조 변경 시 경로 깨짐 | tag/commit pinning |
| GitHub 접근 불가 | 스킬 세팅 건너뜀 안내 후 계속 진행 |
| 인터뷰 종료 시점 불명확 | 차후 종료 조건 설계 (미정) |
| 유형별 질문 분기 미설계 | 차후 템플릿 매핑 (미정) |

## 개발 로드맵

- MVP: 1→2→3→4→5→8→9 (프로필, 점검, 체크리스트, 스킬세팅)
- v2: 6→7 추가 (Phase 생성, 문서 7종 자동 생성)
