---
type: source
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-4%EC%A3%BC%EC%B0%A8-%EC%A3%BC%EA%B0%84%ED%9A%8C%EA%B3%A0-26.08.24-26.08.28"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] 4주차 주간회고 (26.08.24 ~ 26.08.28)"
source_id: 3b1aca7a-b503-409a-9160-699e1a703fe9
source_author: doldolkoong
source_published: 2026-08-31
source_updated: 2026-09-03
archived: 2026-09-08
tags:
  - velog-source
---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] 4주차 주간회고 (26.08.24 ~ 26.08.28)

[Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-4%EC%A3%BC%EC%B0%A8-%EC%A3%BC%EA%B0%84%ED%9A%8C%EA%B3%A0-26.08.24-26.08.28) · [[98_Review/Velog/4주차 주간 회고 - 협업과 SAFE 및 NumPy·pandas|4주차 주간 회고 - 협업과 SAFE 및 NumPy·pandas]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

## [플레이데이터 SK네트웍스 Family AI 캠프 36기] 4주차 주간회고 (26.08.24 ~ 26.08.28)

2주차는 팀 프로젝트가 본격적으로 시작된 한 주였다. GitHub 협업 환경을 세팅하고, SAFE 프로젝트의 요구사항·데이터를 정의하고 DB에 적재하는 것까지 진행했고, 목요일부터는 머신러닝 커리큘럼(numpy·pandas)이 시작되면서 배우는 내용의 결이 확 바뀐 한 주이기도 했다.

**회고 순서**
> 1. 08.24 (월) - GitHub 협업 세팅 & 프로젝트 요구사항/데이터 정의
> 2. 08.25 (화) - MySQL 재설치 & 데이터 적재
> 3. 08.26 (수) - SQL 심화 & 모델 모듈화·웹 서비스 구현
> 4. 08.27 (목) - 머신러닝 커리큘럼 시작 (기초통계·행렬·numpy)
> 5. 08.28 (금) - pandas 기초 (Series·DataFrame·map·apply)
> 6. 좋았던 점
> 7. 아쉬웠던 점

<br>

#### **💻 08.24 (월) - GitHub 협업 세팅 & 프로젝트 요구사항/데이터 정의**

팀 프로젝트(SAFE)가 본격적으로 시작된 날. 팀장 입장에서 레파지토리를 만들고, 브랜치 보호 규칙(Branch Protection Rule)을 설정하고, `dev` 브랜치를 기본 브랜치로 바꾼 뒤 팀원을 Collaborator로 초대해서 PR 기반 협업 흐름을 처음부터 끝까지 직접 세팅해봤다. "PR 없이는 아무도 브랜치에 직접 push 할 수 없게 만드는 것"이 핵심이었는데, 팀장이라도 규칙을 우회하지 못하게 막는 옵션까지 켜두고 나니 협업 구조가 훨씬 명확해진 느낌이었다.

오후에는 프로젝트 방향을 잡기 위해 요구사항정의서와 데이터정의서 작업을 시작했다.

수업 내용 정리 - [Day 13 프로젝트 - 요구사항 정의](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EC%9A%94%EA%B5%AC%EC%82%AC%ED%95%AD-%EC%A0%95%EC%9D%98) / [Day 13 프로젝트 - 데이터 정의](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%95%EC%9D%98)

<br>


#### **💻 08.25 (화) - MySQL 재설치 & 데이터 적재**

기존에 설치돼 있던 MySQL에 문제가 생겨서 하루의 상당 시간을 재설치하고 테이블을 다시 만드는 데 썼다. 이후 전처리한 데이터를 분석하고 SQLAlchemy와 PyMySQL을 이용해 MySQL에 적재하는 작업까지 진행했다.

수업 내용 정리 - [Day 14 프로젝트 - 데이터 분석](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B6%84%EC%84%9D) / [Day 14 프로젝트 - DB 적재](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-DB-%EC%A0%81%EC%9E%AC)

<br>


#### **💻 08.26 (수) - SQL 심화 & 모델 모듈화·웹 서비스 구현**

SQL 조회·정렬·그룹핑·조인을 다지면서, 1차 프로젝트에서 만든 모델 코드를 모듈화하고 시각화/시계열 모델을 분리해 Streamlit 기반 웹 서비스로 구현하는 작업을 진행했다. 예측 모델을 선정하고 실제로 화면에서 결과를 확인할 수 있게 만드는 과정이었다.

수업 내용 정리 - [Day 15 수업 내용 정리](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%AA%A8%EB%8D%B8-%EB%AA%A8%EB%93%88%ED%99%94-%EB%B0%8F-%EC%9B%B9-%EC%84%9C%EB%B9%84%EC%8A%A4-%EA%B5%AC%ED%98%84)

<br>

#### **💻 08.27 (목) - 머신러닝 커리큘럼 시작 (기초통계·행렬·numpy)**

오늘부터 본격적으로 머신러닝 커리큘럼(8/27~9/10)이 시작됐다. 표준편차, 독립변수/종속변수, 상관관계/인과관계 같은 기초 통계 개념을 짚은 뒤, 스칼라·벡터·행렬·텐서 개념과 대각행렬·단위행렬·전치행렬 같은 행렬의 종류를 정리했다. 이어서 numpy로 넘어가 배열 생성(`zeros`, `ones`, `full`, `eye`), `vstack`/`hstack`으로 배열 합치기, `reshape`, 조건 인덱싱(Boolean Indexing), `axis` 기준 통계 함수까지 실습했다. `axis`는 "어느 차원을 없앨지"로 이해하는 게 헷갈리지 않는다는 점이 오늘의 핵심이었다.

수업 내용 정리 - [Day 16 수업 내용 정리](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY13-26.08.27)

<br>

#### **💻 08.28 (금) - pandas 기초 (Series·DataFrame·map·apply)**

전날 배운 numpy의 shape, axis 개념을 간단히 복습한 뒤, 본격적으로 pandas로 넘어가 Series와 DataFrame을 다뤘다. iris·titanic 데이터셋으로 조건 검색, `groupby()`, `agg()`, `map()`, `apply()`를 실습했고, 마지막에는 titanic 승객의 10대·20대·30대 생존률을 구하는 문제를 풀었다. `groupby()` 결과에서 원하는 구간만 걸러내면 되는 걸 못 찾아 헤매다가 결국 강사님께 질문해서 "시리즈라서 슬라이싱하면 된다"는 답을 듣고 나서야 풀렸다.

수업 내용 정리 - [Day 17 수업 내용 정리](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY17-26.08.28)

<br>

**👍 좋았던 점**
> - SAFE 프로젝트가 요구사항정의 → 데이터정의 → DB 적재까지 순서대로 이어지면서, 팀 프로젝트가 손에 잡히는 단계로 넘어가는 걸 체감할 수 있었다. 특히 팀장으로서 GitHub 협업 규칙을 처음부터 끝까지 직접 세팅해본 경험이 좋았다.
> - Streamlit과 모델 모듈화 작업을 통해 그동안 배운 분석 결과를 눈에 보이는 서비스 형태로 만들어보는 경험이 재밌었다.
> - numpy에서 pandas로 넘어가면서 벡터·행렬 개념이 실제 데이터 분석(iris, titanic)에 어떻게 쓰이는지 연결해서 이해할 수 있었다.

<br>


**😂 아쉬웠던 점**
> - MySQL을 재설치하고 테이블을 다시 만드는 과정에서 예상보다 시간을 많이 써서, 정작 데이터 적재·분석에 쓸 시간이 줄어들었다.
> - `groupby()` 결과에서 원하는 구간만 슬라이싱하면 되는 간단한 문제를 스스로 못 풀고 결국 질문해서 해결했는데, 기본기가 아직 부족하다는 걸 느꼈다.
> - 한 주 동안 Git 협업, SQL, Streamlit, numpy/pandas가 연달아 나오면서 각 내용을 깊이 있게 복습할 시간이 부족했다.

<br>

**목표**
프로젝트 발표 전까지 요구사항·데이터정의서 다시 점검하기
numpy/pandas 매일 조금씩 복습하기
groupby·map·apply는 직접 문제를 만들어서 풀어보기


