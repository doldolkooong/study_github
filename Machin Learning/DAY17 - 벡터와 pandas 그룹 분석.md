---
type: study
subject: "Machin Learning"
difficulty: "중급"
created: 2026-09-08
review_1d: 2026-09-09
review_7d: 2026-09-15
review_30d: 2026-10-08
status: learning
source: "[[90_Sources/Velog/09 - DAY17 - 벡터와 pandas 그룹 분석 - 원문]]"
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY17-26.08.28"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY17 (26.08.28)"
source_published: 2026-08-28
source_updated: 2026-09-04
source_id: 58aea05f-32a3-4705-bc9a-17a28e2a7ea9
source_author: doldolkoong
template: "99_Templates/WikiDocs Study Note.md"
tags:
  - study
  - velog
---

# DAY17 - 벡터와 pandas 그룹 분석

[원문 보기](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY17-26.08.28) · 2026-09-08 정리

> [!attention] 원문 확인·보완
> 직교는 내적이 0이라는 기하학적 성질이며 통계적 독립과 같은 말이 아니다. L1/L2 Norm과 두 벡터 차이의 Norm(거리)도 구분한다.

> [!tip] 💡 이 수업을 한 문장으로
> 벡터·행렬의 shape을 이해하고 pandas 변환과 그룹 집계를 연결한다.

> [!example] 🎨 한 줄 비유
> 표를 원하는 기준으로 분류한 뒤 각 서랍의 합계나 평균을 계산한다.

## 📌 선행지식

| 필요한 지식 | 어느 정도로? | 관련 노트 |
|---|---|---|
| DAY16 - 기초 통계와 NumPy 배열 | 핵심 용어와 입력·출력 흐름 설명 | [[DAY16 - 기초 통계와 NumPy 배열\|DAY16 - 기초 통계와 NumPy 배열]] |
| Seaborn Titanic 데이터로 EDA 연습하기 | 핵심 용어와 입력·출력 흐름 설명 | [[Seaborn Titanic 데이터로 EDA 연습하기\|Seaborn Titanic 데이터로 EDA 연습하기]] |

## 🎯 학습 목표

- [ ] 벡터·행렬의 shape을 이해하고 pandas 변환과 그룹 집계를 연결한다.
- [ ] shape와 axis: 예제로 설명할 수 있다.
- [ ] 행렬곱과 Norm: 예제로 설명할 수 있다.
- [ ] Series와 DataFrame: 예제로 설명할 수 있다.

## 1단원 — 핵심 정의 🟢 ⭐

### ① 무엇인가?

벡터·행렬의 shape을 이해하고 pandas 변환과 그룹 집계를 연결한다.

### ② 왜 필요한가?

입력 shape와 컬럼·인덱스를 확인한다. groupby·agg로 평균과 개수를 구하고 원하는 라벨을 선택한다. 이를 통해 shape와 axis에서 groupby 결과까지 연결해 이해한다.

### ③ 쉽게 이해하기 🎨

> [!example] 비유
> 표를 원하는 기준으로 분류한 뒤 각 서랍의 합계나 평균을 계산한다.

### ④ 핵심 용어

| 용어 | 뜻과 적용 포인트 |
|---|---|
| shape와 axis | 집계할 축이 사라진 뒤 어떤 차원이 남는지 예측한다. |
| 행렬곱과 Norm | 행렬곱의 안쪽 차원이 같아야 하며 L1·L2는 벡터 크기와 거리 계산에 연결된다. |
| Series와 DataFrame | 하나의 컬럼 선택은 보통 Series, 표 전체는 DataFrame이다. |
| map과 apply | Series 원소 변환에는 map, 여러 컬럼을 이용한 행 함수에는 apply(axis=1)를 쓸 수 있다. |
| groupby 결과 | 생존률은 survived 평균으로 계산하고 반환된 인덱스를 확인하여 연령대를 선택한다. |

## 2단원 — 원리 / 동작 과정 🔵 ⭐

### ① 전체 흐름

1. 입력 shape와 컬럼·인덱스를 확인한다.
2. map 또는 벡터 연산으로 연령대·가족 수를 만든다.
3. groupby·agg로 평균과 개수를 구하고 원하는 라벨을 선택한다.

### ② 왜 이렇게 동작하는가?

행렬곱의 안쪽 차원이 같아야 하며 L1·L2는 벡터 크기와 거리 계산에 연결된다. 생존률은 survived 평균으로 계산하고 반환된 인덱스를 확인하여 연령대를 선택한다.

### ③ 그림으로 설명

```mermaid
flowchart LR
    A["shape와 axis"] --> B["행렬곱과 Norm"] --> C["groupby 결과"]
```

## 3단원 — 코드 / 공식 🔵 ⭐

### ① 핵심 코드

> 아래는 원문의 개념을 작은 입력으로 재구성한 학습용 예제다. 원문 코드는 하단 원문에서 확인할 수 있다.

```python
import pandas as pd
df = pd.DataFrame({'age':[12,18,25,35], 'survived':[1,0,1,0]})
df['age_group'] = (df['age']//10)*10
result = df.groupby('age_group')['survived'].mean()
print(result.reindex([10,20,30]).tolist())
```

### ② 코드 이해

| 읽는 순서 | 의미 |
|---|---|
| 입력과 전제 | 입력 shape와 컬럼·인덱스를 확인한다. |
| 처리 | map 또는 벡터 연산으로 연령대·가족 수를 만든다. |
| 결과 | 설명용 데이터에서 10대 50%, 20대 100%, 30대 0%다. 실제 Titanic 집계 수치와 구분한다. |

