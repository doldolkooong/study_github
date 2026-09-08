---
type: study
subject: "Database"
difficulty: "초급"
created: 2026-09-08
review_1d: 2026-09-09
review_7d: 2026-09-15
review_30d: 2026-10-08
status: learning
source: "[[90_Sources/Velog/19 - DAY10 - SQL 조회와 그룹핑 및 JOIN - 원문]]"
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY10-26.08.20"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY10 (26.08.20)"
source_published: 2026-08-20
source_updated: 2026-09-05
source_id: f99952bf-0ca9-414d-8130-e5b2eb837abc
source_author: doldolkoong
template: "99_Templates/WikiDocs Study Note.md"
tags:
  - study
  - velog
---

# DAY10 - SQL 조회와 그룹핑 및 JOIN

[원문 보기](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY10-26.08.20) · 2026-09-08 정리

> [!attention] 원문 확인·보완
> 원문의 SQL 순서 설명은 수정했다. 개념적 처리 흐름과 DB의 실제 물리 실행 계획은 다르며 MySQL은 ORDER BY에서 SELECT 별칭을 사용할 수 있다.

> [!tip] 💡 이 수업을 한 문장으로
> 행 필터·그룹 집계·정렬·JOIN을 조합해 고객별 주문과 금액을 계산한다.

> [!example] 🎨 한 줄 비유
> 영수증을 주문별로 합하고 고객별로 다시 묶은 다음 큰 금액순으로 정렬한다.

## 📌 선행지식

| 필요한 지식 | 어느 정도로? | 관련 노트 |
|---|---|---|
| DAY9 - MySQL 연결과 테이블 생성 | 핵심 용어와 입력·출력 흐름 설명 | [[DAY9 - MySQL 연결과 테이블 생성\|DAY9 - MySQL 연결과 테이블 생성]] |
| DAY8 - 게임 모듈화와 DB 기초 | 핵심 용어와 입력·출력 흐름 설명 | [[DAY8 - 게임 모듈화와 DB 기초\|DAY8 - 게임 모듈화와 DB 기초]] |

## 🎯 학습 목표

- [ ] 행 필터·그룹 집계·정렬·JOIN을 조합해 고객별 주문과 금액을 계산한다.
- [ ] 계정과 접속: 예제로 설명할 수 있다.
- [ ] WHERE: 예제로 설명할 수 있다.
- [ ] GROUP BY: 예제로 설명할 수 있다.

## 1단원 — 핵심 정의 🟢 ⭐

### ① 무엇인가?

행 필터·그룹 집계·정렬·JOIN을 조합해 고객별 주문과 금액을 계산한다.

### ② 왜 필요한가?

FROM/JOIN으로 대상과 관계를 정하고 WHERE로 행을 고른다. SELECT할 결과를 정하고 ORDER BY·LIMIT로 상위 고객을 조회한다. 이를 통해 계정과 접속에서 JOIN과 서브쿼리까지 연결해 이해한다.

### ③ 쉽게 이해하기 🎨

> [!example] 비유
> 영수증을 주문별로 합하고 고객별로 다시 묶은 다음 큰 금액순으로 정렬한다.

### ④ 핵심 용어

| 용어 | 뜻과 적용 포인트 |
|---|---|
| 계정과 접속 | DB 사용자·호스트 조건과 실제 네트워크 접근은 구분한다. |
| WHERE | 집계 전에 조건에 맞는 행을 고른다. 1=1은 항상 참인 조건이다. |
| GROUP BY | 정한 키별로 COUNT·SUM 등 집계를 계산한다. |
| ORDER BY와 LIMIT | 결과를 정렬하고 상위 개수를 선택한다. |
| JOIN과 서브쿼리 | 주문 상세 → 주문 → 고객으로 집계 수준을 단계적으로 연결한다. |

## 2단원 — 원리 / 동작 과정 🔵 ⭐

### ① 전체 흐름

