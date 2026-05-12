# Backlog

하네스 개선/수정 사항을 관리하는 목록. 각 항목에 결정 배경을 포함한다.

---

## 대기 중

## 완료

### BL-016: 킥오프 시작 시 언어 선택 (한국어/영어)

**상태**: ✅ 완료
**등록일**: 2026-05-12
**완료일**: 2026-05-12

**내용**: kickoff-start 첫 단계에서 언어를 선택하고, 이후 모든 스킬의 산출물이 선택된 언어로 출력되도록 변경. 최소 접근법 (2개 파일).

**배경**: 영어권 사용자 또는 영문 포트폴리오 용도로 킥오프 문서를 영어로 생성하고 싶은 니즈.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| kickoff-start SKILL.md | STEP 1에 언어 선택 추가, 출력 템플릿 이중 언어화, YAML frontmatter에 `language` 필드 | ✅ 반영 |
| profile-template.md | YAML frontmatter에 `language` 필드 추가, 작성 규칙 6을 frontmatter 기반으로 변경 | ✅ 반영 |

---

### BL-014: evaluate 스킬에 scope 변경 시 문서 연쇄 갱신 체크리스트 추가

**상태**: ✅ 완료
**등록일**: 2026-05-12
**완료일**: 2026-05-12

**내용**: kickoff-evaluate STEP 4에 "문서 연쇄 갱신" 서브스텝 추가. 기능이 MVP ↔ v2로 이동할 때 영향받는 6개 필드를 순회하여 불일치를 수정한다.

**배경**: finance_data_platform 통합테스트에서 8개 모순 중 3개가 evaluate의 scope 변경 후 관련 필드를 갱신하지 않아 발생.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| kickoff-evaluate SKILL.md | STEP 4에 "조정 후 문서 연쇄 갱신" 섹션 추가 (6개 필드 체크리스트 + 수행 순서 + 점검 범위 판단) | ✅ 반영 |

### BL-015: gap/checklist 스킬을 체인 맨 끝으로 이동 + v2 정합성 카테고리 추가

**상태**: ✅ 완료
**등록일**: 2026-05-12
**완료일**: 2026-05-12

**내용**: 스킬 체인 구조 변경 + gap-rules 확장
- **(1) 체인 구조 변경**: gap/checklist를 profile 후(이전) → 체인 맨 끝(변경)으로 이동
  - v1 경로: start → interview → suggest → profile → evaluate → done → **gap → checklist**
  - v2 경로: ... → done → design-requirements → ... → design-ai-workflow → **gap → checklist**
- **(2) gap depends_on 변경**: kickoff-profile → **kickoff-done** (최소), design-ai-workflow(v2 시)
- **(3) gap-rules.md에 카테고리 7 추가** (v2 설계 섹션 교차 정합성):
  - 7-1: NFR 수치 vs 제약사항 산술 검증
  - 7-2: 사용자 흐름 vs 아키텍처 진입점/순서
  - 7-3: 아키텍처 통신 vs 데이터 모델 저장소, ADR vs 생명주기
  - 7-4: v1 섹션(실패 시나리오 등) vs v2 섹션(FR 에러 처리 등)
- **(4) checklist 확장**: v2 섹션(9-12) 존재 시 프로젝트 구조 트리 + .env.example 생성

**배경**: finance_data_platform 통합테스트에서 8개 모순 중 5개가 v2 스킬 간 교차 갱신 부재로 발생. gap/checklist를 최종 관문으로 이동하면 전체 문서의 정합성을 한 번에 검증 가능.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| gap-rules.md | 카테고리 7 (v2 교차 정합성 4개 하위 규칙) 추가, 점검 범위 조건 재구성 | ✅ 반영 |
| kickoff-gap SKILL.md | v2.0 — depends_on: kickoff-done, 7개 카테고리, v2 미수행 시 건너뜀 | ✅ 반영 |
| kickoff-checklist SKILL.md | v2 시스템 구조/기술 선택/엔티티 추출 추가, v2 프로젝트 구조 + .env 생성 | ✅ 반영 |

---

