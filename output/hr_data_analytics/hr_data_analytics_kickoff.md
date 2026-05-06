# Project Kickoff — hr_data_analytics

> HR 채용 데이터를 수집·가공하고 AI 기반 후보자 적합도를 분석하여 Power BI로 시각화하는 포트폴리오 프로젝트

---

## 1. 프로젝트 프로필

### 기본 정보

| 항목 | 내용 |
|---|---|
| 프로젝트명 | hr_data_analytics |
| 유형 | 데이터 파이프라인 + AI 프로젝트 (부가: BI 대시보드) |
| 목적 | 데이터 가공/로드, AI 활용, 시각화 역량을 증명하는 포트폴리오 구축 |
| 주요 사용자 | 본인 (포트폴리오 목적) |
| 데이터 소스 | O*NET API (스킬 기준) + JSearch API (채용공고) + Kaggle HR 데이터 (FastAPI Mock) |
| 결과 형태 | Power BI 대시보드 |

### 핵심 기능

| # | 기능 | MVP 포함 |
|---|---|---|
| 1 | API 데이터 수집 (O*NET, JSearch, Kaggle/FastAPI) | ✅ |
| 2 | Snowflake 적재 (raw_data 스키마) | ✅ |
| 3 | 필수요건 필터링 (경력/학력/자격 기준) | ✅ |
| 4 | 고성과자-지원자 유사도 점수화 (코사인 유사도 + 가중합) | ✅ |
| 5 | 후보자 랭킹 | ✅ |
| 6 | Power BI 대시보드 시각화 | ✅ |

### 채택된 AI 제안

| # | 아이디어 | 분류 |
|---|---|---|
| 1 | 스킬 동의어 매핑 테이블 (JS↔JavaScript 등 정규화) | MVP |
| 2 | 데이터 품질 검증 레이어 (NULL 체크, 중복 제거, 포맷 검증) | MVP |
| 3 | 후보자 추천 이유 생성 (상위 랭킹 후보자의 점수 근거 텍스트) | 이후 확장 |
| 4 | 파이프라인 실행 로그 테이블 (ETL 단계별 성공/실패/건수 기록) | 이후 확장 |
| 5 | 가중치 설정 Config 파일 (스킬/학력/경력 가중치를 YAML/JSON으로 외부 설정) | MVP |

### 기술 스택

| 레이어 | 기술 | 선택 이유 |
|---|---|---|
| Data Lake (수집) | Python + requests | API 호출 및 데이터 추출 |
| Data Lake (원본 저장) | Snowflake raw_data 스키마 | API 직접 수집 → 즉시 적재 |
| Data Warehouse | Snowflake | 클라우드 DW, 무료 크레딧 $400 |
| Data Mart | Snowflake (analytics_mart 스키마) | 동일 플랫폼 내 스키마 분리 |
| AI 분석 | Python (cosine similarity + 가중합) | 초보 수준에 적합한 유사도 분석 |
| 시각화 | Power BI Desktop | 무료, Snowflake 직접 연결 지원 |
| Mock API | FastAPI | Kaggle 데이터를 REST API로 서빙 |
| 데이터 생성 | Faker (Python) | 샘플 HR 더미 데이터 생성 (AI 추천) |

### 제약사항

| 유형 | 내용 |
|---|---|
| 기술 수준 | 초보 단계 — 복잡한 ML/회귀분석 미사용 |
| 비용 | 무료 tier만 사용 (Snowflake 크레딧, Power BI Desktop, API Free tier) |
| 인증 관리 | API 키/credentials는 .env 파일로 관리 |

---

## 2. 시스템 아키텍처

### 파이프라인 흐름

```
[API 수집] → [Snowflake raw_data] → [SQL 변환] → [Snowflake analytics_mart] → [Power BI]
```

각 단계 설명:

