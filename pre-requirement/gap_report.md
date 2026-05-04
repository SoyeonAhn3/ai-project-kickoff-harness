# Gap Report — 누락/모순 점검 결과

## 모순 (해결됨)

| # | 문제 | 해결 |
|---|---|---|
| 1 | Plan.txt에서 `project_profile.json`으로 표기 | Markdown으로 확정. Plan.txt 수정 필요 |
| 2 | README.md가 MVP 산출물에 포함되어 있었음 | MVP에서 제외. v2에서 readme-gen 스킬로 생성 |

## 누락 (해결됨)

| # | 문제 | 결정 |
|---|---|---|
| 3 | 다른 CLI(Codex, Gemini) 지원 방식 미정 | Claude Code Skill로만 만들고, 나머지 CLI는 v2에서 결정 |
| 4 | gh CLI 미설치/미인증 시 처리 | 미설치 안내 → 사용자가 설치 또는 패스 선택 |
| 5 | pre-requirement/와 .claude/skills/ 위치 관계 | 기획 산출물은 pre-requirement/, 스킬은 .claude/skills/ (프로젝트 루트). 각자 역할이 다름 |
| 6 | 하네스 자체 구조 | 단계별 분리된 스킬 (kickoff-interview, kickoff-profile, kickoff-gap 등) |

## 잔여 미정 사항 (v2 이후)

| 항목 | 비고 |
|---|---|
| 인터뷰 종료 조건 | 차후 설계 |
| 유형별 질문 템플릿 매핑 | 차후 설계 |
| Codex/Gemini CLI 지원 방식 | v2에서 결정 |
| README 자동 생성 | v2에서 readme-gen 스킬로 |

## Plan.txt 수정 필요 사항

- `project_profile.json` → `project_profile.md`로 변경
- MVP 산출물에서 README.md 제거
- 하네스 구조: 단계별 분리 스킬임을 명시
- 다른 CLI 지원: v2로 이동 명시
