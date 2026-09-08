---
type: source
source_url: "https://velog.io/@doldolkoong/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-EDA-%EC%9A%A9%EC%96%B4-%EC%A0%95%EB%A6%AC"
source_title: "머신러닝 EDA 용어 정리"
source_id: 3789d3b8-0980-4e1c-8027-8c4d5d6ef661
source_author: doldolkoong
source_published: 2026-09-05
source_updated: 2026-09-06
archived: 2026-09-08
tags:
  - velog-source
---

# 머신러닝 EDA 용어 정리

[Velog 원문](https://velog.io/@doldolkoong/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-EDA-%EC%9A%A9%EC%96%B4-%EC%A0%95%EB%A6%AC) · [[머신러닝 EDA 용어 정리|머신러닝 EDA 용어 정리]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

# 📊 머신러닝 EDA 용어 총정리

머신러닝을 시작하면 가장 먼저 하는 작업 중 하나가 **EDA(Exploratory Data Analysis, 탐색적 데이터 분석)**이다.

EDA는 단순히 그래프 몇 개 그리는 과정이 아니라,

> **데이터가 어떤 구조인지 확인하고, 문제를 발견하고, 모델링 방향을 결정하는 과정**

이라고 볼 수 있다.

이 글에서는 머신러닝 EDA 과정에서 자주 등장하는 용어들을 순서대로 정리한다.

---

## 목차

1. [EDA 기초 개념](#1-eda-기초-개념) — EDA, Dataset, Observation, Feature, Target, Column, Row, Shape, Dimension
2. [데이터 타입과 변수 종류](#2-데이터-타입과-변수-종류) — Data Type, Numerical/Categorical, Continuous/Discrete, Nominal/Ordinal/Binary
3. [고유값·빈도 관련](#3-고유값빈도-관련) — Cardinality, Unique, nunique, Frequency
4. [결측치와 중복](#4-결측치와-중복) — Missing Value, Missing Rate, Imputation, Duplicate
5. [기술통계](#5-기술통계) — Descriptive Statistics, Count, Mean, Median, Mode, Min/Max, Range
6. [산포도 지표](#6-산포도-지표) — Variance, Standard Deviation, Quantile, Quartile, Percentile, IQR
7. [이상치](#7-이상치) — Outlier, IQR Rule
8. [분포 관련 개념](#8-분포-관련-개념) — Distribution, Normal/Gaussian, Skewness, Kurtosis, Uni/Bi/Multimodal
9. [상관관계와 인과관계](#9-상관관계와-인과관계) — Correlation, Pearson/Spearman/Kendall, Correlation Matrix, Causality, Covariance
10. [데이터 시각화](#10-데이터-시각화) — Histogram, Bin, Bar/Count/Box/Scatter/Line Plot, Heatmap, Pair Plot, Violin Plot, KDE, Density
11. [Feature 관련 작업](#11-feature-관련-작업) — Feature Engineering/Selection/Extraction
12. [데이터 전처리](#12-데이터-전처리) — Data Preprocessing, Encoding(Label/One-Hot/Ordinal), Dummy Variable
13. [스케일링과 변환](#13-스케일링과-변환) — Scaling, Standardization, Normalization, Min-Max, Robust, Log Transformation, Binning, Discretization
14. [Target과 클래스 불균형](#14-target과-클래스-불균형) — Target Distribution, Class, Class Imbalance, Oversampling/Undersampling, SMOTE
15. [데이터 분할](#15-데이터-분할) — Train/Test/Validation Data, Train-Test Split, Random State, Seed, Stratify
16. [데이터 누수](#16-데이터-누수) — Data Leakage, Target Leakage, Scaling Leakage
17. [표본과 편향](#17-표본과-편향) — Sampling, Population, Sample, Sampling Bias, Selection Bias, Bias
18. [잡음과 다중공선성](#18-잡음과-다중공선성) — Noise, Signal, Multicollinearity, VIF
19. [차원 축소](#19-차원-축소) — High Dimensionality, Curse of Dimensionality, Dimensionality Reduction, PCA, t-SNE, UMAP
20. [집계와 그룹 분석](#20-집계와-그룹-분석) — GroupBy, Aggregation, Pivot Table, Crosstab, Contingency Table
21. [변량 분석](#21-변량-분석) — Univariate/Bivariate/Multivariate Analysis, Segment, Pattern
22. [시계열 관련 개념](#22-시계열-관련-개념) — Trend, Seasonality, Time Series, Time Index, Lag, Rolling, Moving Average, Stationarity
23. [분포 변화](#23-분포-변화) — Distribution Shift, Data Drift, Concept Drift
24. [모델 적합 관련](#24-모델-적합-관련) — Baseline, Overfitting, Underfitting, Generalization, Bias-Variance Tradeoff
25. [교차검증](#25-교차검증) — Cross Validation, K-Fold, Stratified K-Fold
26. [모델과 파라미터](#26-모델과-파라미터) — Model, Algorithm, Parameter, Hyperparameter, Grid/Random Search
27. [학습 방식과 문제 유형](#27-학습-방식과-문제-유형) — Supervised/Unsupervised Learning, Classification, Regression, Clustering
28. [평가 지표 - 분류](#28-평가-지표---분류) — Accuracy, Confusion Matrix, TP/TN/FP/FN, Precision, Recall, F1-Score, ROC, AUC
29. [평가 지표 - 회귀](#29-평가-지표---회귀) — MAE, MSE, RMSE, MAPE, R², Residual
30. [모델 해석](#30-모델-해석) — Feature Importance, Permutation Importance, SHAP
31. [EDA 실전 체크리스트](#31-eda-실전-체크리스트) — 진행 순서, info(), describe(), unique(), value_counts(), isnull(), duplicated(), corr()
32. [용어 빠른 참조표](#32-용어-빠른-참조표)
33. [EDA를 왜 해야 할까](#33-eda를-왜-해야-할까)

---

## 1. EDA 기초 개념

### EDA — Exploratory Data Analysis (탐색적 데이터 분석)

데이터를 본격적으로 모델에 학습시키기 전에 데이터의 구조, 분포, 관계, 이상 여부 등을 탐색하는 과정이다.

EDA에서 주로 확인하는 것들은 다음과 같다.

- 데이터 크기
- 변수 종류
- 데이터 타입
- 결측치
- 이상치
- 데이터 분포
- 변수 간 관계
- Target과 Feature의 관계
- 클래스 불균형
- 중복 데이터
- 상관관계

즉, **EDA = 데이터를 이해하는 과정**이라고 생각하면 된다.

### Dataset (데이터셋)

분석이나 머신러닝에 사용하는 전체 데이터 집합을 의미한다.

예를 들어 타이타닉 데이터가 있다면,

```text
age
sex
fare
pclass
survived
```

등의 컬럼과 여러 승객 데이터가 하나의 Dataset을 구성한다.

### Observation / Sample / Instance

하나의 관측값을 의미한다. DataFrame에서는 보통 **한 행(row)**에 해당한다.

예를 들어

```text
age = 25
sex = male
fare = 30
survived = 1
```

이라면 한 명의 승객 정보 전체가 하나의 Observation이다.

비슷한 의미로 다음 용어들이 사용된다.

- Observation
- Sample
- Instance
- Record

### Feature

머신러닝 모델이 예측할 때 사용하는 입력 변수이다.

다른 표현으로는 다음과 같은 말이 있다.

- Feature
- Input Variable
- Independent Variable
- Predictor
- 설명변수
- 독립변수

예를 들어 타이타닉 생존 여부를 예측한다면 `age`, `sex`, `fare`, `pclass` 등이 Feature가 될 수 있다.

보통 머신러닝에서는 Feature 데이터를 `X`라고 표현한다.

```python
X = df[['age', 'sex', 'fare', 'pclass']]
```

### Target

머신러닝 모델이 **예측하려는 값**이다.

다음과 같은 이름으로도 사용된다.

- Target
- Label
- Output
- Response Variable
- Dependent Variable
- 종속변수
- 목적변수

타이타닉 데이터에서는 `survived`가 Target이 된다. 보통 `y`로 표현한다.

```python
y = df['survived']
```

### Feature와 Target의 관계

머신러닝 데이터는 보통 다음처럼 생각할 수 있다.

```text
Feature → Model → Target 예측
```

예를 들어

```text
성별
나이
객실등급
운임
   ↓
머신러닝 모델
   ↓
생존 여부
```

가 된다.

### Column (컬럼)

데이터의 하나의 속성 또는 변수를 의미한다. 예를 들어 `age`, `sex`, `fare`, `survived` 각각이 하나의 Column이다.

### Row (행)

데이터의 한 행이다. 보통 하나의 사람, 제품, 거래, 사건 등 하나의 관측 대상을 의미한다.

### Shape

데이터의 행과 열 개수를 의미한다.

```python
df.shape
```

결과가 `(891, 12)`라면 `891 rows`, `12 columns`라는 의미이다.

### Dimension (차원)

데이터의 차원을 의미한다. 머신러닝에서는 Feature의 개수를 데이터의 차원이라고 표현하기도 한다.

예를 들어 Feature가 `age`, `fare`, `pclass` 3개라면 `3-dimensional data`라고 볼 수 있다.

---

## 2. 데이터 타입과 변수 종류

### Data Type — dtype

데이터가 어떤 자료형으로 저장되어 있는지를 의미한다.

pandas에서 자주 등장하는 타입은 다음과 같다.

```text
int
float
object
bool
datetime
category
```

예를 들어

```text
age      float64
fare     float64
sex      object
```

와 같이 나타날 수 있다.

EDA에서는 dtype을 반드시 확인해야 한다. 숫자인데 `object`로 저장되어 있거나 날짜 데이터가 문자열인 경우가 있기 때문이다.

### Numerical Feature (숫자형 변수)

숫자로 이루어진 변수이다. 예시: `age`, `height`, `weight`, `income`, `fare`

숫자형 데이터는 다시 두 종류로 구분할 수 있다.

### Continuous Variable — 연속형 변수

연속적인 값을 가질 수 있는 데이터이다. 예시: 키, 몸무게, 온도, 가격, 거리

예를 들어 `170.1`, `170.15`, `170.153`처럼 연속적인 값을 가질 수 있다.

### Discrete Variable — 이산형 변수

셀 수 있는 형태의 숫자 데이터이다. 예시: 자녀 수, 구매 횟수, 사고 건수, 학생 수

값이 보통 `0, 1, 2, 3 ...`처럼 구분된다.

### Categorical Feature (범주형 변수)

범주를 나타내는 데이터이다. 예시: 남자/여자, 서울/부산/인천, A/B/C

숫자로 표현되어 있다고 해서 반드시 Numerical Feature인 것은 아니다. 예를 들어 `1=서울, 2=부산, 3=대구`라면 숫자로 저장되어 있어도 실제 의미는 **범주형 변수**이다.

### Nominal Variable — 명목형 변수

순서가 없는 범주형 데이터이다. 예시: 남자/여자, 서울/부산/인천, 빨강/파랑/초록

서울이 부산보다 크거나 작다는 개념이 없기 때문에 순서가 없다.

### Ordinal Variable — 순서형 변수

범주 사이에 순서가 존재하는 데이터이다. 예시: 하/중/상, 1등급/2등급/3등급, 불만족/보통/만족

순서는 있지만 각 단계 사이의 차이가 동일하다고 보장할 수는 없다.

### Binary Variable — 이진 변수

값이 두 종류만 존재하는 변수이다. 예시: 생존/사망, Yes/No, True/False, 0/1

---

## 3. 고유값·빈도 관련

### Cardinality

범주형 Feature에서 **고유한 값의 개수**를 의미한다. 예를 들어 지역 = 서울, 부산, 인천이라면 Cardinality는 3이다.

Cardinality가 매우 높은 범주형 변수는 고객 ID, 주소, 상품명, 닉네임 등에서 자주 나타난다. 이를 **High Cardinality**라고 한다.

### Unique

중복을 제외한 고유값이다.

```python
df['sex'].unique()
```

결과: `male`, `female`

### nunique

컬럼 안에 존재하는 고유값의 **개수**를 확인한다.

```python
df['sex'].nunique()
```

결과: `2`

### Frequency (빈도)

특정 값이 데이터에서 몇 번 등장하는지를 의미한다.

```python
df['sex'].value_counts()
```

처럼 확인할 수 있다.

### Frequency Distribution (도수분포)

각 값 또는 구간별로 데이터가 얼마나 존재하는지를 나타낸 것이다.

예를 들어 연령을 10대/20대/30대/40대 등으로 나누어 사람 수를 계산하는 것이 도수분포의 예이다.

---

## 4. 결측치와 중복

### Missing Value — 결측치

데이터가 존재하지 않는 상태를 의미한다.

pandas에서는 주로 `NaN`, `None`, `NaT`로 나타난다.

예를 들어 `age = NaN`이라면 나이 정보가 없는 데이터이다.

### 결측률 (Missing Rate)

전체 데이터 중 결측치가 차지하는 비율이다. 예를 들어 100개의 데이터 중 20개가 결측치라면 결측률 = 20%이다.

결측률이 지나치게 높은 Feature는 제거를 고려할 수 있다.

### Imputation — 결측치 대체

결측치를 다른 값으로 채우는 작업이다.

대표적으로 평균, 중앙값, 최빈값, 0, Unknown 등을 사용할 수 있다. 예를 들어 나이 결측치를 중앙값으로 채울 수 있다.

- **Mean Imputation**: 평균값으로 결측치를 채우는 방법. 단점은 이상치에 영향을 많이 받을 수 있다는 것이다.
- **Median Imputation**: 중앙값으로 결측치를 채우는 방법. 이상치가 존재하는 데이터에서는 평균보다 중앙값을 사용하는 경우가 많다.
- **Mode Imputation**: 최빈값으로 결측치를 채우는 방법. 범주형 데이터에서 많이 사용된다.

### Duplicate Data — 중복 데이터

동일한 데이터가 여러 번 존재하는 경우이다.

예를 들어

```text
이름    나이
철수    25
철수    25
```

처럼 같은 데이터가 중복되어 존재할 수 있다. 중복 데이터는 통계나 모델 학습 결과를 왜곡할 수 있기 때문에 확인이 필요하다.

---

## 5. 기술통계

### Descriptive Statistics — 기술통계

데이터의 특징을 숫자로 요약한 것이다. 대표적인 기술통계량은 `count, mean, std, min, 25%, 50%, 75%, max`이다.

```python
df.describe()
```

로 확인할 수 있다.

### Count

데이터의 개수이다. 결측치는 일반적으로 count에서 제외된다.

### Mean (평균)

모든 값을 더한 후 데이터 개수로 나눈 값이다.

```text
1, 2, 3, 4, 5 → 평균 = 3
```

이상치의 영향을 많이 받는다.

### Median (중앙값)

데이터를 크기순으로 정렬했을 때 가운데 위치한 값이다.

```text
1, 2, 3, 4, 100 → Mean = 22, Median = 3
```

따라서 이상치가 많은 데이터에서는 Median이 중심을 더 잘 나타내는 경우가 있다.

### Mode (최빈값)

가장 많이 등장하는 값이다.

```text
1, 1, 1, 2, 3 → Mode = 1
```

범주형 데이터 분석에서 특히 자주 사용된다.

### Min / Max / Range

- **Min**: 데이터의 최솟값
- **Max**: 데이터의 최댓값
- **Range (범위)**: 최댓값과 최솟값의 차이 → `Range = Max - Min`

---

## 6. 산포도 지표

### Variance — 분산

데이터가 평균을 기준으로 얼마나 퍼져 있는지를 나타낸다.

분산이 크다면 데이터가 넓게 퍼져 있다는 의미이고, 분산이 작다면 평균 주변에 데이터가 모여 있다는 의미이다.

### Standard Deviation — 표준편차

분산의 제곱근이다. 보통 `std`라고 표현한다.

표준편차가 클수록 데이터가 평균에서 멀리 퍼져 있다고 볼 수 있다.

### Quantile — 분위수

데이터를 일정한 비율로 나눈 지점이다. 대표적으로 `25%, 50%, 75%`를 많이 사용한다.

### Quartile — 사분위수

데이터를 4개 구간으로 나눈 것이다.

```text
Q1 = 25%
Q2 = 50%
Q3 = 75%
```

여기서 Q2는 Median과 동일하다.

### Percentile — 백분위수

전체 데이터를 100개의 구간으로 나눈 위치를 의미한다.

예를 들어 `90 percentile`은 전체 데이터의 약 90%가 해당 값보다 작거나 같다는 의미이다.

### IQR — Interquartile Range (사분위 범위)

```text
IQR = Q3 - Q1
```

으로 계산한다. 이상치를 탐지할 때 많이 사용된다.

---

## 7. 이상치

### Outlier — 이상치

다른 데이터와 크게 떨어져 있는 값을 의미한다.

예를 들어 대부분 사람의 나이가 20~60인데 `age = 500`이라는 값이 있다면 이상치일 가능성이 매우 높다.

### IQR Rule

IQR을 이용하여 이상치를 찾는 대표적인 방법이다.

```text
Lower Bound = Q1 - 1.5 × IQR
Upper Bound = Q3 + 1.5 × IQR
```

이 범위를 벗어나는 데이터를 이상치 후보로 본다.

단, 범위를 벗어났다고 무조건 잘못된 데이터는 아니다. 실제 의미를 확인해야 한다.

---

## 8. 분포 관련 개념

### Distribution — 분포

데이터가 어떤 형태로 퍼져 있는지를 의미한다. EDA에서 매우 중요한 개념이다.

예를 들어 다음을 확인한다.

- 중앙에 몰려 있는가?
- 한쪽으로 치우쳐 있는가?
- 값이 두 군데로 나뉘어 있는가?
- 이상치가 많은가?

### Normal Distribution — 정규분포

평균을 중심으로 좌우가 대칭인 종 모양의 분포이다.

```text
          /\
        /    \
      /        \
_____/__________\_____
```

평균, 중앙값, 최빈값이 비슷한 위치에 나타나는 특징이 있다.

### Gaussian Distribution

Normal Distribution과 같은 의미로 사용되는 경우가 많다. 즉, `Gaussian Distribution = Normal Distribution`이다.

### Skewness — 왜도

데이터 분포가 한쪽으로 얼마나 치우쳐 있는지를 나타낸다.

- **Positive Skew**: 오른쪽 꼬리가 긴 형태. 보통 `Mean > Median` 경향이 나타난다. 소득, 집값, 매출 등의 데이터에서 자주 나타난다.
- **Negative Skew**: 왼쪽 꼬리가 긴 형태. 보통 `Mean < Median`의 경향을 가진다.

### Kurtosis — 첨도

분포의 꼬리와 뾰족함 정도를 나타내는 지표이다. 극단적인 값이 얼마나 자주 발생하는지를 이해할 때 참고할 수 있다.

### Unimodal / Bimodal / Multimodal

- **Unimodal (단봉분포)**: 하나의 뚜렷한 봉우리를 가지는 분포이다.
- **Bimodal (이봉분포)**: 두 개의 봉우리가 나타나는 분포이다. 서로 다른 두 집단이 하나의 데이터에 섞여 있을 가능성이 있다.
- **Multimodal**: 여러 개의 봉우리가 나타나는 분포이다. 데이터에 여러 하위 집단이 존재할 가능성을 생각해볼 수 있다.

---

## 9. 상관관계와 인과관계

### Correlation — 상관관계

두 변수의 값이 함께 변화하는 정도이다. 예를 들어 키가 증가하면 몸무게도 증가하는 것처럼, 한 변수가 증가할 때 다른 변수도 증가하는 관계가 있을 수 있다.

### 상관계수 (Correlation Coefficient)

상관관계를 숫자로 나타낸 값이다. 보통 `-1 ~ 1` 사이의 값을 가진다.

```text
1에 가까움    → 강한 양의 상관관계
0에 가까움    → 선형 관계가 약함
-1에 가까움   → 강한 음의 상관관계
```

### Positive / Negative / No Correlation

- **양의 상관관계**: 한 변수가 증가할수록 다른 변수도 증가하는 관계 (`X ↑ → Y ↑`)
- **음의 상관관계**: 한 변수가 증가할수록 다른 변수는 감소하는 관계 (`X ↑ → Y ↓`)
- **No Correlation**: 상관계수가 0에 가까운 경우. 다만 상관계수가 0이라고 두 변수 사이에 아무런 관계도 없는 것은 아니다 — 비선형 관계가 존재할 수도 있다.

### Pearson / Spearman / Kendall Correlation

- **피어슨 상관계수**: 두 연속형 변수 사이의 **선형 관계**를 측정한다. EDA에서 가장 많이 사용하는 상관계수 중 하나이다.
- **스피어만 상관계수**: 실제 값보다는 **순위**를 기반으로 상관관계를 측정한다. 선형 관계가 아니더라도 한쪽이 증가할수록 다른 쪽이 일정하게 증가하거나 감소하는 관계를 분석할 때 활용할 수 있다.
- **켄달 상관계수**: 순위를 기반으로 두 변수의 관계를 분석하는 방법이다. 표본이 작거나 순위 데이터 분석에서 활용된다.

### Correlation Matrix — 상관행렬

여러 변수들의 상관계수를 행렬 형태로 표현한 것이다.

```text
        age   fare  pclass
age     1.0   0.1   -0.3
fare    0.1   1.0   -0.5
pclass -0.3  -0.5    1.0
```

Heatmap으로 시각화하는 경우가 많다.

### Correlation ≠ Causation — 상관관계는 인과관계를 의미하지 않는다

매우 중요한 개념이다. 두 변수의 상관관계가 높더라도 "X가 Y의 원인이다"라고 바로 결론내릴 수 없다.

```text
Correlation ≠ Causation
상관관계 ≠ 인과관계
```

### Causality — 인과관계

한 변수가 다른 변수의 변화를 실제로 발생시키는 관계를 의미한다. 상관관계 분석만으로는 일반적으로 인과관계를 증명할 수 없다.

### Covariance — 공분산

두 변수가 함께 변화하는 방향을 나타낸다.

```text
양수 → 같은 방향으로 움직이는 경향
음수 → 반대 방향으로 움직이는 경향
```

다만 값의 크기가 변수 단위에 영향을 받기 때문에 해석하기 어렵다는 단점이 있다. 이를 표준화한 개념이 상관계수라고 볼 수 있다.

---

## 10. 데이터 시각화

### Data Visualization — 데이터 시각화

데이터를 그래프로 표현하여 패턴을 발견하는 과정이다. EDA에서 통계 수치만큼 중요하다.

대표적인 그래프: Histogram, Bar Plot, Box Plot, Scatter Plot, Line Plot, Heatmap, Violin Plot, Pair Plot

### Histogram (히스토그램)

연속형 데이터의 분포를 확인할 때 사용한다. 예를 들어 Age Histogram을 보면 어떤 연령대가 많은지, 분포가 치우쳐 있는지, 이상치가 있는지 등을 확인할 수 있다.

### Bin

Histogram에서 데이터를 묶는 구간을 의미한다. 예를 들어 나이를 0~10, 10~20, 20~30, 30~40처럼 나누었다면 각각의 구간이 Bin이다.

Bin의 개수에 따라 그래프 모양이 크게 달라질 수 있다.

### Bar Plot (막대그래프)

주로 범주형 변수의 빈도나 평균 등을 비교할 때 사용한다. 예를 들어 남성 생존률, 여성 생존률 비교에 사용할 수 있다.

### Count Plot

범주별 데이터 개수를 막대그래프로 표현한다. 예를 들어 남성 577명, 여성 314명처럼 범주의 빈도를 확인할 수 있다.

### Box Plot — 상자 그림

데이터의 분포와 이상치를 확인하는 데 유용하다. 주요 요소는 Q1, Median, Q3, IQR, Outlier이다.

```text
        ┌──────────┐
───|────│────|─────│────|────  ●
        └──────────┘
       Q1 Median   Q3        Outlier
```

### Scatter Plot (산점도)

두 연속형 변수의 관계를 확인할 때 사용한다. 예를 들어 공부시간 vs 시험점수, 키 vs 몸무게, 광고비 vs 매출 등의 관계를 볼 수 있다.

상관관계, 이상치, 그룹 패턴을 발견할 때 유용하다.

### Line Plot (선 그래프)

시간의 흐름에 따른 변화를 분석할 때 많이 사용한다. 연도별 매출, 월별 사고 건수, 일별 방문자 수 등을 분석하는 데 적합하다.

### Heatmap (히트맵)

값의 크기를 색상 차이로 표현하는 그래프이다. EDA에서는 특히 **Correlation Matrix**를 시각화할 때 많이 사용한다.

### Pair Plot

여러 숫자형 Feature 사이의 관계를 한 번에 확인하는 그래프이다. 각 Feature의 분포와 Feature끼리의 산점도를 동시에 볼 수 있다.

### Violin Plot

Box Plot과 비슷하지만 데이터의 **분포 밀도**까지 함께 보여준다. 특정 값 주변에 데이터가 얼마나 몰려 있는지 확인하기 좋다.

### KDE — Kernel Density Estimation

데이터의 확률 밀도를 부드러운 곡선 형태로 추정하여 표현하는 방법이다. Histogram보다 부드럽게 데이터의 분포를 확인할 수 있다.

### Density — 밀도

특정 구간에 데이터가 얼마나 집중되어 있는지를 나타낸다.

---

## 11. Feature 관련 작업

### Feature Engineering — 특성 공학

기존 데이터를 이용하여 모델 학습에 도움이 되는 Feature를 만들거나 변형하는 과정이다.

예를 들어 `birth_year → age`, `sibsp + parch → family_size`, `날짜 → 연도/월/요일` 등이 Feature Engineering이다.

### Feature Selection — 특성 선택

많은 Feature 중 모델에 사용할 Feature만 선택하는 과정이다.

불필요한 Feature를 제거하면 모델 단순화, 학습속도 개선, 과적합 감소, 해석력 향상 등의 효과를 기대할 수 있다.

### Feature Extraction — 특성 추출

기존 데이터에서 새로운 형태의 특징을 추출하는 것이다.

예를 들어 텍스트 데이터를 문장 → 숫자 벡터로 변환하거나, PCA를 통해 여러 Feature를 몇 개의 새로운 Feature로 변환하는 것이 이에 해당한다.

---

## 12. 데이터 전처리

### Data Preprocessing — 데이터 전처리

머신러닝 모델이 학습할 수 있도록 데이터를 정리하고 변환하는 과정이다.

대표적으로 결측치 처리, 이상치 처리, 중복 제거, Encoding, Scaling, Feature Engineering 등이 포함된다.

### Encoding — 인코딩

범주형 데이터를 머신러닝 모델이 처리할 수 있도록 숫자로 변환하는 과정이다.

대표적인 방법: Label Encoding, One-Hot Encoding, Ordinal Encoding

### Label Encoding

범주를 숫자로 변환한다.

```text
Seoul → 0
Busan → 1
Incheon → 2
```

다만 모델이 `2 > 1 > 0`이라는 순서 관계가 존재한다고 잘못 해석할 가능성이 있기 때문에 사용 시 주의해야 한다.

### One-Hot Encoding

범주별 새로운 컬럼을 생성한다.

```text
city
Seoul
Busan
Incheon
```

을

```text
Seoul  Busan  Incheon
1      0      0
0      1      0
0      0      1
```

형태로 변환한다. 순서가 없는 범주형 변수에 많이 사용한다.

### Ordinal Encoding

순서가 존재하는 범주형 데이터를 숫자로 변환한다.

```text
Low    → 0
Medium → 1
High   → 2
```

와 같이 변환할 수 있다.

### Dummy Variable

One-Hot Encoding 등을 통해 생성된 0과 1 형태의 변수이다.

---

## 13. 스케일링과 변환

### Feature Scaling

Feature들의 값 범위를 비슷하게 맞추는 과정이다.

예를 들어 `age`는 20~80, `income`은 1,000,000~100,000,000이라면 값의 범위 차이가 매우 크다. 일부 머신러닝 알고리즘에서는 이런 차이가 학습에 영향을 줄 수 있다.

### Standardization — 표준화

평균을 0, 표준편차를 1에 가깝게 변환한다.

```text
z = (x - mean) / standard deviation
```

Scikit-learn에서는 대표적으로 `StandardScaler`를 사용한다.

### Normalization — 정규화

값을 일정 범위로 조정하는 방법이다. 대표적으로 0~1 사이로 변환하는 Min-Max Scaling이 있다.

### Min-Max Scaling

```text
x' = (x - min) / (max - min)
```

방식으로 데이터를 보통 0~1 사이로 변환한다. Scikit-learn의 `MinMaxScaler`가 대표적이다.

### Robust Scaling

Median과 IQR을 사용하는 Scaling 방법이다. 이상치의 영향을 StandardScaler나 MinMaxScaler보다 적게 받을 수 있다.

### Log Transformation — 로그 변환

오른쪽으로 심하게 치우친 데이터를 완화하기 위해 로그를 적용하는 방법이다. 예를 들어 1, 10, 100, 1000처럼 값 차이가 매우 큰 경우 활용할 수 있다.

### Binning — 구간화

연속형 데이터를 구간별 범주로 변환하는 작업이다. 예를 들어 `age → 10대/20대/30대/40대`로 변환하는 것이 Binning이다.

### Discretization

연속형 데이터를 이산적인 구간이나 범주로 바꾸는 과정이다. Binning과 비슷한 의미로 사용된다.

---

## 14. Target과 클래스 불균형

### Target Distribution — Target 분포

Target 값이 어떻게 구성되어 있는지를 확인하는 것이다. 분류에서는 특히 중요하다.

예를 들어 `0: 950개, 1: 50개`라면 Target이 심하게 불균형한 상태이다.

### Class — 클래스

분류 문제에서 예측하려는 각각의 범주를 의미한다. 예를 들어 생존 예측에서는 `0=사망, 1=생존`으로 총 2개의 Class가 있다.

### Class Imbalance — 클래스 불균형

특정 Class의 데이터가 다른 Class보다 훨씬 많은 상태이다. 예를 들어 정상 99%, 사기 1% 같은 경우이다.

사기 탐지, 질병 진단, 이상 탐지 등의 데이터에서 자주 발생한다.

- **Majority Class**: 데이터가 더 많이 존재하는 Class
- **Minority Class**: 데이터가 적게 존재하는 Class

### Oversampling / Undersampling

- **Oversampling**: Minority Class 데이터를 늘려 데이터 불균형을 완화하는 방법
- **Undersampling**: Majority Class 데이터를 줄여 데이터 불균형을 완화하는 방법

### SMOTE — Synthetic Minority Over-sampling Technique

Minority Class의 기존 데이터를 기반으로 새로운 샘플을 생성하여 데이터 수를 늘리는 방법이다. 단순히 데이터를 복사하는 것과는 차이가 있다.

---

## 15. 데이터 분할

### Training Data — 학습 데이터

머신러닝 모델이 실제로 패턴을 학습할 때 사용하는 데이터이다.

### Testing Data — 테스트 데이터

학습이 끝난 모델의 성능을 최종적으로 평가하는 데이터이다. 모델 학습 과정에서는 사용하지 않는 것이 원칙이다.

### 검증 데이터 (Validation Data)

모델이나 Hyperparameter를 선택하는 과정에서 성능을 확인하기 위해 사용하는 데이터이다.

일반적으로 Train, Validation, Test 세 영역으로 나눌 수 있다.

### Train-Test Split

데이터를 학습용 데이터와 테스트용 데이터로 나누는 과정이다. 예를 들어 Train 80%, Test 20%처럼 나눌 수 있다.

### Random State

데이터 분할이나 난수 생성 결과를 재현하기 위해 사용하는 Seed 값이다. 같은 `random_state`를 사용하면 일반적으로 같은 방식으로 데이터가 나뉘므로 실험 결과를 비교하기 편하다.

### Seed

난수 생성의 시작 기준값이다. 머신러닝 실험을 재현하기 위해 사용한다.

### Stratify

Train/Test를 나눌 때 Target Class의 비율을 비슷하게 유지하도록 하는 옵션이다. 예를 들어 전체 데이터가 0:80%, 1:20%라면 Train과 Test도 비슷한 비율을 유지하도록 나눌 수 있다.

---

## 16. 데이터 누수

### Data Leakage — 데이터 누수

모델이 실제 예측 시점에는 알 수 없는 정보를 학습 과정에서 미리 알게 되는 문제이다.

시험 문제 정답을 공부한 뒤 시험 보는 것과 비슷하다. 성능은 매우 높게 나오지만 실제 서비스에서는 성능이 떨어질 수 있다.

### Target Leakage

Target과 직접적으로 연결된 정보를 Feature로 사용하는 경우이다. 예를 들어 대출 연체 여부를 예측하면서 "연체 후 부과된 벌금" 같은 Feature를 사용하는 경우가 될 수 있다.

### Scaling Leakage

Train/Test 전체 데이터에 먼저 Scaling을 적용하면 Test 데이터 정보가 Train 데이터에 간접적으로 반영될 수 있다.

따라서 일반적으로 다음 순서를 사용한다.

```text
Train으로 scaler 학습
↓
Train 변환
↓
같은 scaler로 Test 변환
```

---

## 17. 표본과 편향

### Sampling — 표본 추출

전체 데이터 중 일부 데이터를 선택하는 과정이다.

### Population — 모집단

분석하고자 하는 전체 대상이다.

### Sample — 표본

모집단에서 추출한 일부 데이터이다.

### Sampling Bias — 표본편향

표본이 모집단을 제대로 대표하지 못하는 문제이다. 예를 들어 "대한민국 전체 소비 패턴"을 분석하면서 서울 20대만 조사한다면 전체 인구를 제대로 대표하지 못할 수 있다.

### Selection Bias — 선택편향

데이터를 선택하는 과정에서 특정 집단이 과도하게 포함되거나 제외되면서 발생하는 편향이다.

### Bias — 편향

모델이나 데이터가 특정 방향으로 체계적으로 치우치는 현상을 의미한다. 머신러닝에서는 여러 의미로 사용되므로 문맥을 확인해야 한다.

---

## 18. 잡음과 다중공선성

### Noise — 잡음

실제 패턴과 관계없는 불필요한 변동이나 오류를 의미한다. 예를 들어 센서 측정 오류, 잘못 입력된 값, 랜덤한 변동 등이 Noise가 될 수 있다.

### Signal

데이터 안에서 실제 예측에 도움이 되는 의미 있는 패턴을 말한다. 따라서 머신러닝의 목표를 간단하게 표현하면 "Noise 속에서 Signal을 찾아내는 것"이라고 볼 수도 있다.

### Multicollinearity — 다중공선성

Feature들끼리 매우 강한 상관관계를 가지는 현상이다. 예를 들어 키(cm)와 키(m)를 동시에 Feature로 사용하면 거의 같은 정보를 두 번 사용하는 셈이다.

특히 선형 회귀 모델의 계수 해석에 문제를 일으킬 수 있다.

### VIF — Variance Inflation Factor

다중공선성의 정도를 측정하는 지표 중 하나이다. VIF 값이 높을수록 다른 Feature들과 강하게 연결되어 있을 가능성이 있다.

단, 특정 기준값 하나만으로 무조건 Feature를 제거하기보다는 데이터와 분석 목적을 함께 고려해야 한다.

---

## 19. 차원 축소

### High Dimensionality — 고차원 데이터

Feature의 개수가 매우 많은 데이터이다. Feature가 지나치게 많아질 경우 학습 비용이 증가하고 과적합 위험도 커질 수 있다.

### Curse of Dimensionality — 차원의 저주

Feature가 지나치게 많아질수록 데이터 공간이 매우 넓어지면서 데이터 간 거리나 밀도 기반 분석이 어려워지는 현상을 의미한다.

### Dimensionality Reduction — 차원 축소

많은 Feature를 더 적은 수의 Feature로 축소하는 과정이다. 대표적인 방법: PCA, t-SNE, UMAP

### PCA — Principal Component Analysis (주성분 분석)

여러 Feature가 가지고 있는 정보를 가능한 많이 유지하면서 더 적은 수의 새로운 축으로 데이터를 변환하는 차원 축소 기법이다.

- **Principal Component**: PCA를 통해 새롭게 생성된 축 또는 Feature. `PC1, PC2, PC3` 등으로 표현한다.
- **Explained Variance**: PCA에서 각 주성분이 원래 데이터의 변동성을 얼마나 설명하는지를 나타낸다.

### t-SNE

고차원 데이터를 2차원이나 3차원으로 표현하여 데이터의 군집 구조를 시각적으로 탐색할 때 많이 사용하는 차원 축소 방법이다. 주로 시각화 목적으로 사용한다.

### UMAP

고차원 데이터를 낮은 차원으로 축소하는 방법 중 하나이다. 클러스터 구조를 탐색하거나 고차원 데이터를 시각화할 때 활용된다.

---

## 20. 집계와 그룹 분석

### GroupBy

데이터를 특정 기준으로 그룹화하여 통계를 계산하는 과정이다. 예를 들어 성별별 생존률, 연령대별 평균 운임, 지역별 사고 건수 등을 계산할 수 있다. EDA에서 매우 자주 사용한다.

### Aggregation — 집계

여러 개의 데이터를 하나의 통계값으로 요약하는 과정이다. 대표적인 Aggregation Function: `sum, mean, median, count, min, max, std`

### Pivot Table — 피벗 테이블

데이터를 행과 열 기준으로 재구성하여 집계 결과를 확인하는 방법이다.

```text
          남자   여자
1등급      100    90
2등급      80     70
3등급      200    150
```

처럼 두 범주를 동시에 비교할 수 있다.

### Crosstab — 교차표

두 범주형 변수의 관계를 빈도 형태로 확인할 때 사용한다. 예를 들어 성별×생존여부, 객실등급×생존여부 등을 분석할 수 있다.

### Contingency Table

Crosstab과 같이 범주형 변수들의 빈도를 정리한 표를 의미한다.

---

## 21. 변량 분석

### Univariate Analysis — 단변량 분석

하나의 변수만 분석하는 것이다. 예를 들어 `age` 하나를 대상으로 평균, 중앙값, 분포, 이상치를 분석한다.

### Bivariate Analysis — 이변량 분석

두 변수 사이의 관계를 분석한다. 예를 들어 성별 vs 생존률, 나이 vs 운임, 광고비 vs 매출 등을 분석한다.

### Multivariate Analysis — 다변량 분석

3개 이상의 변수를 동시에 분석하는 것이다. 예를 들어 성별+연령+객실등급+생존여부 등의 관계를 함께 분석한다.

### Segmentation

전체 데이터를 특정 조건에 따라 여러 집단으로 나누는 것을 의미한다. 예를 들어 10대/20대/30대 또는 남성/여성 등으로 구분하여 분석할 수 있다.

### Pattern — 패턴

데이터에서 반복적으로 나타나는 규칙이나 관계를 의미한다. EDA의 중요한 목적 중 하나는 데이터의 Pattern을 발견하는 것이다.

---

## 22. 시계열 관련 개념

### Trend — 추세

시간의 흐름에 따라 데이터가 장기적으로 증가하거나 감소하는 방향을 의미한다. 예를 들어 연도별 사고 건수 증가, 월별 매출 감소 등이다.

### Seasonality — 계절성

일정한 주기로 반복되는 패턴이다. 예를 들어 여름마다 아이스크림 판매 증가, 주말마다 방문자 증가, 겨울마다 난방비 증가 등이 있다.

### Time Series — 시계열 데이터

시간 순서대로 기록된 데이터이다. 예시: 일별 주가, 월별 매출, 연도별 인구, 시간대별 교통사고

### Time Index

시계열 데이터에서 시간을 나타내는 기준값이다. 날짜, 시간, 연도, 월 등이 해당한다.

### Lag — 시차

이전 시점의 값을 의미한다. 예를 들어 오늘 매출, 어제 매출 = Lag 1, 일주일 전 매출 = Lag 7처럼 사용할 수 있다.

### Rolling Window

일정한 기간의 데이터를 이동하면서 통계량을 계산하는 방식이다. 예를 들어 7일 이동평균, 30일 이동평균 등이 있다.

### Moving Average — 이동평균

일정 기간의 평균을 계속 이동하면서 계산하는 방법이다. 데이터의 단기적인 변동을 완화하고 전체적인 Trend를 파악할 때 유용하다.

### Stationarity — 정상성

시계열 데이터의 통계적 특성이 시간에 따라 크게 변하지 않는 성질이다. ARIMA 등의 시계열 모델에서 중요한 개념이다.

---

## 23. 분포 변화

### Distribution Shift — 데이터 분포 변화

Train 데이터와 실제 예측 환경의 데이터 분포가 달라지는 현상이다. 예를 들어 2020년 고객 데이터로 학습했는데 2026년 고객 행동이 크게 변화한다면 모델 성능이 떨어질 수 있다.

### Data Drift

시간이 지나면서 입력 데이터의 분포가 변하는 현상이다.

### Concept Drift

입력과 Target 사이의 관계 자체가 시간에 따라 변하는 현상이다. 예를 들어 과거와 현재의 소비 패턴이 달라져 동일한 Feature가 Target에 미치는 영향이 달라질 수 있다.

---

## 24. 모델 적합 관련

### Baseline Model

복잡한 모델을 만들기 전에 비교 기준으로 사용하는 간단한 모델이다. 예를 들어 평균값으로 예측, 최빈 Class로 예측, 간단한 Logistic Regression 등을 Baseline으로 사용할 수 있다.

### Overfitting — 과적합

모델이 Training Data에 지나치게 맞춰져 새로운 데이터에서는 성능이 떨어지는 현상이다.

```text
Train 성능 ↑↑
Test 성능 ↓
```

형태가 대표적이다. 쉽게 말하면 "문제를 이해한 것이 아니라 학습 문제를 외워버린 상태"라고 볼 수 있다.

### Underfitting — 과소적합

모델이 데이터의 패턴을 충분히 학습하지 못한 상태이다.

```text
Train 성능 ↓
Test 성능 ↓
```

가 나타나는 경우가 많다.

### Generalization — 일반화

모델이 학습한 적 없는 새로운 데이터에서도 좋은 성능을 내는 능력이다. 머신러닝의 궁극적인 목표 중 하나이다.

### Bias-Variance Tradeoff — 편향-분산 Trade-off

모델이 너무 단순하면 Underfitting이 발생할 수 있고, 너무 복잡하면 Overfitting이 발생할 수 있다. 이 둘의 균형을 맞추는 것이 중요한 문제이다.

---

## 25. 교차검증

### Cross Validation — 교차검증

데이터를 여러 부분으로 나누어 반복적으로 학습과 검증을 진행하는 방법이다. 모델의 성능을 보다 안정적으로 평가할 수 있다.

### K-Fold Cross Validation

데이터를 K개의 그룹으로 나누어 한 그룹씩 Validation Data로 사용한다. 예를 들어 `5-Fold`라면

```text
1 2 3 4 → Train / 5 → Validation
1 2 3 5 → Train / 4 → Validation
...
```

처럼 총 5번 평가한다.

### Stratified K-Fold

분류 문제에서 각 Fold의 Class 비율을 비슷하게 유지하면서 Cross Validation을 수행한다.

---

## 26. 모델과 파라미터

### Model — 모델

Feature를 입력받아 Target을 예측하도록 학습된 함수 또는 알고리즘이라고 볼 수 있다.

```text
Feature
   ↓
Model
   ↓
Prediction
```

### Algorithm — 알고리즘

데이터를 이용해 모델을 학습하는 방법이다. 예를 들어 Linear Regression, Logistic Regression, Decision Tree, Random Forest, XGBoost, KNN, SVM 등이 있다.

### Parameter — 파라미터

모델이 데이터를 학습하면서 자동으로 결정하는 값이다. 예를 들어 Linear Regression의 회귀계수, Intercept 등이 Parameter에 해당한다.

### Hyperparameter — 하이퍼파라미터

모델이 학습하기 전에 사람이 설정하는 값이다. 예를 들어 `max_depth, n_estimators, learning_rate, k` 등이 있다.

### Hyperparameter Tuning

모델의 성능을 높이기 위해 적절한 Hyperparameter를 찾는 과정이다.

- **Grid Search**: 미리 지정한 Hyperparameter 조합을 모두 탐색하여 좋은 조합을 찾는 방법이다.
- **Random Search**: 지정된 Hyperparameter 범위에서 일부 조합을 랜덤하게 탐색하는 방법이다.

---

## 27. 학습 방식과 문제 유형

### 지도학습 (Supervised Learning)

정답인 Target이 존재하는 데이터로 학습하는 방식이다. 대표적으로 Classification, Regression이 있다.

### 비지도학습 (Unsupervised Learning)

정답 Target 없이 데이터의 구조나 패턴을 찾는 학습 방식이다. 대표적으로 Clustering, Dimensionality Reduction 등이 있다.

### 분류 (Classification)

범주를 예측하는 머신러닝 문제이다. 예를 들어 생존/사망, 정상/사기, 스팸/정상 등을 예측한다.

- **Binary Classification**: 두 개의 Class 중 하나를 예측하는 문제 (`0/1`, `True/False`)
- **Multiclass Classification**: 3개 이상의 Class 중 하나를 예측한다 (예: 고양이/강아지/토끼)

### 회귀 (Regression)

연속적인 숫자 값을 예측하는 문제이다. 예를 들어 집값, 매출, 온도, 수요량 등을 예측한다.

### 군집화 (Clustering)

정답 없이 비슷한 데이터끼리 그룹을 만드는 비지도학습 방법이다. 대표적인 알고리즘: K-Means, DBSCAN, Hierarchical Clustering

**Cluster**: Clustering으로 생성된 하나의 데이터 그룹을 의미한다.

---

## 28. 평가 지표 - 분류

### 평가 지표 (Evaluation Metric)

머신러닝 모델의 성능을 숫자로 평가하기 위한 기준이다. 분류와 회귀에서 사용하는 평가 지표가 다르다.

### Accuracy — 정확도

전체 예측 중 맞게 예측한 비율이다.

```text
Accuracy = 맞춘 개수 / 전체 데이터
```

Class가 균형 잡힌 데이터에서는 이해하기 쉽지만 불균형 데이터에서는 주의해야 한다.

### Confusion Matrix — 혼동행렬

분류 모델의 예측 결과를 다음 4가지로 구분한다: `TP, TN, FP, FN`

- **True Positive (TP)**: 실제 Positive인데 모델도 Positive라고 예측했다. (예: 실제 암 환자 → 암이라고 예측)
- **True Negative (TN)**: 실제 Negative인데 모델도 Negative라고 예측했다.
- **False Positive (FP)**: 실제 Negative인데 Positive라고 잘못 예측했다. (예: 정상 → 암이라고 예측)
- **False Negative (FN)**: 실제 Positive인데 Negative라고 잘못 예측했다. (예: 암 환자 → 정상이라고 예측)

### Precision — 정밀도

모델이 Positive라고 예측한 데이터 중 실제 Positive인 비율이다.

```text
Precision = TP / (TP + FP)
```

### Recall — 재현율

실제 Positive 데이터 중 모델이 Positive로 찾아낸 비율이다.

```text
Recall = TP / (TP + FN)
```

민감도라고 부르기도 한다.

### Sensitivity

Recall과 동일하거나 매우 유사한 의미로 사용된다.

```text
Sensitivity = TP / (TP + FN)
```

### Specificity

실제 Negative 중 모델이 Negative로 정확히 찾아낸 비율이다.

```text
Specificity = TN / (TN + FP)
```

### F1-Score

Precision과 Recall의 조화평균이다.

```text
F1 = 2 × Precision × Recall / (Precision + Recall)
```

Precision과 Recall을 함께 고려하고 싶을 때 사용한다.

### Probability — 예측 확률

분류 모델이 특정 Class에 속할 가능성을 확률 형태로 출력할 수 있다. 예를 들어 생존 확률 = 0.87 같은 형태이다.

### Threshold — 임계값

예측 확률을 실제 Class로 변환하는 기준이다.

```text
Probability ≥ 0.5 → 1
Probability < 0.5 → 0
```

처럼 사용할 수 있다. Threshold를 변경하면 Precision과 Recall도 달라질 수 있다.

### ROC Curve — Receiver Operating Characteristic Curve

Threshold를 변경하면서 True Positive Rate와 False Positive Rate의 관계를 표현한 그래프이다.

### AUC — Area Under the Curve

ROC Curve 아래의 면적이다. 모델이 Positive와 Negative를 얼마나 잘 구분하는지 평가하는 지표 중 하나이다. 보통 값이 클수록 구분 능력이 좋은 것으로 해석한다.

---

## 29. 평가 지표 - 회귀

### MAE — Mean Absolute Error

실제값과 예측값 차이의 절댓값 평균이다. `|Actual - Prediction|`을 평균낸다. 단위가 원래 Target과 같아 비교적 직관적이다.

### MSE — Mean Squared Error

오차를 제곱한 후 평균을 계산한다. 큰 오차에 더 큰 패널티가 적용된다.

### RMSE — Root Mean Squared Error

MSE에 제곱근을 적용한 값이다. Target과 단위가 같기 때문에 MSE보다 직관적으로 해석하기 쉽다.

### MAPE — Mean Absolute Percentage Error

실제값 대비 예측 오차를 백분율로 계산한다. 예를 들어 `MAPE = 10%`이라면 평균적으로 실제값 대비 약 10% 수준의 오차가 발생했다는 식으로 해석할 수 있다.

다만 실제값이 0이거나 매우 작은 경우 문제가 발생할 수 있다.

### R² — R-Squared (결정계수)

회귀 모델이 Target의 변동을 얼마나 설명하는지를 나타내는 대표적인 지표이다. 일반적으로 값이 1에 가까울수록 설명력이 높은 것으로 해석한다.

단, R² 하나만으로 모델의 성능을 판단해서는 안 된다.

### Residual — 잔차

실제값과 모델 예측값의 차이이다.

```text
Residual = Actual - Prediction
```

회귀 모델에서는 잔차의 패턴을 확인하는 것도 중요하다.

### 잔차 분석 (Residual Analysis)

잔차가 특정 패턴 없이 랜덤하게 분포하는지 확인하는 과정이다. 잔차에 뚜렷한 패턴이 있다면 모델이 데이터의 구조를 충분히 설명하지 못하고 있을 가능성이 있다.

---

## 30. 모델 해석

### Feature Importance — 변수 중요도

각 Feature가 모델 예측에 얼마나 중요한 역할을 했는지를 나타내는 값이다. Tree 계열 모델에서 자주 확인한다.

단, Feature Importance가 높다고 해당 Feature가 Target의 원인이라는 의미는 아니다.

### Permutation Importance

특정 Feature의 값을 무작위로 섞었을 때 모델 성능이 얼마나 감소하는지를 이용하여 Feature 중요도를 평가하는 방식이다.

### SHAP Value

각 Feature가 개별 예측 결과에 얼마나 영향을 주었는지 설명하는 데 사용되는 방법이다.

예를 들어

```text
Age       → 생존 확률 -0.1
Sex       → 생존 확률 +0.3
Pclass    → 생존 확률 -0.2
```

처럼 해석할 수 있다.

---

## 31. EDA 실전 체크리스트

### EDA에서 가장 먼저 확인할 것

실제 데이터를 받으면 보통 다음 순서로 살펴볼 수 있다.

```text
1. 데이터 크기 확인
        ↓
2. 컬럼 확인
        ↓
3. 데이터 타입 확인
        ↓
4. Feature / Target 확인
        ↓
5. 결측치 확인
        ↓
6. 중복 데이터 확인
        ↓
7. 고유값 확인
        ↓
8. 기술통계 확인
        ↓
9. 데이터 분포 확인
        ↓
10. 이상치 확인
        ↓
11. 범주별 빈도 확인
        ↓
12. Feature 간 관계 분석
        ↓
13. Feature와 Target 관계 분석
        ↓
14. 상관관계 확인
        ↓
15. 데이터 불균형 확인
        ↓
16. 전처리 방향 결정
```

### `info()`에서 확인해야 하는 것

```python
df.info()
```

EDA를 시작할 때 굉장히 중요한 함수이다. 여기서 확인해야 할 것:

- 전체 데이터 개수
- 컬럼 개수
- Non-Null Count
- 결측치 여부
- 데이터 타입
- 메모리 사용량

예를 들어

```text
891 entries
age       714 non-null
fare      891 non-null
```

이라면 전체 데이터 = 891, age 데이터 = 714이므로 Age에 결측치가 있다는 것을 알 수 있다.

### `describe()`에서 확인해야 하는 것

```python
df.describe()
```

대표적으로 다음 값을 확인한다: `count, mean, std, min, 25%, 50%, 75%, max`

특히 `min, max, mean, median`을 비교하면 이상치나 데이터 분포를 빠르게 파악할 수 있다.

### `unique()`와 `nunique()`

```python
unique()
```

는 실제 고유값을 보여준다 (예: `male, female`). 반면

```python
nunique()
```

는 고유값의 개수를 반환한다 (예: `2`).

### `value_counts()`

범주형 데이터를 분석할 때 가장 많이 사용하는 함수 중 하나이다. 각 값이 몇 번 등장했는지 확인한다.

```text
male      577
female    314
```

Class Imbalance나 범주 분포를 확인할 때 유용하다.

### `isnull()` / `isna()`

결측치 여부를 확인한다. 보통

```python
df.isnull().sum()
```

또는

```python
df.isna().sum()
```

으로 컬럼별 결측치 개수를 확인한다.

### `duplicated()`

중복 데이터 여부를 확인한다.

### `corr()`

숫자형 Feature들의 상관계수를 확인한다. 상관관계 Heatmap을 만들 때 자주 사용한다.

---

## 32. 용어 빠른 참조표

| 용어 | 의미 |
|---|---|
| Dataset | 전체 데이터 |
| Observation | 하나의 관측 데이터 |
| Sample | 샘플 |
| Feature | 입력 변수 |
| Target | 예측 대상 |
| Label | 정답 |
| Row | 행 |
| Column | 열 |
| Numerical | 숫자형 |
| Categorical | 범주형 |
| Continuous | 연속형 |
| Discrete | 이산형 |
| Nominal | 명목형 |
| Ordinal | 순서형 |
| Binary | 이진형 |
| Missing Value | 결측치 |
| Duplicate | 중복 |
| Outlier | 이상치 |
| Mean | 평균 |
| Median | 중앙값 |
| Mode | 최빈값 |
| Variance | 분산 |
| Standard Deviation | 표준편차 |
| Quantile | 분위수 |
| IQR | 사분위 범위 |
| Distribution | 분포 |
| Skewness | 왜도 |
| Kurtosis | 첨도 |
| Correlation | 상관관계 |
| Covariance | 공분산 |
| Visualization | 시각화 |
| Feature Engineering | 특성 공학 |
| Feature Selection | 특성 선택 |
| Encoding | 인코딩 |
| Scaling | 스케일링 |
| Standardization | 표준화 |
| Normalization | 정규화 |
| Imputation | 결측치 대체 |
| Binning | 구간화 |
| Class Imbalance | 클래스 불균형 |
| Sampling | 표본 추출 |
| Bias | 편향 |
| Noise | 잡음 |
| Multicollinearity | 다중공선성 |
| Train Data | 학습 데이터 |
| Validation Data | 검증 데이터 |
| Test Data | 테스트 데이터 |
| Data Leakage | 데이터 누수 |
| Overfitting | 과적합 |
| Underfitting | 과소적합 |
| Generalization | 일반화 |
| Cross Validation | 교차검증 |
| Parameter | 파라미터 |
| Hyperparameter | 하이퍼파라미터 |
| Classification | 분류 |
| Regression | 회귀 |
| Clustering | 군집화 |
| Accuracy | 정확도 |
| Precision | 정밀도 |
| Recall | 재현율 |
| F1-Score | F1 점수 |
| MAE | 평균 절대 오차 |
| MSE | 평균 제곱 오차 |
| RMSE | 평균 제곱근 오차 |
| R² | 결정계수 |
| Residual | 잔차 |
| Feature Importance | 변수 중요도 |

---

## 33. EDA를 왜 해야 할까

머신러닝에서는 좋은 알고리즘을 선택하는 것만큼 **데이터를 이해하는 것이 중요하다.**

EDA를 제대로 하지 않고 모델부터 학습시키면 다음을 발견하지 못할 수 있다.

- 잘못된 데이터 타입
- 결측치
- 이상치
- 데이터 누수
- 클래스 불균형
- 잘못된 Feature
- 중복 데이터
- 편향된 데이터

그러면 모델의 Accuracy가 높게 나오더라도 실제로는 제대로 된 모델이 아닐 수 있다.

따라서 머신러닝 프로젝트에서는 보통 다음 순서로 진행하게 된다.

```text
문제 정의
    ↓
데이터 수집
    ↓
EDA
    ↓
데이터 전처리
    ↓
Feature Engineering
    ↓
Train / Test Split
    ↓
모델 학습
    ↓
모델 평가
    ↓
모델 개선
```

### 💡 정리

EDA의 핵심은 단순히 `describe()`나 그래프를 출력하는 것이 아니다. 결국 EDA를 통해 알아내야 하는 것은 다음과 같다.

> **이 데이터가 어떤 데이터인가?**
> **데이터에 문제가 있는가?**
> **각 변수는 어떤 특징을 가지고 있는가?**
> **Feature끼리는 어떤 관계를 가지고 있는가?**
> **어떤 Feature가 Target과 관계가 있는가?**
> **머신러닝에 사용하기 전에 무엇을 전처리해야 하는가?**

즉,

```text
EDA
= 데이터 확인
+ 데이터 이해
+ 문제 발견
+ 패턴 탐색
+ 모델링 방향 결정
```

이라고 정리할 수 있다.

머신러닝 모델을 만드는 과정에서 **EDA는 모델 학습 전에 하는 부가적인 작업이 아니라, 모델링 방향을 결정하는 핵심 과정**이다.
