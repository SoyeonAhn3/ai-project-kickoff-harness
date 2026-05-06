# Backlog

하네스 개선/수정 사항을 관리하는 목록. 각 항목에 결정 배경을 포함한다.

---

## 대기 중

### BL-001: State 파일 슬림화

**상태**: 대기 (Phase 8~10 구현 시 반영)
**등록일**: 2026-05-06

**내용**: kickoff-profile 실행 후 state 섹션 2~4를 상태 요약으로 슬림화하는 단계 추가

**배경**: kickoff_state.md와 kickoff 문서의 내용이 약 80% 중복됨. state는 인터뷰 답변 전체를 담고 있고, kickoff 문서는 같은 내용을 구조화해서 다시 담고 있음. 두 파일을 동시에 유지보수하는 부담이 있고, 어느 쪽이 최신인지 혼란 가능.

**해결 방향**:
- profile 생성 전: state가 유일한 저장소 → 인터뷰 답변 유지 (변경 없음)
- profile 생성 후: state 섹션 2~4를 상태만 남기고 슬림화, 상세는 kickoff 문서 참조
- 원칙: state = 진행 추적기, kickoff 문서 = 콘텐츠 단일 출처

**영향 범위**:
| 파일 | 변경 | 이유 |
|---|---|---|
| kickoff-profile SKILL.md | 슬림화 단계 추가 | 전환점 역할 |
| kickoff-gap SKILL.md | state 섹션 형식 축소 | 중복 제거 |
| Phase 8~10 신규 스킬 | 처음부터 슬림 패턴 적용 | 신규이므로 바로 적용 |
| kickoff-interview SKILL.md | 변경 없음 | profile 전이라 전체 저장 필요 |
| kickoff-suggest SKILL.md | 변경 없음 | 같은 이유 |
| kickoff-checklist SKILL.md | 변경 없음 | 이미 슬림 |

### BL-002: 스킬 소스를 GitHub Skill_package로 통일

**상태**: 대기
**등록일**: 2026-05-06

**내용**: kickoff 스킬들을 Skill_package 레포에 추가하여, 어떤 프로젝트에서든 gh CLI로 전체 스킬(기본 7개 + kickoff 스킬)을 설치할 수 있게 함

**배경**: 현재 kickoff 스킬은 이 레포 로컬에만 존재. 다른 사람이 하네스를 사용하려면 이 레포를 통째로 클론해야 하고, 로컬 경로(OneDrive 등)에 의존적. gh CLI 기반 fetch가 이식성이 훨씬 좋음.

**해결 방향**:
- Skill_package 레포에 kickoff-* 스킬들을 추가
- kickoff-skills SKILL.md의 fetch 목록에 kickoff 스킬도 포함 (또는 별도 bootstrap 명령)
- 이 레포는 "하네스 소스 + 설계 문서" 역할, Skill_package는 "배포 채널" 역할

**구조 예시**:
```
Skill_package/.claude/skills/
├── dev-log/              # 기존 기본 7개
├── github-push/
├── ...
├── kickoff-context/      # kickoff 스킬 추가
├── kickoff-start/
├── kickoff-interview/
├── kickoff-suggest/
├── kickoff-profile/
├── kickoff-gap/
├── kickoff-checklist/
└── kickoff-skills/
```

**영향 범위**:
| 대상 | 변경 | 이유 |
|---|---|---|
| Skill_package 레포 | kickoff-* 폴더 추가 | 배포 채널 역할 |
| kickoff-skills SKILL.md | fetch 대상에 kickoff 스킬 포함 여부 결정 | 부트스트랩 방식 |
| README | 설치 방법을 "gh에서 fetch"로 통일 | 이식성 |

---

## 완료

(아직 없음)
