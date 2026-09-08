---
type: source
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY16-2026.09.01"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY19 (2026.09.01)"
source_id: 6effd2fd-d0a0-432d-843f-b27c4acb0efa
source_author: doldolkoong
source_published: 2026-09-01
source_updated: 2026-09-03
archived: 2026-09-08
tags:
  - velog-source
---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY19 (2026.09.01)

[Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY16-2026.09.01) · [[DAY19 - EDA와 결측치 처리|DAY19 - EDA와 결측치 처리]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY19 (2026.09.01)

**DAY 16**

> 📖 오늘 학습 내용
> 1. 데이터의 형태 (정형/반정형/비정형)
> 2. 데이터 유형 (수치형/범주형)
> 3. 데이터 타입과 데이터 의미
> 4. Feature와 Target
> 5. 데이터 누수(Data Leakage)
> 6. EDA(탐색적 데이터 분석)
> 7. 상관계수(Correlation Coefficient)
> 8. 왜도(Skewness)
> 9. 첨도(Kurtosis)
> 10. 이상치(Outlier)
> 11. Titanic 데이터로 EDA 실습
> 12. Data Cleaning
> 13. 결측치(Missing Value)와 결측 메커니즘
> 14. 결측치 처리 방법 (평균/중앙값/랜덤 샘플링/그룹별/KNN)
> 15. EDA 전체 흐름 정리

---

**1. 데이터의 형태**

데이터는 크게 **정형 데이터 / 반정형 데이터 / 비정형 데이터**로 나눌 수 있다.

정형 데이터(Structured Data)는 스키마가 명확하게 정의되어 있고, 행(Row)과 열(Column) 형태의 2차원 구조로 표현되는 데이터다. CSV, Excel, 관계형 데이터베이스(RDB), 고객 정보, 주문 정보, 매출 데이터 등이 예시이며 일반적으로 머신러닝에서 많이 사용한다.

반정형 데이터(Semi-structured Data)는 완전히 행과 열 형태는 아니지만 일정한 구조나 태그를 가지고 있는 데이터다. JSON, XML, HTML, 로그 데이터가 여기 속한다.

비정형 데이터(Unstructured Data)는 정해진 스키마나 행/열 구조가 없는 데이터다. 이미지, 영상, 음성, 자연어 텍스트가 예시이며 딥러닝에서 많이 활용된다.

> 💡 다만 `정형 데이터 = 머신러닝`, `비정형 데이터 = 딥러닝`으로 반드시 나뉘는 것은 아니다. 정형 데이터에도 딥러닝을 사용할 수 있고, 텍스트 데이터에 전통적인 머신러닝을 사용할 수도 있다. 일반적으로 그렇게 많이 쓰인다는 정도로 이해하면 된다.

---

**2. 데이터 유형**

데이터를 분석할 때 단순히 `dtype`만 보는 것이 아니라 **데이터가 실제로 어떤 의미를 가지고 있는지 해석하는 것이 중요**하다.

```text
데이터
├─ 수치형 데이터
│   ├─ 연속형
│   └─ 이산형
│
└─ 범주형 데이터
    ├─ 순서형
    └─ 명목형
```

**수치형 데이터**는 숫자로 표현되며 수학적인 연산이 의미 있는 데이터다.

- 연속형(Continuous): 값을 더 작은 단위로 계속 나눌 수 있는 데이터. 1년 강수량, 집에서 직장까지의 거리, 몸무게, 키, 온도, 소비한 물의 양, 나이 등. 키가 170cm, 170.1cm, 170.12cm...처럼 계속 세분화될 수 있기 때문에 연속형이다.
- 이산형(Discrete): 셀 수 있는 값으로 이루어져 있으며 중간 값을 사용할 수 없는 데이터. 오늘 마주친 개의 수, 한 주에 본 영화의 수, 가족 구성원 수, 책의 페이지 수, 형제자매 수 등. 영화 1편, 2편, 3편은 가능하지만 1.7편처럼 표현하지 않는다.

**범주형 데이터**는 데이터를 특정 범주(Category) 또는 그룹으로 구분하기 위해 사용하는 데이터다.

- 순서형(Ordinal): 범주 사이에 순서 관계가 존재하는 데이터. 별점(1점 < 2점 < ... < 5점), 성적(F < D < C < B < A), 객실 등급(3등석 < 2등석 < 1등석) 등.
- 명목형(Nominal): 범주 사이에 순서 관계가 없는 데이터. 개의 품종, 성별, 혈액형, 지역, 색상 등. 혈액형 A, B, AB, O 사이에는 대소 관계가 존재하지 않는다.

---

**3. 데이터 타입과 데이터 의미**

데이터 분석에서는 저장되어 있는 데이터 타입과 실제 데이터의 의미가 다를 수 있다.

예를 들어 `pclass = 1, 2, 3`이면 pandas에서는 숫자이기 때문에 `int`로 저장된다. 하지만 실제 의미는 1등석, 2등석, 3등석이므로 **순서형 범주 데이터**로 보는 것이 더 적절하다.

> 데이터 타입을 먼저 보고 판단하기보다는 데이터가 어떤 의미인지 해석한 뒤 분석 방법을 결정해야 한다.

---

**4. Feature와 Target**

머신러닝에서 데이터는 크게 Feature와 Target으로 나눌 수 있다.

- Feature: 모델이 예측하기 위해 사용하는 입력 데이터 (성별, 나이, 객실 등급, 운임, 탑승 항구 등)
- Target: 모델이 최종적으로 예측하려는 값. 타이타닉 데이터에서는 `survived`가 Target이다 (0 = 사망, 1 = 생존). 나머지 변수들은 생존 여부를 예측하기 위한 Feature 후보가 된다.

---

**5. 데이터 누수(Data Leakage)**

Data Leakage는 머신러닝에서 매우 중요한 문제다. 모델이 실제 예측 시점에서는 알 수 없는 정보를 학습 과정에서 미리 사용한 경우를 의미한다. 대표적인 경우는 다음과 같다.

1. **Test 데이터가 학습에 사용된 경우**: train 데이터는 모델 학습, test 데이터는 모델 평가에 사용되어야 하는데, test 데이터의 정보가 train 과정에 들어가면 데이터 누수가 발생한다.
2. **미래 정보를 사용하는 경우**: 예를 들어 "오늘 고객이 대출을 연체할지 예측"하는 모델인데 "다음 달 연체 여부"를 Feature로 사용한다면 미래 정보를 미리 사용한 것이다.
3. **Target과 사실상 동일한 Feature를 사용하는 경우**: 타이타닉에서는 `survived`와 `alive`가 사실상 같은 정보를 가지고 있다. `survived`를 Target으로 사용하면서 `alive`를 Feature에 포함하면 모델이 정답을 미리 알고 학습하는 것과 비슷한 문제가 발생한다.

---

**6. EDA란?**

EDA(Exploratory Data Analysis, 탐색적 데이터 분석)는 데이터를 본격적으로 모델링하기 전에 통계량과 그래프를 이용하여 데이터의 특성을 파악하는 과정이다.

EDA의 목적은 데이터 크기 확인, 데이터 타입 확인, 데이터 분포 확인, 결측치 확인, 이상치 확인, 변수 관계 확인, 중복 데이터 확인, 잘못된 데이터 확인 등을 통해 데이터에 대한 이해도를 높이는 것이다.

일반적으로 다음 순서로 진행한다.

```text
데이터 수집 → 데이터 확인 → EDA → Data Cleaning → Feature Engineering → 모델링
```

---

**7. 상관계수(Correlation Coefficient)**

두 변수 X, Y 사이의 관계의 방향과 정도를 나타내는 수치다. 대표적으로 피어슨 상관계수(Pearson Correlation Coefficient)를 사용하며 범위는 `-1 ≤ r ≤ 1`이다.

| 상관계수 | 의미 |
|---|---|
| r = -1 | 완전한 음의 상관관계 |
| -1 < r < 0 | 음의 상관관계 |
| r ≈ 0 | 선형 상관관계가 거의 없음 |
| 0 < r < 1 | 양의 상관관계 |
| r = 1 | 완전한 양의 상관관계 |

양의 상관관계는 한 변수가 증가하면 다른 변수도 증가하는 경향, 음의 상관관계는 한 변수가 증가하면 다른 변수는 감소하는 경향을 말한다.

Target과 Feature를 비교할 때는 일반적으로 `|r|`이 클수록(즉 r → 1 또는 r → -1에 가까울수록) 선형적인 관계가 강하다고 볼 수 있다.

Feature끼리 지나치게 강한 상관관계를 가지고 있으면 **다중공선성(Multicollinearity)** 문제가 발생할 수 있다. 예를 들어 키(cm)와 키(m)를 동시에 Feature로 사용한다면 거의 동일한 정보를 두 번 제공하는 셈이다. 따라서 회귀 모델 등을 사용할 때는 Feature 사이의 높은 상관관계를 확인할 필요가 있다. 다만 상관관계가 있다고 해서 무조건 제거하는 것은 아니고, 모델과 데이터 특성에 따라 판단해야 한다.

> 💡 상관계수 = 0이라고 해서 두 변수가 완전히 아무 관계가 없다는 뜻은 아니다. 피어슨 상관계수는 기본적으로 **선형적인 관계**만 측정하기 때문에, `y = x²` 같은 곡선 관계에서는 상관계수가 낮게 나올 수도 있다. 그래서 상관계수뿐 아니라 산점도(Scatter Plot)도 같이 확인하는 것이 좋다.

---

**8. 왜도(Skewness)**

왜도는 데이터 분포가 좌우로 얼마나 비대칭인지 나타내는 통계량이다.

- 정규분포: 좌우 대칭이면 `skew ≈ 0`
- 양의 왜도(Positive Skew, `skew > 0`): 오른쪽에 긴 꼬리를 가진 형태 (`Mode < Median < Mean`). 대표적인 예가 연봉, 집값, 자산 등으로, 소수의 매우 큰 값 때문에 평균이 오른쪽으로 끌려간다.
- 음의 왜도(Negative Skew, `skew < 0`): 왼쪽으로 긴 꼬리를 가진 형태 (`Mean < Median < Mode`)

대략적인 판단 기준은 다음과 같다.

```text
-0.5 ≤ skew ≤ 0.5 → 비교적 대칭적인 분포
skew > 0.5 → 오른쪽 꼬리가 긴 양의 왜도
skew < -0.5 → 왼쪽 꼬리가 긴 음의 왜도
```

※ 정확한 기준은 분석 목적에 따라 달라질 수 있다.

---

**9. 첨도(Kurtosis)**

첨도는 데이터 분포의 꼬리와 극단값의 정도를 나타내는 통계량이다. 일반적으로 데이터가 정규분포보다 극단값을 많이 가지는지 파악하는 데 활용한다.

> ⚠️ 일반 통계학에서 Pearson Kurtosis를 사용하면 정규분포 = 3이지만, pandas의 `df['column'].kurt()`는 기본적으로 **Fisher's Excess Kurtosis**를 반환하기 때문에 pandas에서는 정규분포 ≈ 0으로 해석한다.

```text
kurt > 0 → 정규분포보다 꼬리가 두껍고 극단값이 발생하기 쉬움
kurt < 0 → 정규분포보다 꼬리가 얇은 편
```

---

**10. 이상치(Outlier)**

다른 데이터와 비교했을 때 지나치게 크거나 작은 값을 이상치라고 한다. 이상치가 존재하면 평균 왜곡, 분산 증가, 회귀선 왜곡, 모델 성능 저하 등의 문제가 발생할 수 있다. 대표적으로 Box Plot을 이용하여 확인할 수 있다.

```python
sns.boxplot(data=df, y='fare')
```

---

**11. Titanic 데이터로 EDA 실습**

먼저 데이터를 불러오고 크기를 확인한다.

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = sns.load_dataset('titanic')
df.shape
```
> (891, 15) → 891개의 Row, 15개의 Column

`head()`, `tail()`, `sample()`로 실제 데이터 형태를 확인하고, `info()`로 전체 데이터 수/컬럼 수/컬럼명/결측치 여부/Non-Null 데이터 수/데이터 타입/메모리 사용량을 확인할 수 있다. `age`는 714개만 non-null이라 891 - 714 = 177개의 결측치가 있다는 걸 알 수 있다.

`select_dtypes(include=np.number)`로 수치형 컬럼만 선택할 수 있지만, 이는 **저장된 dtype만 기준으로 선택**할 뿐 실제 의미까지 판단하지는 않는다. 예를 들어 `survived`는 int 타입이지만 실제로는 0=사망, 1=생존을 나타내는 범주형 데이터이고, `pclass` 역시 숫자로 저장되어 있지만 객실 등급을 의미하는 범주형 데이터로 보는 게 맞다.

의미에 따라 분류하면:
- 연속형 수치 데이터: `age`, `fare`
- 이산형 수치 데이터: `sibsp`, `parch` (단, 분석 목적에 따라 범주형처럼 처리할 수도 있음)
- 범주형 데이터: `survived`, `pclass`, `sex`, `embarked` 등

`select_dtypes(exclude=np.number)`로 비수치형 데이터를 선택하면 `describe()`에서 count, unique(고유값 개수), top(가장 많이 등장한 값), freq(그 값의 개수)를 확인할 수 있다.

**중복되는 의미의 컬럼 제거**: 타이타닉에는 `survived`↔`alive`, `pclass`↔`class`, `embarked`↔`embark_town`처럼 비슷하거나 동일한 정보를 제공하는 컬럼이 존재한다. 하나만 남기고 제거한다.

```python
df.drop(['alive', 'class', 'embark_town'], axis=1, inplace=True)
```

`axis=0`은 행, `axis=1`은 열을 의미하며, `inplace=True`를 쓰면 원본 `df`에 바로 적용되어 다시 저장할 필요가 없다.

**분포 확인**: 히스토그램과 KDE(Kernel Density Estimation)로 분포를 확인한다.

```python
sns.displot(df, x='age', kind='hist')
sns.displot(df, x='age', bins=10)
sns.displot(df, x='age', kind='kde')
```

`age`의 왜도를 확인하면 0.389로 0에 비교적 가까워 심하게 치우친 분포는 아니다. 반면 `fare`의 왜도는 4.787로 매우 큰 양의 왜도를 보이는데, 일부 승객의 매우 비싼 운임 때문에 오른쪽 꼬리가 길게 형성된 것이다.

**로그 변환(Log Transformation)**: 왜도가 심한 데이터는 로그 변환으로 분포를 완화할 수 있다.

```python
df['fare_log'] = np.log1p(df['fare'])
df['fare_log'].skew()
```
> 0.394... (기존 4.787보다 크게 감소)

`np.log1p()`는 `log(1 + x)`를 계산하는데, 값이 0일 때 문제가 생기는 `np.log()` 대신 자주 사용한다.

첨도도 확인해보면:

```python
df['fare_log'].kurt()
```
> 0.976... (pandas의 Excess Kurtosis 기준이므로 0보다 조금 큰 값으로 해석)

**Box Plot**으로 중앙값, 1/3사분위수, 데이터 범위, 이상치 후보를 한 번에 확인할 수 있다.

```python
sns.boxplot(data=df, y='fare')
```

**범주별 생존율 확인**: `survived`가 0/1로 구성되어 있어 평균을 계산하면 사실상 생존율이 된다.

```python
sns.catplot(data=df, x='sex', y='survived', hue='pclass', kind='bar')
```

**상관관계 Heatmap**:

```python
sns.heatmap(
    df.select_dtypes(include=np.number).corr(),
    vmin=-1, vmax=1, annot=True, linewidths=0.2, cmap='coolwarm'
)
```

`annot=True`는 각 셀에 실제 상관계수를 출력하고, `vmin`/`vmax`로 색상 범위를 -1~1로 고정할 수 있다. 색 자체보다는 셀에 표시된 상관계수 값을 중심으로 해석하는 것이 안전하다.

---

**12. Data Cleaning**

EDA를 통해 데이터의 문제점을 확인했다면 다음 단계는 Data Cleaning이다. 대표적인 과정은 결측치 처리, 중복 데이터 처리, 이상치 처리, 잘못된 값 수정, 데이터 타입 수정, 불필요한 컬럼 제거 등이다.

**결측치(Missing Value)**는 데이터에 값이 존재하지 않는 상태로, NaN, NULL, None, undefined 등으로 표현된다. NaN(Not a Number)은 pandas와 NumPy에서 결측값을 표현할 때 많이 사용한다.

결측치가 있다고 모든 행을 무조건 삭제하면 많은 데이터가 손실될 수 있고, 반대로 임의의 값으로 잘못 채우면 데이터 분포 왜곡, 편향 발생, 모델 성능 저하가 발생할 수 있다. 따라서 결측치가 왜 발생했는지, 비율이 얼마인지, 해당 Feature가 얼마나 중요한지를 함께 고려해야 한다.

**결측 메커니즘**은 크게 세 가지로 나뉜다.

- MCAR(Missing Completely At Random, 완전 무작위 결측): 결측 발생이 다른 변수나 자신의 값과 관련이 없는 경우. 예: 설문 시스템 오류로 일부 응답자의 체중 데이터가 무작위로 누락됨.
- MAR(Missing At Random, 무작위 결측): 결측 여부가 다른 관측 변수와 관련이 있는 경우. 예: 성별에 따라 체중 문항의 응답률 차이가 발생.
- MNAR(Missing Not At Random, 비무작위 결측): 결측 여부가 결측된 값 자체와 관련이 있는 경우. 예: 체중이 높은 사람일수록 자신의 체중을 응답하지 않는 경우.

---

**13. 결측치 확인**

```python
df = sns.load_dataset('titanic')
df.isnull()  # 각 값이 결측치인지 True/False로 반환
df.isnull().sum(axis=0)  # 컬럼별 결측치 개수
```
> age 177, embarked 2, deck 688, embark_town 2

```python
df.isnull().sum(axis=0).sum()  # 전체 결측치 개수
df.isnull().sum().sort_values(ascending=False)  # 많은 순 정렬
```

**결측치 비율**: 개수만 보면 얼마나 비어있는지 판단하기 어려워 비율을 계산한다.

```python
df.isnull().sum() / df.shape[0]
```
> deck 약 77.2%, age 약 19.9%

백분율로 보려면 `(df.isnull().sum() / len(df)) * 100`을 사용한다.

**결측치가 있는 컬럼만 추출**:

```python
df_isnull = df.isnull().sum()
cond = df_isnull > 0
df_isnull[cond]
df_isnull[cond].index.tolist()  # 컬럼 이름만 추출 → ['age', 'embarked', 'deck', 'embark_town']
```

**결측치 Heatmap**으로 위치를 시각적으로 확인할 수 있지만, 그래프만 보고 판단하면 잘못 해석할 수 있어 반드시 개수와 비율도 같이 확인해야 한다.

```python
sns.heatmap(df.isnull(), cbar=False, cmap='viridis')
```

**결측치가 너무 많은 컬럼 제거**: `deck`은 약 77%가 결측치라 제거를 고려할 수 있다.

```python
df.drop(['deck'], axis=1, inplace=True)
```

단, "결측치가 50% 이상이면 무조건 삭제" 같은 절대적 기준은 없고 컬럼의 중요성과 분석 목적을 함께 판단해야 한다.

---

**14. 수치형 결측치 처리 방법**

대표적으로 평균, 중앙값, 최빈값, 랜덤 샘플링, 그룹별 대체, KNN, 모델 기반 대체가 있다.

**평균으로 채우기**:

```python
age_mean = df['age'].mean()
df['age'] = df['age'].fillna(age_mean)
```

또는 `df['age'].fillna(age_mean, inplace=True)`.

**평균과 중앙값 비교**:

```python
df['age_median'] = df['age'].fillna(df['age'].median())
df['age_mean'] = df['age'].fillna(df['age'].mean())
```

KDE 그래프로 평균/중앙값 대체 전후 분포를 비교할 수 있다.

```python
fig, ax = plt.subplots(figsize=(10, 6))
df['age'].plot(kind='kde', ax=ax)
df['age_median'].plot(kind='kde', ax=ax)
df['age_mean'].plot(kind='kde', ax=ax)
plt.show()
```

평균은 이상치가 많지 않고 비교적 대칭적인 데이터에 사용하기 좋고, 중앙값은 이상치가 많거나 분포가 한쪽으로 치우쳐 있을 때 평균보다 안정적일 수 있다. 예를 들어 `10, 20, 20, 30, 1000`이면 1000 때문에 평균이 크게 증가하므로 이런 데이터는 중앙값이 더 적절할 수 있다.

**구간화(Binning)**: 연속형 데이터를 일정한 범위로 나눠 범주형 데이터로 변경하는 방법이다. 예를 들어 나이를 0~9(어린이), 10~19(10대), 20~29(20대)... 처럼 변환할 수 있다. `pd.cut()`은 직접 지정한 범위로 나누고, `pd.qcut()`은 각 구간에 들어가는 데이터 수가 비슷하도록 나눈다. 구간화는 세부 정보 일부가 사라질 수 있으므로 분석 목적에 따라 사용해야 한다.

**Random Sampling Imputation**: 평균이나 중앙값 하나로 모두 채우면 특정 값에 데이터가 몰려 분포가 변할 수 있는데, 이를 줄이기 위해 기존 정상 데이터에서 무작위로 값을 선택해 결측치를 채운다.

```python
random_sampling = (
    df['age']
    .dropna()
    .sample(df['age'].isnull().sum(), random_state=0)
)
```

`random_state=0`을 지정하면 실행할 때마다 같은 결과가 나와 재현성(Reproducibility)을 확보할 수 있다.

랜덤으로 추출한 데이터는 원래 인덱스를 가지고 있어서, 결측치가 있는 인덱스와 맞춰줘야 한다. pandas가 값을 넣을 때 Index 기준으로 정렬하기 때문이다.

```python
random_sampling.index = df['age'][df['age'].isnull()].index

df['age_random'] = df['age']
df.loc[df['age'].isnull(), 'age_random'] = random_sampling
```

이후 `age`, `age_median`, `age_mean`, `age_random`을 KDE로 함께 그려보면 각 방법이 분포에 어떤 영향을 주는지 비교할 수 있다.

**그룹별 결측치 처리**: 전체 평균보다 다른 Feature와의 관계를 이용하는 것이 더 적절할 수 있다. 예를 들어 성별에 따라 나이 분포가 다르다면 남성/여성 각각의 기준으로 처리할 수 있고, Titanic에서는 `sex`, `pclass`, `who` 등을 함께 활용할 수도 있다.

```python
df.groupby('sex')['age'].median()
```

남녀 나이 분포를 KDE로 비교해본 뒤 그룹별 처리 여부를 판단할 수 있다.

```python
df_male = df[df['sex'] == 'male']
df_female = df[df['sex'] == 'female']
```

**결측치 처리 방법별 장단점 정리**

| 방법 | 장점 | 단점 |
|---|---|---|
| 평균 대체 | 간단하고 빠름 | 평균 주변에 값이 몰려 분포 왜곡 가능 |
| 중앙값 대체 | 이상치 영향을 적게 받음 | 마찬가지로 특정 값에 데이터가 몰릴 수 있음 |
| 랜덤 샘플링 | 기존 분포를 상대적으로 잘 유지 | 랜덤성 존재 |
| 그룹별 대체 | 다른 Feature 정보를 활용 가능 | 그룹을 잘못 설정하면 오히려 편향 발생 |
| 모델 기반 대체 | 여러 Feature의 관계를 이용 가능 | 계산량 증가, 구현 복잡 |

> 결측치의 발생 원인 → 데이터 분포 → 다른 Feature와의 관계 → 모델 특성 순으로 생각한 뒤 적절한 방법을 선택해야 한다.

**sklearn 활용**: `SimpleImputer`는 `missing_values`(기본값 `np.nan`)와 `strategy`(mean/median/most_frequent/constant) 옵션으로 결측치를 처리할 수 있다.

```python
from sklearn.impute import SimpleImputer
imputer = SimpleImputer(strategy='median')
```

`KNNImputer`는 주변 데이터와 가장 비슷한 데이터들을 이용해 결측치를 추정한다. 예를 들어 나이가 없는 승객이 있다면 객실 등급, 운임, 가족 수 등이 비슷한 승객들을 찾아 나이를 추정하는 방식으로, 단순 평균 대체보다 많은 정보를 활용할 수 있다.

```python
from sklearn.impute import KNNImputer
```

---

**15. EDA 전체 흐름 정리**

```text
1. 데이터 불러오기
2. shape으로 데이터 크기 확인
3. head / sample로 실제 데이터 확인
4. info로 데이터 타입과 결측치 확인
5. describe로 통계량 확인
6. 데이터 의미에 맞게 수치형 / 범주형 구분
7. 분포 확인
8. 왜도 / 첨도 확인
9. 이상치 확인
10. 변수 간 관계 및 상관관계 확인
11. 결측치 확인
12. 중복 / 불필요한 Feature 확인
13. Data Cleaning
14. Feature Engineering
15. 머신러닝 모델링
```

---

**핵심 정리**

EDA는 데이터를 통계량과 그래프로 탐색하여 데이터의 특성과 문제점을 파악하는 과정이고, Data Cleaning은 EDA에서 발견한 문제를 실제 분석이나 머신러닝에 사용할 수 있도록 정리하는 과정이다.

가장 중요한 점은 데이터 분석에서 `dtype`이 숫자인지가 아니라 **이 숫자가 실제로 무엇을 의미하는가**를 판단해야 한다는 것이다. `pclass = 1, 2, 3`은 숫자지만 실제로는 객실 등급이라는 순서형 범주 데이터인 것처럼 말이다.

결측치를 처리할 때도 단순히 "NaN 발견 → 평균으로 채우기"가 아니라, 왜 결측되었는지 → 얼마나 결측되었는지 → 데이터 분포는 어떠한지 → 다른 Feature와 관계가 있는지 → 어떤 방법이 원래 정보를 가장 덜 왜곡하는지를 순서대로 판단하는 것이 중요하다.

결국 EDA의 핵심은 단순히 그래프를 그리는 것이 아니라 **데이터를 이해하고, 이후 어떤 전처리와 모델링을 해야 하는지 결정하는 과정**이라고 볼 수 있다.