| 단계 | 설명 | 도구/서비스 |
|---|---|---|
| 1 | 직업별 스킬/역량 기준 수집 | O*NET API |
| 2 | 채용공고 요구사항 수집 | JSearch API (RapidAPI) |
| 3 | 고성과자/후보자 데이터 수집 | Kaggle HR → FastAPI Mock |
| 4 | 데이터 품질 검증 (NULL, 중복, 포맷) | Python Script |
| 5 | 스킬명 정규화 (동의어 매핑) | Python + 매핑 테이블 |
| 6 | Snowflake raw_data 스키마 적재 | Snowflake Python Connector |
| 7 | SQL 변환 → 점수 계산 → 랭킹 | Snowflake SQL |
| 8 | 대시보드 시각화 | Power BI Desktop |

### 외부 서비스 의존성

| 서비스 | 용도 | 필수 여부 |
|---|---|---|
| O*NET Web Services | 직업-스킬 매핑 데이터 | 필수 |
| JSearch (RapidAPI) | 채용공고 데이터 | 필수 |
| Snowflake | 데이터 웨어하우스 / 데이터 마트 | 필수 |
| FastAPI (로컬) | Kaggle 데이터 Mock API 서빙 | 필수 |

---

## 3. 데이터 구조

### 테이블/데이터 구조

#### raw_job_skills (O*NET 직업별 스킬 기준)

| 컬럼 | 타입 | 설명 |
|---|---|---|
| occupation_code | VARCHAR | O*NET 직업 고유 코드 |
| occupation_title | VARCHAR | 직업명 |
| skill_name | VARCHAR | 필요 스킬명 |
| skill_level | FLOAT | 요구 수준 (0~100) |
| skill_category | VARCHAR | Knowledge/Skills/Abilities 분류 |
| loaded_at | TIMESTAMP | 적재 시각 |

#### raw_job_postings (JSearch 채용공고)

| 컬럼 | 타입 | 설명 |
|---|---|---|
| job_id | VARCHAR | 공고 고유 ID |
| job_title | VARCHAR | 공고 제목 |
| company_name | VARCHAR | 회사명 |
| required_skills | VARIANT | 요구 스킬 목록 (JSON) |
| required_experience | VARCHAR | 요구 경력 |
| required_education | VARCHAR | 요구 학력 |
| location | VARCHAR | 근무지 |
| posted_date | DATE | 게시일 |
| loaded_at | TIMESTAMP | 적재 시각 |

#### raw_high_performers (Kaggle — 해당 직무 현재 근무 중 고성과자)

| 컬럼 | 타입 | 설명 |
|---|---|---|
| employee_id | INTEGER | 직원 고유 ID |
| job_role | VARCHAR | 직무 |
| department | VARCHAR | 부서 |
| performance_rating | INTEGER | 성과 등급 (3~4) |
| education | VARCHAR | 학력 |
| years_at_company | INTEGER | 근속 연수 |
| job_satisfaction | INTEGER | 만족도 |
| total_working_years | INTEGER | 총 경력 |

#### raw_candidates (Kaggle — 후보자 이력서)

| 컬럼 | 타입 | 설명 |
|---|---|---|
| candidate_id | INTEGER | 후보자 고유 ID |
| name | VARCHAR | 이름 |
| skills | VARIANT | 보유 스킬 목록 (JSON) |
| education_level | VARCHAR | 학력 |
| experience_years | INTEGER | 경력 연수 |
| category | VARCHAR | 직무 분야 |

#### mart_candidate_scores (최종 스코어링 결과)

| 컬럼 | 타입 | 설명 |
|---|---|---|
| candidate_id | INTEGER | 후보자 식별 |
| job_id | VARCHAR | 대상 공고 |
| requirement_met | BOOLEAN | 필수요건 충족 여부 |
| skill_match_score | FLOAT | 스킬 매칭 점수 (0~100) |
| experience_score | FLOAT | 경력 적합도 점수 |
| education_score | FLOAT | 학력 적합도 점수 |
| similarity_to_top | FLOAT | 고성과자 유사도 (0~1) |
| total_score | FLOAT | 종합 점수 |
| rank | INTEGER | 순위 |
| scored_at | TIMESTAMP | 점수 산출 시각 |

#### mart_skill_comparison (역량 비교 상세 — 레이더 차트용)