1. FROM/JOIN으로 대상과 관계를 정하고 WHERE로 행을 고른다.
2. GROUP BY와 집계로 고객별 결과를 만들고 필요하면 HAVING을 적용한다.
3. SELECT할 결과를 정하고 ORDER BY·LIMIT로 상위 고객을 조회한다.

### ② 왜 이렇게 동작하는가?

집계 전에 조건에 맞는 행을 고른다. 1=1은 항상 참인 조건이다. 주문 상세 → 주문 → 고객으로 집계 수준을 단계적으로 연결한다.

### ③ 그림으로 설명

```mermaid
flowchart LR
    A["계정과 접속"] --> B["WHERE"] --> C["JOIN과 서브쿼리"]
```

## 3단원 — 코드 / 공식 🔵 ⭐

### ① 핵심 코드

> 아래는 원문의 개념을 작은 입력으로 재구성한 학습용 예제다. 원문 코드는 하단 원문에서 확인할 수 있다.

```sql
SELECT customerNumber, COUNT(*) AS cnt
FROM orders
GROUP BY customerNumber
ORDER BY cnt DESC, customerNumber
LIMIT 3;
```

### ② 코드 이해

| 읽는 순서 | 의미 |
|---|---|
| 입력과 전제 | FROM/JOIN으로 대상과 관계를 정하고 WHERE로 행을 고른다. |
| 처리 | GROUP BY와 집계로 고객별 결과를 만들고 필요하면 HAVING을 적용한다. |
| 결과 | 원문 orders 구조를 이용한 정리 쿼리다. 실제 DB를 실행하지 않아 고객 번호와 개수는 확정하지 않는다. |

### ③ 실행 결과

**예상 결과·해석 기준 — 실제 환경 실행 결과와 구분**

```text
주문 수가 많은 고객 최대 3명의 번호와 주문 수. 같은 주문 수면 고객 번호 순.
```

### ④ 결과 해석

원문 orders 구조를 이용한 정리 쿼리다. 실제 DB를 실행하지 않아 고객 번호와 개수는 확정하지 않는다.

## 4단원 — 실습 🚀

### 🧪 실습

**문제**

주문 상세 수량×단가를 고객별로 합치려면 어떤 연결이 필요한가?

**내 코드 / 내 풀이**

> 직접 풀이한 뒤 이 칸에 기록한다. 아래 해설을 보기 전에 먼저 답을 생각한다.

**결과·해석**

<details>
<summary>해설 보기</summary>

orderdetails를 orderNumber로 orders와 연결한 뒤 customerNumber로 SUM(quantityOrdered*priceEach)를 집계한다. 고객 이름은 그 결과를 customers와 연결한다.

</details>

## 🔧 디버깅 포인트

| 증상 | 원인 | 해결 |
|---|---|---|
| 금액 합계가 예상보다 증가 | JOIN으로 행이 중복됨 | 주문별·고객별 집계 단위와 키 확인 |
| WHERE에 집계 조건을 사용 | 행 조건과 그룹 조건 혼동 | COUNT·SUM 결과 조건은 HAVING으로 표현 |

## 🤖 ChatGPT 요약 붙여넣기

### 📚 이번 수업에서 배운 내용

- **계정과 접속**: DB 사용자·호스트 조건과 실제 네트워크 접근은 구분한다.
- **WHERE**: 집계 전에 조건에 맞는 행을 고른다. 1=1은 항상 참인 조건이다.
- **GROUP BY**: 정한 키별로 COUNT·SUM 등 집계를 계산한다.
- **ORDER BY와 LIMIT**: 결과를 정렬하고 상위 개수를 선택한다.
- **JOIN과 서브쿼리**: 주문 상세 → 주문 → 고객으로 집계 수준을 단계적으로 연결한다.

### 🔑 핵심 문장 3개

