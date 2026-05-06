# Kickoff 진행 상태

마지막 완료: kickoff-checklist
마지막 갱신: 2026-05-06T10:15:00+09:00

## 0. 산출물 설정

- 프로젝트명: hr_data_analytics
- 산출물 경로: output/hr_data_analytics/
- 킥오프 문서: output/hr_data_analytics/hr_data_analytics_kickoff.md

## 1. 프로젝트 정보 (kickoff-start)

- 주 유형: 데이터 파이프라인 + AI 프로젝트
- 부가 유형: BI 대시보드
- 원본 아이디어: HR정보를 대상으로 데이터 로드,가공 & AI분석 & 데이터 시각화를 하고 싶음. 데이터는 datalake - data warehouse - data mart 구조를 사용하고 싶음. 다만, 아직 초보단계로 너무 어려운 데이터 가공이나 회귀분석같은 전문적인 내용은 쉽게 하지 않음.

## 2. 기획 인터뷰 (kickoff-interview)

| 항목 | 내용 |
|---|---|
| 사용자 | 본인 (포트폴리오 목적) |
| 핵심 문제 | 데이터 가공/로드, AI 활용, 시각화 역량을 증명하는 포트폴리오 구축 |
| 데이터 소스 | O*NET API (스킬 기준) + JSearch API (채용공고) + Kaggle HR 데이터 (FastAPI Mock) |
| 결과 형태 | Power BI 대시보드 |
| 핵심 기능 | ①API 데이터 수집 ②Snowflake 적재 ③필수요건 필터링 ④고성과자-지원자 유사도 점수화 ⑤랭킹 ⑥Power BI 시각화 |
| MVP 범위 | API→Snowflake 로드 + 필터링/점수화 + Power BI 대시보드 1개 |
| 제약사항 | 초보 수준 (복잡한 ML 미사용), API 키는 .env로 관리 |
| 파이프라인 구조 | Data Lake (API 원본) → Data Warehouse (Snowflake raw_data) → Data Mart (Snowflake analytics_mart) → Power BI |
| AI 역할 | 코사인 유사도 + 가중합 기반 지원자 적합도 점수 계산 |
| 시각화 KPI | 적합도 랭킹, 역량 비교 레이더 차트, 필수요건 충족 히트맵 |

## 3. 설계 인터뷰 (kickoff-interview)

상태: 완료

### 파이프라인 흐름
- O*NET API → 직업별 스킬/역량 기준 수집
- JSearch API (RapidAPI) → 채용공고 요구사항 수집
- Kaggle HR 데이터 → FastAPI Mock 서버로 서빙 → 고성과자/후보자 데이터
- Python Script로 전체 수집 → Snowflake raw_data 스키마 적재
- SQL 변환 → analytics_mart 스키마 (점수/랭킹)
- Power BI 연결 → 대시보드 시각화

### 데이터 구조
- Raw 테이블 4개: raw_job_skills, raw_job_postings, raw_high_performers, raw_candidates
- Mart 테이블 2개: mart_candidate_scores, mart_skill_comparison
- 고성과자 기준: 해당 직무에서 현재 근무 중인 고성과자

### 볼륨 & 갱신 주기
- 배치 처리 (실시간 아님)
- 지원자 데이터 보관: 5년
- Snowflake XS warehouse 충분

### 실패 시나리오
1. API 호출 실패 (서버 다운/Rate Limit)
2. 스킬명 불일치 (JS vs JavaScript)
3. 고성과자 데이터 부족 (편향)
4. Snowflake 연결 끊김 (크레딧 소진)
5. 지원자 데이터 품질 문제 (누락/비정형)

## 4. 채택된 아이디어 (kickoff-suggest)

상태: 5개 채택

| # | 아이디어 | 분류 |
|---|---|---|
| 1 | 스킬 동의어 매핑 테이블 (JS↔JavaScript 등 정규화) | MVP |
| 2 | 데이터 품질 검증 레이어 (NULL 체크, 중복 제거, 포맷 검증) | MVP |
| 3 | 후보자 추천 이유 생성 (상위 랭킹 후보자의 점수 근거 텍스트) | MVP 이후 |
| 4 | 파이프라인 실행 로그 테이블 (ETL 단계별 성공/실패/건수 기록) | MVP 이후 |
| 5 | 가중치 설정 Config 파일 (스킬/학력/경력 가중치를 YAML/JSON으로 외부 설정) | MVP |

## 5. 프로필 생성 (kickoff-profile)

상태: 완료
파일: output/hr_data_analytics/hr_data_analytics_kickoff.md

## 6. Gap 점검 (kickoff-gap)

상태: 완료
발견: 2건 (모순 1건, 누락 1건)
해결: 전체 해결됨
- 누락: API 인증/키 관리 → .env 파일로 관리
- 모순: Google Sheets 역할 → 제거, API 직접 수집으로 변경

## 7. 체크리스트 (kickoff-checklist)

상태: 완료
체크 항목: 18개 생성