| 컬럼 | 타입 | 설명 |
|---|---|---|
| candidate_id | INTEGER | 후보자 식별 |
| skill_category | VARCHAR | 스킬 영역 |
| candidate_level | FLOAT | 후보자 수준 |
| top_performer_avg | FLOAT | 고성과자 평균 수준 |
| gap | FLOAT | 차이 (부족/초과) |

### 볼륨 & 갱신 주기

| 항목 | 내용 |
|---|---|
| 처리 방식 | 배치 처리 (채용 시작 시 1회 + 지원자 유입 시 추가 로드) |
| 보관 기간 | 지원자 데이터 5년, 나머지는 갱신 ��� 덮어쓰기 |
| 규모 | Snowflake XS warehouse 충분 |

---

## 4. 실패 시나리오 / 엣지케이스

| # | 시나리오 | 심각도 | 비고 |
|---|---|---|---|
| 1 | API 호출 실패 (서버 다운/Rate Limit 초과) | 높 | 재시도 로직 또는 캐싱 필요 |
| 2 | 스킬명 불일치 (JS vs JavaScript) | 중 | 동의어 매핑 테이블로 해결 (MVP 포함) |
| 3 | 고성과자 데이터 부족 (해당 직무 1~2명) | 중 | 비교 기준 편향 가능 — 최소 인원 임계값 설정 |
| 4 | Snowflake 연결 끊김 (크레딧 소진/네트워크) | 높 | 크레딧 모니터링, 에러 핸들링 |
| 5 | 지원자 데이터 품질 문제 (스킬/경력 누락, 비정형) | 중 | 품질 검증 레이어로 해결 (MVP 포함) |

---

## 5. 누락/모순 점검 결과

| # | 유형 | 내용 | 상태 | 해결 방법 |
|---|---|---|---|---|
| 1 | 누락 | API 인증/키 관리 방식 미정의 (O*NET, JSearch, Snowflake) | ✅ 해결 | .env 파일로 관리 |
| 2 | 모순 | Google Sheets가 기술 스택에 있으나 파이프라인에서 미사용 | ✅ 해결 | Google Sheets 제거, API 직접 수집으로 변경 |

점검 일시: 2026-05-06

---

## 6. 개발 착수 체크리스트

> 아래 항목을 모두 확인하면 개발을 시작할 수 있습니다.

### 환경 구성
- [ ] Python 3.8+ 설치 확인
- [ ] 필수 패키지 설치 가능 확인 (requests, snowflake-connector-python, pandas, fastapi, uvicorn, faker, scikit-learn)
- [ ] Power BI Desktop 설치 확인
- [ ] .env 파일 생성 및 .gitignore에 추가

### 데이터 & 접근
- [ ] O*NET 개발자 계정 등록 완료 (Basic Auth 발급)
- [ ] RapidAPI 가입 + JSearch API 구독 (Free tier)
- [ ] Kaggle HR 데이터셋 다운로드 (IBM HR Analytics)
- [ ] Faker로 후보자 샘플 데이터 생성 스크립트 준비

### 외부 서비스
- [ ] Snowflake 무료 계정 가입 (크레딧 $400 확인)
- [ ] Snowflake에 HR_DB 데이터베이스 생성
- [ ] Snowflake에 raw_data / analytics_mart 스키마 생성
- [ ] Power BI → Snowflake 연결 테스트

### 설계 확정
- [ ] MVP 범위 최종 확정 (핵심 6개 + AI 제안 3개)
- [ ] 가중치 Config 초기값 결정 (스킬/학력/경력 비중)
- [ ] 스킬 동의어 매핑 초기 목록 작성
- [ ] 테이블 스키마 6개 확정 (변경 없음 확인)

### 프로젝트 설정
- [ ] Git 저장소 초기화
- [ ] 프로젝트 폴더 구조 생성 (src/, data/, config/, tests/)
- [ ] requirements.txt 작성
- [ ] 기본 스킬 세팅 (/kickoff-skills)

생성일: 2026-05-06