### BL-013: design-impl-spec 삭제 → checklist에 프로젝트 구조/.env 흡수

**상태**: ✅ 완료
**등록일**: 2026-05-12
**완료일**: 2026-05-12

**결정**: checklist에 흡수 — design-impl-spec 스킬 삭제, 프로젝트 구조(13-1)와 환경 설정(13-2)을 checklist 스킬(섹션 6)의 서브섹션으로 이동. v2 디자인 체인 5→4 스킬로 감소.

**배경**: finance_data_platform 통합테스트에서 발견. 섹션 13의 컴포넌트 상세/의존성이 섹션 10-1, 10-2와 70~80% 중복. BL-015와 결합하여 checklist가 전체 섹션을 참조 가능.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| design-impl-spec/ | SKILL.md + references/impl-spec-template.md 삭제 | ✅ 삭제 |
| design-ai-workflow SKILL.md | 다음 단계: /kickoff-gap → /kickoff-checklist로 변경 | ✅ 반영 |
| design-ai-workflow references | ai-workflow-template.md 비AI 스킵 안내 변경 | ✅ 반영 |
| design-data-model SKILL.md | 다음 단계 안내에서 design-impl-spec 제거 | ✅ 반영 |
| kickoff-skills SKILL.md | v2 설계 스킬 테이블에서 design-impl-spec 행 제거, 4종으로 변경 | ✅ 반영 |
| profile-template.md | 섹션 13 플레이스홀더 제거, 섹션 6에 v2 안내 추가, 규칙 9 섹션 범위 조정 | ✅ 반영 |
| README.md / README_ko.md | 설계 문서 5종 → 4종, design-impl-spec 행 제거 | ✅ 반영 |

### BL-012: 외부 의존성 배포 환경 리스크 탐지 추가

**상태**: ✅ 완료
**등록일**: 2026-05-08
**완료일**: 2026-05-08

**내용**: (1) gap-rules.md 카테고리 2에 비공식 API/스크래핑 의존 시 클라우드 배포 환경 리스크 경고 규칙 추가, (2) kickoff-checklist에 gap에서 배포 리스크가 발견된 경우 PoC 및 Fallback 확보 체크항목 조건부 생성

**배경**: 실제 프로젝트(주식 데이터 대시보드)에서 yfinance의 `stock.info`가 로컬에서는 정상 동작하지만 클라우드(Render) 배포 시 Yahoo Finance의 데이터센터 IP 차단으로 실패. 인터뷰에서 데이터 소스와 기술 스택은 이미 수집하고 있으므로, 추가 질문 없이 gap이 수집된 정보에서 리스크를 탐지하고 checklist가 실행 항목을 생성하는 방식으로 해결.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| gap-rules.md | 카테고리 2에 "배포 환경 접근 제한 리스크" + "Fallback 미정의" 하위 규칙 추가 | ✅ 반영 |
| kickoff-checklist SKILL.md | 외부 서비스 영역에 gap 배포 리스크 연동 조건부 항목 추가 (PoC + Fallback) | ✅ 반영 |

---

### BL-011: BI 대시보드 키워드 "차트" 오판별 수정

**상태**: ✅ 완료
**등록일**: 2026-05-07
**완료일**: 2026-05-07

**내용**: project-types.md의 BI 대시보드 키워드에서 "차트"를 "데이터 차트, 분석 차트"로 좁혀 다이어그램/플로우차트와의 오판별 방지

**배경**: workflow_process_manager 테스트에서 발견. "workflow 차트"가 BI 대시보드의 "차트" 키워드에 매칭되어 부가 유형이 BI로 잘못 판별됨. "차트"는 데이터 시각화 차트와 프로세스 다이어그램을 구분하지 못하는 너무 넓은 키워드.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| references/project-types.md | BI 키워드 "차트" → "데이터 차트, 분석 차트"로 변경 | ✅ 반영 |

---

### BL-010: 기술 스택 미정 레이어 확인 규칙 추가

**상태**: ✅ 완료
**등록일**: 2026-05-07
**완료일**: 2026-05-07