### ③ 실행 결과

**예상 결과·해석 기준 — 실제 환경 실행 결과와 구분**

```text
[0.5, 1.0, 0.0]
```

### ④ 결과 해석

설명용 데이터에서 10대 50%, 20대 100%, 30대 0%다. 실제 Titanic 집계 수치와 구분한다.

## 4단원 — 실습 🚀

### 🧪 실습

**문제**

(4,5) 행렬의 axis=1 평균 결과 shape는?

**내 코드 / 내 풀이**

> 직접 풀이한 뒤 이 칸에 기록한다. 아래 해설을 보기 전에 먼저 답을 생각한다.

**결과·해석**

<details>
<summary>해설 보기</summary>

(4,)이다. 각 행의 열 방향 값 5개를 하나로 줄여 행마다 평균 하나가 남는다.

</details>

## 🔧 디버깅 포인트

| 증상 | 원인 | 해결 |
|---|---|---|
| 10 <= Series < 40에서 오류 | 전체 Series를 단일 참거짓으로 평가 | (s>=10)&(s<40)처럼 각 조건을 괄호로 묶는다 |
| 직교를 통계적 독립과 동일시 | 기하학과 확률 개념 혼동 | 내적 0이라는 조건과 확률적 독립을 구분한다 |

## 🤖 ChatGPT 요약 붙여넣기

### 📚 이번 수업에서 배운 내용

- **shape와 axis**: 집계할 축이 사라진 뒤 어떤 차원이 남는지 예측한다.
- **행렬곱과 Norm**: 행렬곱의 안쪽 차원이 같아야 하며 L1·L2는 벡터 크기와 거리 계산에 연결된다.
- **Series와 DataFrame**: 하나의 컬럼 선택은 보통 Series, 표 전체는 DataFrame이다.
- **map과 apply**: Series 원소 변환에는 map, 여러 컬럼을 이용한 행 함수에는 apply(axis=1)를 쓸 수 있다.
- **groupby 결과**: 생존률은 survived 평균으로 계산하고 반환된 인덱스를 확인하여 연령대를 선택한다.

### 🔑 핵심 문장 3개

1. 벡터·행렬의 shape을 이해하고 pandas 변환과 그룹 집계를 연결한다.
2. 행렬곱의 안쪽 차원이 같아야 하며 L1·L2는 벡터 크기와 거리 계산에 연결된다.
3. 생존률은 survived 평균으로 계산하고 반환된 인덱스를 확인하여 연령대를 선택한다.

### ⚠️ 시험 / 면접 포인트

- shape와 axis의 핵심은 무엇인가?
- 행렬곱과 Norm를 잘못 이해하면 어떤 문제가 생기는가?
- (4,5) 행렬의 axis=1 평균 결과 shape는?

### ✅ 개념 체크리스트

- [ ] shape와 axis의 의미와 원문에서 사용한 이유를 설명할 수 있는가?
- [ ] 행렬곱과 Norm의 의미와 원문에서 사용한 이유를 설명할 수 있는가?
- [ ] Series와 DataFrame의 의미와 원문에서 사용한 이유를 설명할 수 있는가?
- [ ] map과 apply의 의미와 원문에서 사용한 이유를 설명할 수 있는가?
- [ ] groupby 결과의 의미와 원문에서 사용한 이유를 설명할 수 있는가?

### ⚠️ 실수 방지 체크리스트

| 흔한 실수 | 바로잡기 |
|---|---|
| 10 <= Series < 40에서 오류 | (s>=10)&(s<40)처럼 각 조건을 괄호로 묶는다 |
| 직교를 통계적 독립과 동일시 | 내적 0이라는 조건과 확률적 독립을 구분한다 |

### 📝 미니 연습문제

1. shape와 axis의 핵심은 무엇인가?

<details>
<summary>해설 보기</summary>

집계할 축이 사라진 뒤 어떤 차원이 남는지 예측한다.

</details>

2. 행렬곱과 Norm를 잘못 이해하면 어떤 문제가 생기는가?

<details>
<summary>해설 보기</summary>

행렬곱의 안쪽 차원이 같아야 하며 L1·L2는 벡터 크기와 거리 계산에 연결된다.

</details>

3. 코드 또는 처리 예시의 결과를 설명하라.

<details>
<summary>해설 보기</summary>

설명용 데이터에서 10대 50%, 20대 100%, 30대 0%다. 실제 Titanic 집계 수치와 구분한다.

</details>

4. (4,5) 행렬의 axis=1 평균 결과 shape는?

<details>
<summary>해설 보기</summary>

(4,)이다. 각 행의 열 방향 값 5개를 하나로 줄여 행마다 평균 하나가 남는다.

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

- [[DAY16 - 기초 통계와 NumPy 배열|DAY16 - 기초 통계와 NumPy 배열]]
- [[Seaborn Titanic 데이터로 EDA 연습하기|Seaborn Titanic 데이터로 EDA 연습하기]]
- [[DAY19 - EDA와 결측치 처리|DAY19 - EDA와 결측치 처리]]
- [[00_Dashboard/Velog 학습 자료 목차|전체 32개 글 목차]]

## 📎 원문과 확인 자료

- [Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY17-26.08.28)


> [!quote]- 원문 전체 보기 — 코드·표·이미지 링크 포함
> ![[90_Sources/Velog/09 - DAY17 - 벡터와 pandas 그룹 분석 - 원문]]
