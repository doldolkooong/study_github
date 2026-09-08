---
type: study
subject: "Machin Learning"
difficulty: "중급"
created: 2026-09-08
review_1d: 2026-09-09
review_7d: 2026-09-15
review_30d: 2026-10-08
status: learning
source: "[[90_Sources/Velog/05 - DAY20 - 머신러닝 워크플로우와 데이터 누수 - 원문]]"
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY20-2026.09.02"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY20 (2026.09.02)"
source_published: 2026-09-02
source_updated: 2026-09-03
source_id: f7930a58-792f-4c95-a9f5-f8751ccc6580
source_author: doldolkoong
template: "99_Templates/WikiDocs Study Note.md"
tags:
  - study
  - velog
---

# DAY20 - 머신러닝 워크플로우와 데이터 누수

[원문 보기](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY20-2026.09.02) · 2026-09-08 정리

> [!tip] 💡 이 수업을 한 문장으로
> 정답이 있는 데이터로 모델을 학습하고 전처리부터 평가까지 Train/Test 역할을 지킨다.

> [!example] 🎨 한 줄 비유
> 답안이 적힌 시험지를 보고 공부하면 실제 실력을 측정할 수 없다.

## 📌 선행지식

| 필요한 지식 | 어느 정도로? | 관련 노트 |
|---|---|---|
| DAY19 - EDA와 결측치 처리 | 핵심 용어와 입력·출력 흐름 설명 | [[DAY19 - EDA와 결측치 처리\|DAY19 - EDA와 결측치 처리]] |
| DAY21 - 인코딩과 스케일링 및 모델 평가 | 핵심 용어와 입력·출력 흐름 설명 | [[DAY21 - 인코딩과 스케일링 및 모델 평가\|DAY21 - 인코딩과 스케일링 및 모델 평가]] |

## 🎯 학습 목표

- [ ] 정답이 있는 데이터로 모델을 학습하고 전처리부터 평가까지 Train/Test 역할을 지킨다.
- [ ] 학습 유형: 예제로 설명할 수 있다.
- [ ] 분류와 회귀: 예제로 설명할 수 있다.
- [ ] Parameter와 Hyperparameter: 예제로 설명할 수 있다.

## 1단원 — 핵심 정의 🟢 ⭐

### ① 무엇인가?

정답이 있는 데이터로 모델을 학습하고 전처리부터 평가까지 Train/Test 역할을 지킨다.

### ② 왜 필요한가?

Feature·Target·클래스 의미를 확인하고 Train/Test로 분할한다. 모델을 훈련하고 보지 않은 데이터의 예측과 정답을 비교한다. 이를 통해 학습 유형에서 일관된 전처리까지 연결해 이해한다.

### ③ 쉽게 이해하기 🎨

> [!example] 비유
> 답안이 적힌 시험지를 보고 공부하면 실제 실력을 측정할 수 없다.

### ④ 핵심 용어

| 용어 | 뜻과 적용 포인트 |
|---|---|
| 학습 유형 | 지도학습은 정답을 사용하고 비지도학습은 패턴을 찾으며 강화학습은 보상으로 행동을 학습한다. |
| 분류와 회귀 | 범주를 예측하면 분류, 연속 수치를 예측하면 회귀다. LogisticRegression은 분류 모델이다. |
| Parameter와 Hyperparameter | 학습되는 가중치와 사용자가 지정하는 설정값을 구분한다. |
| Titanic 누수 | alive는 survived와 같은 정답 정보를 담으므로 입력 후보에서 제외한다. |
| 일관된 전처리 | 결측 대체 평균·encoder·scaler는 Train에서만 fit하고 Test에는 transform한다. |

## 2단원 — 원리 / 동작 과정 🔵 ⭐

### ① 전체 흐름

1. Feature·Target·클래스 의미를 확인하고 Train/Test로 분할한다.
2. 학습 데이터의 결측·분포를 분석하고 변환기를 학습한다.
3. 모델을 훈련하고 보지 않은 데이터의 예측과 정답을 비교한다.

### ② 왜 이렇게 동작하는가?

범주를 예측하면 분류, 연속 수치를 예측하면 회귀다. LogisticRegression은 분류 모델이다. 결측 대체 평균·encoder·scaler는 Train에서만 fit하고 Test에는 transform한다.

### ③ 그림으로 설명

```mermaid
flowchart LR
    A["학습 유형"] --> B["분류와 회귀"] --> C["일관된 전처리"]
```

## 3단원 — 코드 / 공식 🔵 ⭐

### ① 핵심 코드

> 아래는 원문의 개념을 작은 입력으로 재구성한 학습용 예제다. 원문 코드는 하단 원문에서 확인할 수 있다.

```python
train_age = [20, 30, None]
test_age = [None, 50]
known = [x for x in train_age if x is not None]
mean_age = sum(known) / len(known)
print([mean_age if x is None else x for x in test_age])
```

### ② 코드 이해

| 읽는 순서 | 의미 |
|---|---|
| 입력과 전제 | Feature·Target·클래스 의미를 확인하고 Train/Test로 분할한다. |
| 처리 | 학습 데이터의 결측·분포를 분석하고 변환기를 학습한다. |
| 결과 | Test의 50을 대체값 계산에 사용하지 않는다. 평균 25는 Train에서만 계산했다. |

### ③ 실행 결과

**예상 결과·해석 기준 — 실제 환경 실행 결과와 구분**