**내용**: kickoff-interview STEP 4에서 기술 스택 테이블에 "미정" 항목이 남아있으면 사용자에게 확인하거나 AI 추천을 제시하는 규칙 추가

**배경**: workflow_process_manager 테스트에서 발견. 사용자가 AI/차트만 지정하고 프론트/백엔드/DB는 언급하지 않았는데, 추가 질문 없이 "미정"으로 넘어감. 인터뷰에 레이어별 기술 스택을 순회하며 확인하는 단계가 없었음.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| kickoff-interview SKILL.md | STEP 4 항목 4에 미정 레이어 확인 → 추천 제안 규칙 추가 | ✅ 반영 |

---

### BL-009: MVP 채택 AI 제안이 핵심 기능 테이블에 자동 반영되지 않음

**상태**: ✅ 완료
**등록일**: 2026-05-07
**완료일**: 2026-05-07

**내용**: kickoff-suggest에서 MVP로 채택된 아이디어가 핵심 기능 테이블에 자동 추가되는 규칙 추가

**배경**: workflow_process_manager 테스트에서 발견. MVP로 채택된 제안 3건이 `### 채택된 AI 제안` 테이블에만 기록되고 `### 핵심 기능` 테이블에는 추가되지 않아, kickoff-gap에서 매번 교차 일관성 누락으로 잡힘.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| kickoff-suggest SKILL.md | STEP 4에 MVP 채택 항목 → 핵심 기능 테이블 자동 추가 규칙 추가 | ✅ 반영 |
| kickoff-suggest SKILL.md | 출력 형식 섹션에 핵심 기능 테이블 연동 명시 | ✅ 반영 |

---

### BL-007: "주요 사용자" 표기 분리 (internal vs presentation)

**상태**: ✅ 완료
**등록일**: 2026-05-07
**완료일**: 2026-05-07

**내용**: 킥오프 문서의 사용자/대상 표기를 내부 기록용과 외부 노출용으로 분리

**배경**: 포트폴리오 목적의 프로젝트에서 "주요 사용자: 본인 (학습용)"이라고 표기하면, GitHub README나 이력서에 그대로 들어갔을 때 채용 어필이 안 됨. readme-gen 등 후속 스킬이 외부 표기용 사용자를 참조하면 자연스럽게 해결.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| references/profile-template.md | 기본 정보에 "주요 사용자 (내부)" / "주요 사용자 (외부 표기)" 행 분리 | ✅ 반영 |
| kickoff-interview SKILL.md | P1-b 질문 추가 (포트폴리오 목적 시 조건부), STEP 4 기본 정보 매핑에 P1-b 추가 | ✅ 반영 |
| kickoff-profile SKILL.md | STEP 2 품질 검토에 외부 표기 톤 점검 항목 추가 | ✅ 반영 |
| kickoff-done SKILL.md | 데모 기준 생성 시 "주요 사용자 (외부 표기)" 참조 규칙 추가 | ✅ 반영 |
| Skill_package readme-gen | 외부 레포 — 향후 별도 반영 필요 | ⏳ 보류 |

---

### BL-003: 설계 인터뷰 중복 질문 제거

**상태**: ✅ 완료
**등록일**: 2026-05-07
**완료일**: 2026-05-07

**내용**: 설계 인터뷰(STEP 3)가 기획 인터뷰에서 이미 수집된 내용을 다시 묻는 문제 수정

**배경**: 통합 테스트(finance_data_platform)에서 발견. 기획 인터뷰에서 파이프라인 구조, 데이터 소스, 볼륨 등을 이미 답변했는데, 설계 인터뷰가 같은 질문을 반복함.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| kickoff-interview SKILL.md | STEP 3 상단에 중복 제거 규칙 + 영역별 기획 답변 대응표 추가 | ✅ 반영 |
| references/design-questions.md | 각 영역에 "기획 답변 중복 확인" 분기 규칙 (충분/부분/없음) 추가 | ✅ 반영 |

---

### BL-008: MVP 항목 교차 일관성 검증 — gap 규칙 보강 + 핵심 기능 행 분리

**상태**: ✅ 완료
**등록일**: 2026-05-07
**완료일**: 2026-05-07

