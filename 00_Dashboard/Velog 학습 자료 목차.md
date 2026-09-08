---
type: index
created: 2026-09-08
source_url: "https://velog.io/@doldolkoong/posts"
post_count: 32
tags:
  - velog-index
---

# Velog 학습 자료 목차

[doldolkoong 블로그 전체 글](https://velog.io/@doldolkoong/posts)을 2026-09-08 기준으로 수집했다. 공개 목록의 **32개 글과 학습 노트 32개**를 대응시켰다. 코드·표·이미지 링크를 포함한 원문 보관 노트 32개도 연결했다.

- WikiDocs Study Note: 수업·프로젝트 26개
- Coding Test: 자작 게임 2개 (공식 플랫폼 난이도 미분류)
- Review Log: 주간 회고 4개 (복습 준비, 이해도 미평가)
- 복습일: **2026-09-09 / 2026-09-15 / 2026-10-08**. 원문 발행일이 아닌 정리일을 기준으로 설정했다.

## 읽는 방법

1. 먼저 학습 노트의 한 문장 요약과 핵심 용어를 읽는다.
2. 예제를 읽고 예상 결과를 설명한 뒤 원문 코드와 비교한다.
3. 미니 문제의 해설을 가리고 답한다.
4. 실제로 복습한 뒤 체크박스를 완료한다. [[00_Dashboard/Review Dashboard|복습 대시보드]]와 [[00_Dashboard/Study Dashboard|학습 대시보드]]에서 확인할 수 있다.

> [!info] 자료 범위
> 원문은 작성 당시 경험과 실행 결과다. 새 학습 예제의 출력은 예상 결과로 표시했다. DB 연결·API 호출·도구 설치·사용자 실습은 실행하지 않았다. 원문 스크린샷 속 정보는 이미지 링크로 보존했으며 이미지 내용 전체를 별도 전사한 자료는 아니다.

## 추천 학습 순서

- 기초: [[DAY1 - 개발 환경 구축|DAY1 - 개발 환경 구축]] → [[DAY2 - Git과 Python 가상환경 및 변수|DAY2 - Git과 Python 가상환경 및 변수]] → [[DAY3 - 자료형과 제어문 및 예외 처리|DAY3 - 자료형과 제어문 및 예외 처리]] → [[DAY4 - 함수와 특수 함수|DAY4 - 함수와 특수 함수]] → [[DAY5 - Enum과 클래스 및 모듈|DAY5 - Enum과 클래스 및 모듈]] → [[DAY6 - 표준 라이브러리와 Streamlit|DAY6 - 표준 라이브러리와 Streamlit]] → [[DAY7 - 묵찌빠 상태와 챗봇 구조|DAY7 - 묵찌빠 상태와 챗봇 구조]] → [[가위바위보·묵찌빠·하나빼기 모듈화|가위바위보·묵찌빠·하나빼기 모듈화]] → [[숫자 맞추기 게임|숫자 맞추기 게임]]
- 데이터·협업: [[DAY8 - 게임 모듈화와 DB 기초|DAY8 - 게임 모듈화와 DB 기초]] → [[DAY9 - MySQL 연결과 테이블 생성|DAY9 - MySQL 연결과 테이블 생성]] → [[DAY10 - SQL 조회와 그룹핑 및 JOIN|DAY10 - SQL 조회와 그룹핑 및 JOIN]] → [[DAY12 - GitHub 팀 협업과 PR|DAY12 - GitHub 팀 협업과 PR]]
- SAFE 프로젝트: [[SAFE - 요구사항 정의|SAFE - 요구사항 정의]] → [[SAFE - 데이터 정의|SAFE - 데이터 정의]] → [[SAFE - 데이터 전처리|SAFE - 데이터 전처리]] → [[SAFE - DB 적재|SAFE - DB 적재]] → [[SAFE - 데이터 분석 및 검증|SAFE - 데이터 분석 및 검증]] → [[SAFE - 모델 모듈화 및 웹 서비스 구현|SAFE - 모델 모듈화 및 웹 서비스 구현]]
- 머신러닝: [[DAY16 - 기초 통계와 NumPy 배열|DAY16 - 기초 통계와 NumPy 배열]] → [[DAY17 - 벡터와 pandas 그룹 분석|DAY17 - 벡터와 pandas 그룹 분석]] → [[DAY18 - Matplotlib과 Seaborn 시각화|DAY18 - Matplotlib과 Seaborn 시각화]] → [[DAY19 - EDA와 결측치 처리|DAY19 - EDA와 결측치 처리]] → [[Seaborn Titanic 데이터로 EDA 연습하기|Seaborn Titanic 데이터로 EDA 연습하기]] → [[DAY20 - 머신러닝 워크플로우와 데이터 누수|DAY20 - 머신러닝 워크플로우와 데이터 누수]] → [[DAY21 - 인코딩과 스케일링 및 모델 평가|DAY21 - 인코딩과 스케일링 및 모델 평가]] → [[DAY22 - 선형 회귀와 경사하강법 및 분류 평가|DAY22 - 선형 회귀와 경사하강법 및 분류 평가]] → [[머신러닝 EDA 용어 정리|머신러닝 EDA 용어 정리]]

## Python

| 노트 | 원문 발행일 | 핵심 내용 |
|---|---|---|
| [[DAY2 - Git과 Python 가상환경 및 변수\|DAY2 - Git과 Python 가상환경 및 변수]] | 2026-08-07 | Git의 변경 저장 흐름과 프로젝트별 Python 환경을 구분하고 변수·상수 표현을 익힌다. |
| [[DAY3 - 자료형과 제어문 및 예외 처리\|DAY3 - 자료형과 제어문 및 예외 처리]] | 2026-08-10 | 자료형에 맞는 연산을 선택하고 조건·반복·예외로 프로그램 흐름을 제어한다. |
| [[DAY4 - 함수와 특수 함수\|DAY4 - 함수와 특수 함수]] | 2026-08-11 | 입력·반환값·스코프를 명확히 하고 함수의 재사용과 실행 시점을 이해한다. |
| [[DAY5 - Enum과 클래스 및 모듈\|DAY5 - Enum과 클래스 및 모듈]] | 2026-08-12 | 값·동작을 Enum과 클래스에 묶고 상속·프로퍼티·매직 메서드·모듈의 역할을 구분한다. |
| [[DAY6 - 표준 라이브러리와 Streamlit\|DAY6 - 표준 라이브러리와 Streamlit]] | 2026-08-14 | 하나빼기 게임과 표준 라이브러리·Streamlit의 역할을 작은 예제로 연결한다. |
| [[DAY7 - 묵찌빠 상태와 챗봇 구조\|DAY7 - 묵찌빠 상태와 챗봇 구조]] | 2026-08-14 | 묵찌빠 공격권과 챗봇 대화 이력처럼 다음 동작에 필요한 상태를 관리한다. |

## Coding Test

| 노트 | 원문 발행일 | 핵심 내용 |
|---|---|---|
| [[숫자 맞추기 게임\|숫자 맞추기 게임]] | 2026-08-10 | 입력 변환·범위 검사·시도 횟수·종료 조건을 분리해 숫자 맞추기를 완성한다. |
| [[가위바위보·묵찌빠·하나빼기 모듈화\|가위바위보·묵찌빠·하나빼기 모듈화]] | 2026-08-16 | Enum·공통 입력·결과 반환을 활용해 세 게임을 조합하고 묵찌빠의 공격권을 상태로 관리한다. |

## 머신러닝

| 노트 | 원문 발행일 | 핵심 내용 |
|---|---|---|
| [[DAY16 - 기초 통계와 NumPy 배열\|DAY16 - 기초 통계와 NumPy 배열]] | 2026-08-27 | 스칼라·벡터·행렬을 배열로 표현하고 인덱싱·reshape·axis 연산을 익힌다. |
| [[DAY17 - 벡터와 pandas 그룹 분석\|DAY17 - 벡터와 pandas 그룹 분석]] | 2026-08-28 | 벡터·행렬의 shape을 이해하고 pandas 변환과 그룹 집계를 연결한다. |
| [[DAY18 - Matplotlib과 Seaborn 시각화\|DAY18 - Matplotlib과 Seaborn 시각화]] | 2026-09-01 | 분석 질문에 맞는 그래프를 고르고 숫자 요약에서 보이지 않는 패턴을 해석한다. |
| [[DAY19 - EDA와 결측치 처리\|DAY19 - EDA와 결측치 처리]] | 2026-09-01 | 데이터의 의미와 분포를 점검한 뒤 결측 원인에 맞춰 정제 방법을 선택한다. |
| [[DAY20 - 머신러닝 워크플로우와 데이터 누수\|DAY20 - 머신러닝 워크플로우와 데이터 누수]] | 2026-09-02 | 정답이 있는 데이터로 모델을 학습하고 전처리부터 평가까지 Train/Test 역할을 지킨다. |
| [[DAY21 - 인코딩과 스케일링 및 모델 평가\|DAY21 - 인코딩과 스케일링 및 모델 평가]] | 2026-09-03 | 범주형과 수치형 전처리를 분리하고 학습한 변환기로 Test를 동일한 구조로 만든다. |
| [[DAY22 - 선형 회귀와 경사하강법 및 분류 평가\|DAY22 - 선형 회귀와 경사하강법 및 분류 평가]] | 2026-09-04 | MSE의 기울기로 회귀 파라미터를 갱신하고 분류 오류를 혼동행렬과 임계값으로 분석한다. |
| [[Seaborn Titanic 데이터로 EDA 연습하기\|Seaborn Titanic 데이터로 EDA 연습하기]] | 2026-09-05 | 생존률을 성별·등급·연령·가족 규모로 나누고 표본 수와 교란 가능성까지 해석한다. |
| [[머신러닝 EDA 용어 정리\|머신러닝 EDA 용어 정리]] | 2026-09-05 | EDA의 용어를 데이터 점검 → 전처리 → 모델 평가의 흐름으로 연결한다. |

## SAFE 프로젝트

| 노트 | 원문 발행일 | 핵심 내용 |
|---|---|---|
| [[SAFE - 요구사항 정의\|SAFE - 요구사항 정의]] | 2026-08-26 | 정책 담당자의 질문을 기준으로 핵심 기능·품질 조건·MVP 범위를 정한다. |
| [[SAFE - 데이터 정의\|SAFE - 데이터 정의]] | 2026-08-26 | 요구사항을 구현할 데이터의 출처·항목·단위·키·미확정 사항을 명세한다. |
| [[SAFE - 데이터 전처리\|SAFE - 데이터 전처리]] | 2026-08-26 | 사람이 보기 편한 공공데이터 파일을 일관된 관측 단위의 분석용 표로 바꾼다. |
| [[SAFE - DB 적재\|SAFE - DB 적재]] | 2026-08-26 | 표준화한 DataFrame을 테이블 구조와 연결하고 적재 결과를 조회로 확인한다. |
| [[SAFE - 데이터 분석 및 검증\|SAFE - 데이터 분석 및 검증]] | 2026-08-26 | DB 적재 뒤에도 자료형·집계·지역 단위·시각화를 확인해 서비스에 쓸 수 있는지 검증한다. |
| [[SAFE - 모델 모듈화 및 웹 서비스 구현\|SAFE - 모델 모듈화 및 웹 서비스 구현]] | 2026-08-27 | 검증한 분석 기능을 모듈과 화면으로 나누고 데이터 기간에 맞는 전망 방식을 선택한다. |

## 데이터베이스

| 노트 | 원문 발행일 | 핵심 내용 |
|---|---|---|
| [[DAY8 - 게임 모듈화와 DB 기초\|DAY8 - 게임 모듈화와 DB 기초]] | 2026-08-19 | 게임 코드를 역할별로 분리하고 데이터를 저장하는 DB·SQL·ERD의 역할을 익힌다. |
| [[DAY9 - MySQL 연결과 테이블 생성\|DAY9 - MySQL 연결과 테이블 생성]] | 2026-08-20 | Docker의 MySQL에 클라이언트로 연결하고 기본키·자동 채번이 있는 테이블을 구성한다. |
| [[DAY10 - SQL 조회와 그룹핑 및 JOIN\|DAY10 - SQL 조회와 그룹핑 및 JOIN]] | 2026-08-20 | 행 필터·그룹 집계·정렬·JOIN을 조합해 고객별 주문과 금액을 계산한다. |

## 개발 환경·협업

| 노트 | 원문 발행일 | 핵심 내용 |
|---|---|---|
| [[DAY1 - 개발 환경 구축\|DAY1 - 개발 환경 구축]] | 2026-08-06 | 개발 도구별 역할과 설치 확인 절차를 연결해 재현 가능한 학습 환경을 준비한다. |
| [[DAY12 - GitHub 팀 협업과 PR\|DAY12 - GitHub 팀 협업과 PR]] | 2026-08-26 | 브랜치·보호 규칙·검토·병합 절차를 정해 팀 코드 변경을 관리한다. |

## 주간 회고

| 노트 | 원문 발행일 | 핵심 내용 |
|---|---|---|
| [[98_Review/Velog/1주차 주간 회고 - 개발 환경과 학습 습관\|1주차 주간 회고 - 개발 환경과 학습 습관]] | 2026-08-07 | 교육 적응과 개발 환경 구축 경험에서 도구 역할 이해·버전 확인·예습 복습 습관을 정리한다. |
| [[98_Review/Velog/2주차 주간 회고 - Python 문법에서 게임과 챗봇까지\|2주차 주간 회고 - Python 문법에서 게임과 챗봇까지]] | 2026-08-16 | 자료형·함수·클래스를 게임과 챗봇으로 연결하고 입력 검증과 역할 분리를 반복 연습한다. |
| [[98_Review/Velog/3주차 주간 회고 - 모듈화와 데이터베이스\|3주차 주간 회고 - 모듈화와 데이터베이스]] | 2026-08-26 | 게임 모듈화에서 Docker·MySQL·SQL로 확장한 경험을 정리하고 오류 해석과 입력 검증을 복습한다. |
| [[98_Review/Velog/4주차 주간 회고 - 협업과 SAFE 및 NumPy·pandas\|4주차 주간 회고 - 협업과 SAFE 및 NumPy·pandas]] | 2026-08-31 | Git 협업부터 SAFE 프로젝트, NumPy·pandas까지 연결하고 환경 복구와 집계 연습을 보완한다. |

## 원문 확인·보완 기록

- [[DAY22 - 선형 회귀와 경사하강법 및 분류 평가|DAY22 - 선형 회귀와 경사하강법 및 분류 평가]]: 실험 선택은 검증 데이터로 하고 최종 Test는 남겨 둔다. 유방암 데이터 예시에서는 원문 DAY20의 0=악성, 1=양성과 일반적인 1=관심 클래스 예시를 혼동하지 않는다.
- [[98_Review/Velog/4주차 주간 회고 - 협업과 SAFE 및 NumPy·pandas|4주차 주간 회고 - 협업과 SAFE 및 NumPy·pandas]]: 제목은 4주차지만 본문 첫 문장은 2주차로 되어 있다. 2026-08-24~28의 4주차 회고로 정리했다.
- [[DAY17 - 벡터와 pandas 그룹 분석|DAY17 - 벡터와 pandas 그룹 분석]]: 직교는 내적이 0이라는 기하학적 성질이며 통계적 독립과 같은 말이 아니다. L1/L2 Norm과 두 벡터 차이의 Norm(거리)도 구분한다.
- [[DAY16 - 기초 통계와 NumPy 배열|DAY16 - 기초 통계와 NumPy 배열]]: 표준편차는 산포의 크기이며 작을수록 무조건 좋다는 의미가 아니다. 텐서는 일반적인 용어로 스칼라·벡터·행렬도 포함할 수 있다.
- [[98_Review/Velog/3주차 주간 회고 - 모듈화와 데이터베이스|3주차 주간 회고 - 모듈화와 데이터베이스]]: 글 제목은 3주차이고 본문 제목은 2주차다. 본문의 2026-08-18~21을 3주차로 정리했다. SQL의 개념적 순서는 FROM/JOIN → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT로 이해하되 실제 물리 실행은 옵티마이저에 따라 다르다.
- [[DAY10 - SQL 조회와 그룹핑 및 JOIN|DAY10 - SQL 조회와 그룹핑 및 JOIN]]: 원문의 SQL 순서 설명은 수정했다. 개념적 처리 흐름과 DB의 실제 물리 실행 계획은 다르며 MySQL은 ORDER BY에서 SELECT 별칭을 사용할 수 있다.
- [[DAY9 - MySQL 연결과 테이블 생성|DAY9 - MySQL 연결과 테이블 생성]]: 원문의 allowPublicKeyRetrieval 설정은 당시 연결 사례다. 모든 환경에서 켜야 하는 필수 설정으로 일반화하지 않는다. SQL은 줄바꿈도 공백으로 처리하며 세미콜론은 보통 클라이언트의 문장 종료 구분자다.
- [[DAY7 - 묵찌빠 상태와 챗봇 구조|DAY7 - 묵찌빠 상태와 챗봇 구조]]: 제목 DAY7(08-14)과 본문 첫 DAY6(08-13) 표기가 다르다. 제목 기준으로 정리했다.
- [[DAY6 - 표준 라이브러리와 Streamlit|DAY6 - 표준 라이브러리와 Streamlit]]: datetime 생성자의 마지막 시간 필드는 밀리초가 아니라 마이크로초다.
- [[DAY3 - 자료형과 제어문 및 예외 처리|DAY3 - 자료형과 제어문 및 예외 처리]]: TypeError는 부적절한 타입의 연산·인자에 관한 오류다. 없는 이름은 NameError, 없는 키는 KeyError, 범위 밖 인덱스는 IndexError로 구분한다.
- [[DAY2 - Git과 Python 가상환경 및 변수|DAY2 - Git과 Python 가상환경 및 변수]]: origin은 원격 저장소의 관례적 이름이며 GitHub 자체를 뜻하는 예약어가 아니다. Git Flow식 브랜치 규칙도 팀별 선택이다.
- [[DAY1 - 개발 환경 구축|DAY1 - 개발 환경 구축]]: 원문의 버전·삭제·실행 정책 변경은 당시 환경 기록이다. 새 환경에서 그대로 반복할 필수 절차로 취급하지 않는다.

## 수집 대조표

| No. | 원문 제목 | 학습 노트 | 출처 |
|---|---|---|---|
| 1 | 머신러닝 EDA 용어 정리 | [[머신러닝 EDA 용어 정리\|머신러닝 EDA 용어 정리]] | [원문](https://velog.io/@doldolkoong/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-EDA-%EC%9A%A9%EC%96%B4-%EC%A0%95%EB%A6%AC) |
| 2 | Seaborn Titanic 데이터로 EDA 연습하기 | [[Seaborn Titanic 데이터로 EDA 연습하기\|Seaborn Titanic 데이터로 EDA 연습하기]] | [원문](https://velog.io/@doldolkoong/Seaborn-Titanic-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%A1%9C-EDA-%EC%97%B0%EC%8A%B5%ED%95%98%EA%B8%B0) |
| 3 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY22 (2026.09.04) | [[DAY22 - 선형 회귀와 경사하강법 및 분류 평가\|DAY22 - 선형 회귀와 경사하강법 및 분류 평가]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY22-2026.09.04) |
| 4 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY21 (2026.09.03) | [[DAY21 - 인코딩과 스케일링 및 모델 평가\|DAY21 - 인코딩과 스케일링 및 모델 평가]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY21-2026.09.03-76c2q711) |
| 5 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY20 (2026.09.02) | [[DAY20 - 머신러닝 워크플로우와 데이터 누수\|DAY20 - 머신러닝 워크플로우와 데이터 누수]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY20-2026.09.02) |
| 6 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY19 (2026.09.01) | [[DAY19 - EDA와 결측치 처리\|DAY19 - EDA와 결측치 처리]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY16-2026.09.01) |
| 7 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY18 (2026.08.31) | [[DAY18 - Matplotlib과 Seaborn 시각화\|DAY18 - Matplotlib과 Seaborn 시각화]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY15-2026.08.31) |
| 8 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] 4주차 주간회고 (26.08.24 ~ 26.08.28) | [[98_Review/Velog/4주차 주간 회고 - 협업과 SAFE 및 NumPy·pandas\|4주차 주간 회고 - 협업과 SAFE 및 NumPy·pandas]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-4%EC%A3%BC%EC%B0%A8-%EC%A3%BC%EA%B0%84%ED%9A%8C%EA%B3%A0-26.08.24-26.08.28) |
| 9 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY17 (26.08.28) | [[DAY17 - 벡터와 pandas 그룹 분석\|DAY17 - 벡터와 pandas 그룹 분석]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY17-26.08.28) |
| 10 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY16 (26.08.27) | [[DAY16 - 기초 통계와 NumPy 배열\|DAY16 - 기초 통계와 NumPy 배열]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY13-26.08.27) |
| 11 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] 1st 프로젝트 - 모델 모듈화 및 웹 서비스 구현 | [[SAFE - 모델 모듈화 및 웹 서비스 구현\|SAFE - 모델 모듈화 및 웹 서비스 구현]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%AA%A8%EB%8D%B8-%EB%AA%A8%EB%93%88%ED%99%94-%EB%B0%8F-%EC%9B%B9-%EC%84%9C%EB%B9%84%EC%8A%A4-%EA%B5%AC%ED%98%84) |
| 12 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] 1st 프로젝트 - 데이터 분석 | [[SAFE - 데이터 분석 및 검증\|SAFE - 데이터 분석 및 검증]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B6%84%EC%84%9D) |
| 13 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] 1st 프로젝트 - DB 적재 | [[SAFE - DB 적재\|SAFE - DB 적재]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-DB-%EC%A0%81%EC%9E%AC) |
| 14 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] 1st 프로젝트 - 데이터 전처리 | [[SAFE - 데이터 전처리\|SAFE - 데이터 전처리]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%84%EC%B2%98%EB%A6%AC) |
| 15 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] 1st 프로젝트 - 데이터 정의 | [[SAFE - 데이터 정의\|SAFE - 데이터 정의]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%95%EC%9D%98) |
| 16 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] 1st 프로젝트 - 요구사항 정의 | [[SAFE - 요구사항 정의\|SAFE - 요구사항 정의]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EC%9A%94%EA%B5%AC%EC%82%AC%ED%95%AD-%EC%A0%95%EC%9D%98) |
| 17 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] 3주차 주간 회고 | [[98_Review/Velog/3주차 주간 회고 - 모듈화와 데이터베이스\|3주차 주간 회고 - 모듈화와 데이터베이스]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-3%EC%A3%BC%EC%B0%A8-%EC%A3%BC%EA%B0%84-%ED%9A%8C%EA%B3%A0) |
| 18 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY12 (26.08.24) | [[DAY12 - GitHub 팀 협업과 PR\|DAY12 - GitHub 팀 협업과 PR]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY12-26.08.24) |
| 19 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY10 (26.08.20) | [[DAY10 - SQL 조회와 그룹핑 및 JOIN\|DAY10 - SQL 조회와 그룹핑 및 JOIN]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY10-26.08.20) |
| 20 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY9 (26.08.19) | [[DAY9 - MySQL 연결과 테이블 생성\|DAY9 - MySQL 연결과 테이블 생성]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY9-26.08.19) |
| 21 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY 8 (26.08.18) | [[DAY8 - 게임 모듈화와 DB 기초\|DAY8 - 게임 모듈화와 DB 기초]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY-8-2026.08.18) |
| 22 | 가위바위보, 묵찌빠, 하나빼기 모듈화 | [[가위바위보·묵찌빠·하나빼기 모듈화\|가위바위보·묵찌빠·하나빼기 모듈화]] | [원문](https://velog.io/@doldolkoong/%EA%B0%80%EC%9C%84%EB%B0%94%EC%9C%84%EB%B3%B4-%EB%AC%B5%EC%B0%8C%EB%B9%A0-%ED%95%98%EB%82%98%EB%B9%BC%EA%B8%B0-%EB%AA%A8%EB%93%88%ED%99%94) |
| 23 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] 2주차 주간 회고 | [[98_Review/Velog/2주차 주간 회고 - Python 문법에서 게임과 챗봇까지\|2주차 주간 회고 - Python 문법에서 게임과 챗봇까지]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-2%EC%A3%BC%EC%B0%A8-%EC%A3%BC%EA%B0%84-%ED%9A%8C%EA%B3%A0) |
| 24 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY7 (26.08.14) | [[DAY7 - 묵찌빠 상태와 챗봇 구조\|DAY7 - 묵찌빠 상태와 챗봇 구조]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY7-2026.08.14) |
| 25 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY6 (26.08.13) | [[DAY6 - 표준 라이브러리와 Streamlit\|DAY6 - 표준 라이브러리와 Streamlit]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY6-2026.08.13) |
| 26 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY5 (26.08.12) | [[DAY5 - Enum과 클래스 및 모듈\|DAY5 - Enum과 클래스 및 모듈]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY5-26.08.12) |
| 27 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY4 (26.08.11) | [[DAY4 - 함수와 특수 함수\|DAY4 - 함수와 특수 함수]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY4-26.08.11) |
| 28 | 숫자 맞추기 게임 | [[숫자 맞추기 게임\|숫자 맞추기 게임]] | [원문](https://velog.io/@doldolkoong/%EC%88%AB%EC%9E%90-%EB%A7%9E%EC%B6%94%EA%B8%B0-%EA%B2%8C%EC%9E%84) |
| 29 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY3 (26.08.10) | [[DAY3 - 자료형과 제어문 및 예외 처리\|DAY3 - 자료형과 제어문 및 예외 처리]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY3-26.08.10) |
| 30 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] 1주차 주간 회고 | [[98_Review/Velog/1주차 주간 회고 - 개발 환경과 학습 습관\|1주차 주간 회고 - 개발 환경과 학습 습관]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1%EC%A3%BC%EC%B0%A8-%EC%A3%BC%EA%B0%84-%ED%9A%8C%EA%B3%A0) |
| 31 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY2 (26.08.07) | [[DAY2 - Git과 Python 가상환경 및 변수\|DAY2 - Git과 Python 가상환경 및 변수]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY-2-26.08.07) |
| 32 | [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY1  (26.08.06) | [[DAY1 - 개발 환경 구축\|DAY1 - 개발 환경 구축]] | [원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY1-%EC%88%98%EC%97%85-%EC%A0%95%EB%A6%AC-26.08.06) |