```text
[25.0, 50]
```

### ④ 결과 해석

Test의 50을 대체값 계산에 사용하지 않는다. 평균 25는 Train에서만 계산했다.

## 4단원 — 실습 🚀

### 🧪 실습

**문제**

Feature에서 survived만 지우고 alive는 남기면 어떤 문제가 생기는가?

**내 코드 / 내 풀이**

> 직접 풀이한 뒤 이 칸에 기록한다. 아래 해설을 보기 전에 먼저 답을 생각한다.

**결과·해석**

<details>
<summary>해설 보기</summary>

같은 정답 정보가 입력에 남는 Target Leakage이다. 평가 점수가 실제 예측 능력을 반영하지 못한다.

</details>

## 🔧 디버깅 포인트

| 증상 | 원인 | 해결 |
|---|---|---|
| 정확도가 비정상적으로 높음 | alive 같은 정답 컬럼을 Feature로 사용 | 예측 시점에 실제로 알 수 있는 컬럼인지 점검 |
| Test를 자기 평균으로 결측 대체 | 변환 기준을 Test에서 새로 학습 | Train의 imputer를 재사용 |

## 🤖 ChatGPT 요약 붙여넣기

### 📚 이번 수업에서 배운 내용

- **학습 유형**: 지도학습은 정답을 사용하고 비지도학습은 패턴을 찾으며 강화학습은 보상으로 행동을 학습한다.
- **분류와 회귀**: 범주를 예측하면 분류, 연속 수치를 예측하면 회귀다. LogisticRegression은 분류 모델이다.
- **Parameter와 Hyperparameter**: 학습되는 가중치와 사용자가 지정하는 설정값을 구분한다.
- **Titanic 누수**: alive는 survived와 같은 정답 정보를 담으므로 입력 후보에서 제외한다.
- **일관된 전처리**: 결측 대체 평균·encoder·scaler는 Train에서만 fit하고 Test에는 transform한다.

### 🔑 핵심 문장 3개

1. 정답이 있는 데이터로 모델을 학습하고 전처리부터 평가까지 Train/Test 역할을 지킨다.
2. 범주를 예측하면 분류, 연속 수치를 예측하면 회귀다. LogisticRegression은 분류 모델이다.
3. 결측 대체 평균·encoder·scaler는 Train에서만 fit하고 Test에는 transform한다.

### ⚠️ 시험 / 면접 포인트

- 학습 유형의 핵심은 무엇인가?
- 분류와 회귀를 잘못 이해하면 어떤 문제가 생기는가?
- Feature에서 survived만 지우고 alive는 남기면 어떤 문제가 생기는가?

### ✅ 개념 체크리스트

- [ ] 학습 유형의 의미와 원문에서 사용한 이유를 설명할 수 있는가?
- [ ] 분류와 회귀의 의미와 원문에서 사용한 이유를 설명할 수 있는가?
- [ ] Parameter와 Hyperparameter의 의미와 원문에서 사용한 이유를 설명할 수 있는가?
- [ ] Titanic 누수의 의미와 원문에서 사용한 이유를 설명할 수 있는가?
- [ ] 일관된 전처리의 의미와 원문에서 사용한 이유를 설명할 수 있는가?

### ⚠️ 실수 방지 체크리스트

| 흔한 실수 | 바로잡기 |
|---|---|
| 정확도가 비정상적으로 높음 | 예측 시점에 실제로 알 수 있는 컬럼인지 점검 |
| Test를 자기 평균으로 결측 대체 | Train의 imputer를 재사용 |

### 📝 미니 연습문제

1. 학습 유형의 핵심은 무엇인가?

<details>
<summary>해설 보기</summary>

지도학습은 정답을 사용하고 비지도학습은 패턴을 찾으며 강화학습은 보상으로 행동을 학습한다.

</details>

2. 분류와 회귀를 잘못 이해하면 어떤 문제가 생기는가?

<details>
<summary>해설 보기</summary>

범주를 예측하면 분류, 연속 수치를 예측하면 회귀다. LogisticRegression은 분류 모델이다.

</details>

3. 코드 또는 처리 예시의 결과를 설명하라.

<details>
<summary>해설 보기</summary>

Test의 50을 대체값 계산에 사용하지 않는다. 평균 25는 Train에서만 계산했다.

</details>

4. Feature에서 survived만 지우고 alive는 남기면 어떤 문제가 생기는가?

<details>
<summary>해설 보기</summary>

같은 정답 정보가 입력에 남는 Target Leakage이다. 평가 점수가 실제 예측 능력을 반영하지 못한다.

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

- [[DAY19 - EDA와 결측치 처리|DAY19 - EDA와 결측치 처리]]
- [[DAY21 - 인코딩과 스케일링 및 모델 평가|DAY21 - 인코딩과 스케일링 및 모델 평가]]
- [[DAY22 - 선형 회귀와 경사하강법 및 분류 평가|DAY22 - 선형 회귀와 경사하강법 및 분류 평가]]
- [[00_Dashboard/Velog 학습 자료 목차|전체 32개 글 목차]]

## 📎 원문과 확인 자료

- [Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY20-2026.09.02)
- [공식 문서 확인](https://scikit-learn.org/stable/common_pitfalls.html)

> [!quote]- 원문 전체 보기 — 코드·표·이미지 링크 포함
> ![[90_Sources/Velog/05 - DAY20 - 머신러닝 워크플로우와 데이터 누수 - 원문]]