**내용**: (1) gap 카테고리 5에 양방향 교차 검증 규칙 추가, (2) 핵심 기능 표에서 필수/선택 행 분리 규칙 추가

**배경**: 핵심 기능/외부 의존성/완료 조건 세 섹션이 서로 다른 필수/선택 분류를 하는데 gap이 잡지 못함.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| gap-rules.md | 카테고리 5에 양방향 교차 일관성 점검 (기능↔의존성↔완료 조건) 추가 | ✅ 반영 |
| profile-template.md | 핵심 기능 표에 행 분리 규칙 + 예시 추가 | ✅ 반영 |
| kickoff-interview SKILL.md | STEP 4 핵심 기능 테이블 작성 시 행 분리 규칙 참조 추가 | ✅ 반영 |
| kickoff-done SKILL.md | MVP 범위 작성 규칙에 "⬜ 선택" 제외 명시 | ✅ 반영 |
| kickoff-checklist SKILL.md | MVP 기능 추출 시 "⬜ 선택" 항목 제외 명시 | ✅ 반영 |

---

### BL-006: MVP 축소 시 프로젝트 유형 재판별

**상태**: ✅ 완료
**등록일**: 2026-05-07
**완료일**: 2026-05-07

**내용**: kickoff-evaluate에서 MVP 범위 조정 시 프로젝트 유형을 재판별하고, 킥오프 문서의 유형 정보를 연동 갱신하는 로직 추가

**배경**: finance_data_platform 테스트에서 Text-to-SQL(AI 핵심 기능)이 v2로 밀렸지만, 부가 유형이 "AI 프로젝트"로 유지됨.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| kickoff-evaluate SKILL.md | STEP 4에 유형 재판별 트리거 추가 | ✅ BL-005와 함께 반영 |
| kickoff-evaluate SKILL.md | STEP 4에 유형 변경 시 킥오프 문서 `### 기본 정보` 갱신 규칙 + 연쇄 영향 안내 추가 | ✅ 반영 |

---

### BL-004: State 파일 제거 및 킥오프 문서 직접 업데이트 방식 전환

**상태**: ✅ 완료
**등록일**: 2026-05-07
**완료일**: 2026-05-07

**내용**: kickoff_state.md를 제거하고, 킥오프 문서를 kickoff-start 시점에 생성하여 각 스킬이 직접 업데이트하는 방식으로 전환. YAML frontmatter `last_skill` 필드로 진행 추적.

**배경**: state 파일에 인터뷰 내용을 전체 저장 → kickoff 문서에 복사 → state 간소화(BL-001)라는 불필요한 3단계 순환 제거. 킥오프 문서가 Single Source of Truth.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| kickoff-start SKILL.md | 프로젝트 폴더 + 킥오프 문서(YAML frontmatter) 생성 | ✅ 반영 |
| kickoff-interview SKILL.md | 킥오프 문서 Section 1, 2-4 직접 Edit | ✅ 반영 |
| kickoff-suggest SKILL.md | 킥오프 문서 `### 채택된 AI 제안` 직접 Edit | ✅ 반영 |
| kickoff-profile SKILL.md | "생성" → "최종 검토/정리"로 역할 전환 (v2.0) | ✅ 반영 |
| kickoff-gap SKILL.md | Glob 탐색 + frontmatter 확인으로 전환 | ✅ 반영 |
| kickoff-checklist SKILL.md | state 갱신 → frontmatter 갱신으로 전환 | ✅ 반영 |
| kickoff-evaluate SKILL.md | state 갱신 → frontmatter 갱신으로 전환 | ✅ 반영 |
| kickoff-done SKILL.md | state 갱신 → frontmatter 갱신으로 전환 | ✅ 반영 |
| kickoff-skills SKILL.md | state 탐색 → Glob + frontmatter로 전환 | ✅ 반영 |
| kickoff-context SKILL.md | 핸드오프 설명을 킥오프 문서 `### 프로젝트 배경`으로 변경 | ✅ 반영 |
| propagation-guide.md | 읽기 위치를 킥오프 문서로 변경 | ✅ 반영 |
| profile-template.md | YAML frontmatter + 플레이스홀더 표준 구조 추가 | ✅ 반영 |