1. 행 필터·그룹 집계·정렬·JOIN을 조합해 고객별 주문과 금액을 계산한다.
2. 집계 전에 조건에 맞는 행을 고른다. 1=1은 항상 참인 조건이다.
3. 주문 상세 → 주문 → 고객으로 집계 수준을 단계적으로 연결한다.

### ⚠️ 시험 / 면접 포인트

- 계정과 접속의 핵심은 무엇인가?
- WHERE를 잘못 이해하면 어떤 문제가 생기는가?
- 주문 상세 수량×단가를 고객별로 합치려면 어떤 연결이 필요한가?

### ✅ 개념 체크리스트

- [ ] 계정과 접속의 의미와 원문에서 사용한 이유를 설명할 수 있는가?
- [ ] WHERE의 의미와 원문에서 사용한 이유를 설명할 수 있는가?
- [ ] GROUP BY의 의미와 원문에서 사용한 이유를 설명할 수 있는가?
- [ ] ORDER BY와 LIMIT의 의미와 원문에서 사용한 이유를 설명할 수 있는가?
- [ ] JOIN과 서브쿼리의 의미와 원문에서 사용한 이유를 설명할 수 있는가?

### ⚠️ 실수 방지 체크리스트

| 흔한 실수 | 바로잡기 |
|---|---|
| 금액 합계가 예상보다 증가 | 주문별·고객별 집계 단위와 키 확인 |
| WHERE에 집계 조건을 사용 | COUNT·SUM 결과 조건은 HAVING으로 표현 |

### 📝 미니 연습문제

1. 계정과 접속의 핵심은 무엇인가?

<details>
<summary>해설 보기</summary>

DB 사용자·호스트 조건과 실제 네트워크 접근은 구분한다.

</details>

2. WHERE를 잘못 이해하면 어떤 문제가 생기는가?

<details>
<summary>해설 보기</summary>

집계 전에 조건에 맞는 행을 고른다. 1=1은 항상 참인 조건이다.

</details>

3. 코드 또는 처리 예시의 결과를 설명하라.

<details>
<summary>해설 보기</summary>

원문 orders 구조를 이용한 정리 쿼리다. 실제 DB를 실행하지 않아 고객 번호와 개수는 확정하지 않는다.

</details>

4. 주문 상세 수량×단가를 고객별로 합치려면 어떤 연결이 필요한가?

<details>
<summary>해설 보기</summary>

orderdetails를 orderNumber로 orders와 연결한 뒤 customerNumber로 SUM(quantityOrdered*priceEach)를 집계한다. 고객 이름은 그 결과를 customers와 연결한다.

</details>

# 🔁 복습 스케줄

- [ ] **1일 복습** [stage:: 1D] [due:: 2026-09-09]
- [ ] **7일 복습** [stage:: 7D] [due:: 2026-09-15]
- [ ] **30일 복습** [stage:: 30D] [due:: 2026-10-08]

### 복습 방법

1. 요약을 가리고 핵심 개념 3개를 설명한다.
2. 예제 또는 처리 흐름을 보지 않고 재현한다.
3. 해설과 비교하고 틀린 부분을 기록한다.
4. 실제 복습을 마친 뒤 체크한다.

## 🔗 관련 노트

- [[DAY9 - MySQL 연결과 테이블 생성|DAY9 - MySQL 연결과 테이블 생성]]
- [[DAY8 - 게임 모듈화와 DB 기초|DAY8 - 게임 모듈화와 DB 기초]]
- [[SAFE - DB 적재|SAFE - DB 적재]]
- [[00_Dashboard/Velog 학습 자료 목차|전체 32개 글 목차]]

## 📎 원문과 확인 자료

- [Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY10-26.08.20)
- [공식 문서 확인](https://dev.mysql.com/doc/refman/8.4/en/select.html)

> [!quote]- 원문 전체 보기 — 코드·표·이미지 링크 포함
> ![[90_Sources/Velog/19 - DAY10 - SQL 조회와 그룹핑 및 JOIN - 원문]]
