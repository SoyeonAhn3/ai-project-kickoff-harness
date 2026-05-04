# 개발 착수 체크리스트

이 체크리스트를 모두 통과하면 개발을 시작할 수 있는 상태다.

## 환경

- [ ] Claude Code CLI 설치 확인
- [ ] gh CLI 설치 및 인증 확인
- [ ] Git 초기화 완료
- [ ] Skill_package GitHub 저장소 접근 가능 확인

## 설계 확정

- [ ] 하네스 단계별 스킬 목록 확정 (kickoff-interview, kickoff-profile, kickoff-gap, kickoff-checklist, kickoff-skills)
- [ ] 각 스킬의 입력/출력 인터페이스 정의
- [ ] 스킬 간 호출 순서 및 데이터 전달 방식 결정
- [ ] project_profile.md 스키마 확정 (필수 필드, 선택 필드)

## 스킬 구조

- [ ] .claude/skills/ 디렉토리 구조 설계
- [ ] 각 스킬의 SKILL.md 템플릿 작성
- [ ] references/ 파일 구조 결정 (질문셋, 유형 판별 기준 등)

## 데이터

- [ ] 프로젝트 유형 분류 기준 정의 (AI / 자동화 / 웹앱 / CLI / BI / 파이프라인 / 라이브러리)
- [ ] 유형별 기본 질문셋 초안 (최소 공통 질문)
- [ ] gap 점검 규칙 정의 (어떤 조건에서 모순으로 판단하는가)

## 외부 의존성

- [ ] Skill_package 저장소 URL 확정
- [ ] 가져올 스킬 7개의 폴더 구조 확인
- [ ] sparse-checkout 또는 복사 스크립트 방식 결정

## 테스트

- [ ] dogfooding 1회차 결과 (이 문서 자체가 결과물)를 기준으로 흐름 검증 완료
- [ ] 최소 1개 다른 프로젝트 아이디어로 dry-run 가능한 상태