---

### BL-005: 차별화 평가 기준 강화 및 MVP 변경 시 재평가 연동

**상태**: ✅ 완료
**등록일**: 2026-05-07
**완료일**: 2026-05-07

**내용**: (1) kickoff-evaluate STEP 4에 조정 후 영향 차원 재평가 루프 추가, (2) 차별화 기준에 MVP 축소 후 범람 체크 필수화

**배경**: finance_data_platform 테스트에서 두 가지 문제 발견. 첫째, Text-to-SQL이 v2로 이동한 후 차별화가 재평가되지 않음(구조 문제). 둘째, "End-to-End 범위 자체가 차별점"이라는 판단으로 🟡가 나왔지만, 실제로는 GitHub에 유사 프로젝트가 다수 존재하여 🔴에 가까움(기준 문제). 재평가 트리거만 추가하면 같은 관대한 기준이 다시 적용될 수 있어, 기준 보강도 함께 필요.

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| kickoff-evaluate SKILL.md | STEP 4에 조정 후 영향 차원 재평가 + 유형 재판별 트리거 추가 | ✅ 반영 |
| references/evaluation-criteria.md | 차원 1 차별화에 "MVP 축소 후 범람 체크" 필수 점검 추가 | ✅ 반영 |

---

### BL-002: 프로젝트 폴더 분리 및 스킬 배포 방식 변경

**상태**: ✅ 완료
**등록일**: 2026-05-06
**완료일**: 2026-05-07

**내용**: 킥오프 산출물을 하네스 외부의 독립 프로젝트 폴더에 생성하고, dev 스킬을 해당 폴더에 복사하는 방식으로 변경

**배경**: 기존에는 산출물이 하네스 내부(`output/`)에 생성되어 하네스와 프로젝트가 분리되지 않았음. Skill_package에 kickoff 스킬을 넣으면 범용 dev 스킬과 kickoff 전용 스킬이 혼재되는 문제도 있었음.

**해결 방향**:
- 하네스(도구)와 프로젝트(산출물)를 물리적으로 분리
- kickoff-profile이 하네스 상위 디렉토리에 프로젝트 폴더 생성
- 킥오프 문서는 프로젝트 폴더의 pre-requirement/에 직접 생성
- kickoff-skills는 완료 후 "스킬도 복사할까요?" 확인 → 프로젝트 폴더에 dev 스킬 복사
- Skill_package는 dev 스킬만 유지 (kickoff 스킬 미포함)

**결과 구조** (BL-004 적용 후 단순화):
```
{상위 디렉토리}/
├── AI-Project-Kickoff-Harness/    (하네스 — 도구)
└── {프로젝트명}/                  (프로젝트 — 산출물)
    ├── pre-requirement/
    │   └── {프로젝트명}_kickoff.md (YAML frontmatter로 진행 추적)
    └── .claude/skills/            (dev 스킬 — kickoff-skills가 복사)
```

**반영 현황**:
| 파일 | 변경 | 상태 |
|---|---|---|
| kickoff-profile SKILL.md | STEP 2 프로젝트 폴더 생성 추가, 산출물 경로 갱신 | ✅ 반영 |
| kickoff-skills SKILL.md | v2.0 — 프로젝트 폴더에 스킬 복사 + "복사할까요?" 확인 | ✅ 반영 |
| kickoff-done SKILL.md | 완료 안내 메시지 업데이트 | ✅ 반영 |
| Skill_package 레포 | 변경 없음 (dev 스킬만 유지) | — |

### BL-001: State 파일 슬림화

**상태**: ✅ 완료 (BL-004에 의해 대체됨)
**등록일**: 2026-05-06
**완료일**: 2026-05-07

**내용**: kickoff-profile 실행 후 state 섹션 2~4를 상태 요약으로 슬림화하는 단계 추가

**배경**: BL-004(state 파일 완전 제거)가 적용되어 이 항목의 슬림화 로직은 불필요해짐. state 파일 자체가 제거되었으므로 BL-001의 모든 로직도 함께 제거됨.
