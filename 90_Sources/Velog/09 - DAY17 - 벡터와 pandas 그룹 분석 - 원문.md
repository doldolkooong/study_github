---
type: source
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY17-26.08.28"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY17 (26.08.28)"
source_id: 58aea05f-32a3-4705-bc9a-17a28e2a7ea9
source_author: doldolkoong
source_published: 2026-08-28
source_updated: 2026-09-04
archived: 2026-09-08
tags:
  - velog-source
---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY17 (26.08.28)

[Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY17-26.08.28) · [[DAY17 - 벡터와 pandas 그룹 분석|DAY17 - 벡터와 pandas 그룹 분석]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY17 (26.08.28)

## 📖 오늘 학습 내용

> 1. numpy 복습
> 2. numpy 심화 - 벡터와 독립변수
> 3. 행렬곱
> 4. Norm
> 5. pandas
> 6. Series
> 7. DataFrame
> 8. iris 데이터셋으로 분석해보기
> 9. map()
> 10. apply()
> 11. 문제 - 10대, 20대, 30대 생존률 구하기

오늘은 전날 배웠던 numpy의 `shape`, `axis` 개념을 간단하게 복습한 뒤, 벡터와 행렬에 대한 내용을 조금 더 깊게 학습했다.

이후 본격적으로 **pandas**를 사용해 Series와 DataFrame을 다루고, 실제 `iris`, `titanic` 데이터셋을 이용해서 조건 검색, 그룹화, 데이터 변환 등을 실습했다.

---

# 1. numpy 복습

먼저 전날 배웠던 numpy의 `reshape`, `shape`, `axis` 개념을 복습했다.

```python
import numpy as np

arr = np.arange(20)

arr.shape

> (20,)
```


현재 `arr`은 데이터가 20개 들어있는 1차원 벡터다.

이를 `reshape()`을 이용해서 4 × 5 형태의 행렬로 변경할 수 있다.

```python
arr1 = arr.reshape(4, 5)

arr1.shape
```

```text
(4, 5)
```

## vector → scalar

벡터에 `max()`, `min()`, `mean()` 같은 연산을 수행하면 여러 개의 데이터에서 하나의 값이 나오게 된다.

즉,

> vector → scalar

형태가 된다.

```python
arr.max()
```

```text
19
```

---

## axis

행렬의 shape이 다음과 같다고 해보자.

```python
arr1.shape
```

```text
(4, 5)
```

즉,

```text
(row, column)
( 4 ,   5   )
```

형태다.

`axis`는 **어떤 차원을 없앨 것인지** 생각하면 이해하기 쉽다.

### axis = 1

```python
arr1.min(axis=1)
```

```text
array([ 0,  5, 10, 15])
```

`axis=1`이면 column 차원이 없어지고 각 row마다 하나의 결과가 나온다.

```text
(4, 5)
   ↓
(4,)
```

### axis = 0

```python
arr1.min(axis=0)
```

```text
array([0, 1, 2, 3, 4])
```

이번에는 row 차원이 없어지고 각 column별 결과가 남는다.

```text
(4, 5)
   ↓
(5,)
```

---

# 2. numpy 심화

## Scalar / Vector

머신러닝 관점에서 생각하면 다음과 같이 볼 수 있다.

```text
Scalar = 데이터 하나
Vector = 하나의 변수(feature)
```

머신러닝에서는 데이터를 이용해 어떤 결과를 예측하게 되는데 이때 변수를 **독립변수와 종속변수**로 나눌 수 있다.

### 독립변수

종속변수를 예측하기 위해 사용하는 변수이다.

### 종속변수

우리가 최종적으로 예측하고 싶은 값이다.

```text
독립변수(feature)
        ↓
      Model
        ↓
종속변수(target)
```

---

## 벡터 사이의 관계

벡터는 크기뿐만 아니라 **방향**을 가지고 있다.

예를 들어 다음 두 벡터를 생각할 수 있다.

```text
(1, 0)
(0, 1)
```

두 벡터는 서로 직교한다.

### 직교

두 변수 사이의 변화 관계가 거의 없는 상태로 생각할 수 있다.

예를 들어

```text
마을 인구수 변화
        ↓
수확량 변화 없음
```

이라면 두 변수의 관계가 크지 않다고 볼 수 있다.

머신러닝에서는 독립변수끼리 지나치게 비슷한 정보를 가지고 있으면 모델에 좋지 않은 영향을 줄 수 있기 때문에 변수 간 관계를 확인하는 것이 중요하다.

---

## 유사도

벡터 사이의 방향을 이용하면 데이터가 얼마나 유사한지도 확인할 수 있다.

대표적인 방법이 **Cosine Similarity(코사인 유사도)**이다.

```text
방향이 비슷함
→ 유사도가 높음

방향이 다름
→ 유사도가 낮음
```

LLM에서도 문장이나 단어 등을 벡터로 표현하고, 벡터 간 유사도를 이용하는 방식이 많이 사용된다.

다만 서로 다른 단위의 값을 비교할 때는 단위를 맞춰줘야 한다.

예를 들어

```text
v1 = 10cm
v2 = 5m
```

를 그대로 비교하기보다는

```text
v1 = 0.1m
v2 = 5m
```

처럼 단위를 통일해서 비교해야 한다.

---

# 3. 행렬곱

행렬곱에서는 **shape**을 확인하는 것이 중요하다.

예를 들어

```text
A = (2, 2)
B = (2, 2)
```

이면

```text
AB = (2, 2) × (2, 2)
```

의 연산이 가능하다.

행렬곱이 가능하려면

> A의 column 개수와 B의 row 개수가 같아야 한다.

예를 들어

```text
(2, 5) × (5, 3)
```

은 가운데의 `5`가 같기 때문에 행렬곱이 가능하다.

결과 shape은 바깥쪽 숫자를 가져온다.

```text
(2, 5) × (5, 3)
   └─────┘
   같아야 함

결과 → (2, 3)
```

따라서 행렬을 다룰 때는 단순히 숫자만 보는 것이 아니라

> 각각의 차원이 무엇을 의미하고 현재 shape이 어떻게 되어 있는지

확인하는 것이 중요하다.

---

# 4. Norm

**Norm**은 벡터의 크기 또는 두 벡터 사이의 거리를 계산할 때 사용하는 개념이다.

## L1 Norm

각 원소의 차이에 절댓값을 적용한 뒤 모두 더한다.

```text
|x₁ - y₁| + |x₂ - y₂| + ...
```

이를 **맨해튼 거리(Manhattan Distance)**라고도 한다.

이름 그대로 격자 형태의 길을 따라 이동하는 거리라고 생각하면 된다.

---

## L2 Norm

각 원소의 차이를 제곱하고 모두 더한 다음 제곱근을 계산한다.

```text
√((x₁-y₁)² + (x₂-y₂)² + ...)
```

이를 **유클리드 거리(Euclidean Distance)**라고 한다.

두 점 사이를 직선으로 연결했을 때의 거리라고 생각할 수 있다.

```text
L1 → 맨해튼 거리
L2 → 유클리드 거리
```

---

# 5. pandas

numpy에서는 벡터, 행렬, 텐서를 모두 `array`라는 하나의 객체로 표현한다.

반면 pandas에서는 1차원과 2차원 데이터를 명확하게 구분한다.

```text
1차원 → Series
2차원 → DataFrame
```

일반적으로 우리가 사용하는 엑셀이나 RDB의 테이블 형태 데이터는 2차원이기 때문에 pandas의 DataFrame으로 표현할 수 있다.

```python
import pandas as pd
```

---

# 6. Series

`Series`는 pandas에서 사용하는 **1차원 Vector 객체**이다.

```python
data = {
    "a": 1,
    "b": 2,
    "c": 3
}

pd.Series(data=data, dtype=np.int16)
```

```text
a    1
b    2
c    3
dtype: int16
```

하나의 값을 여러 index에 넣는 것도 가능하다.

```python
pd.Series(
    data=5.0,
    index=['a', 'b', 'c']
)
```

```text
a    5.0
b    5.0
c    5.0
dtype: float64
```

---

## 정규분포 형태의 Series

`np.random.randn()`을 이용하면 정규분포 형태의 랜덤 데이터를 만들 수 있다.

```python
arr = pd.Series(
    data=np.random.randn(5)
)
```

조건을 만들어 원하는 데이터만 가져올 수도 있다.

```python
cond = arr > 0

arr[cond]
```

또는 평균보다 큰 데이터만 추출할 수도 있다.

```python
cond = arr > arr.mean()

arr[cond]
```

이처럼 pandas에서도 numpy와 마찬가지로 **Boolean Masking**을 사용할 수 있다.

---

# 7. DataFrame

DataFrame은 pandas에서 사용하는 **2차원 Matrix 객체**이다.

```python
data = {
    "one": pd.Series(data=np.random.randn(5)),
    "two": pd.Series(data=np.random.randn(5))
}

df = pd.DataFrame(data=data)

df
```

```text
        one       two
0  0.866470  0.546046
1  1.228915 -0.785753
2 -0.391060 -0.055473
3 -1.306093 -0.214729
4  2.405672  1.135055
```

shape을 확인하면

```python
df.shape
```

```text
(5, 2)
```

이다.

DataFrame에서는

```text
row    = 데이터의 양
column = 변수의 수
```

라고 생각할 수 있다.

머신러닝에서는 column에 **feature와 target**이 들어가게 된다.

---

## Series 가져오기

DataFrame에서 하나의 column을 가져오면 Series가 된다.

```python
df['one']
```

```text
0    0.225197
1   -0.393320
2    0.366827
3   -0.071403
4    1.357561
Name: one, dtype: float64
```

즉,

```text
DataFrame
   ↓ column 하나 선택
Series
```

가 된다.

---

## 새로운 컬럼 생성

기존 column을 이용해서 새로운 column을 만들 수도 있다.

```python
df['new'] = df['one'] + df['two']
```

조건을 걸어 마스킹할 수도 있다.

```python
df['new'] > 0
```

```text
0    False
1     True
2     True
3     True
4     True
```

True인 데이터만 가져오려면

```python
df[df['new'] > 0]
```

처럼 사용한다.

---

## 컬럼 이름 변경

```python
df.columns = ['1', '2', '3']
```

list comprehension을 이용하면 모든 컬럼에 같은 문자열을 붙이는 것도 가능하다.

```python
df.columns = [
    'col_' + col for col in df.columns
]
```

결과는

```text
col_1
col_2
col_3
```

형태가 된다.

---

# 8. iris 데이터셋으로 분석해보기

이번에는 seaborn에서 제공하는 `iris` 데이터셋을 이용해서 실제 데이터 분석을 해봤다.

```python
import pandas as pd
import seaborn as sns

iris = sns.load_dataset('iris')
```

iris 데이터의 target은 `species`이다.

먼저 데이터를 확인한다.

```python
iris.head()
```

앞에서 5개를 확인하고,

```python
iris.tail()
```

뒤에서 5개를 확인할 수 있다.

---

## 데이터 정보 확인

```python
iris.info()
```

`info()`를 이용하면

```text
전체 데이터 개수
컬럼 개수
Non-Null Count
데이터 타입
메모리 사용량
```

등을 확인할 수 있다.

여기서

```text
전체 데이터 수 - Non-Null Count
```

를 계산하면 해당 컬럼의 결측치 개수를 확인할 수 있다.

---

<br>

#### target 분석

데이터 분석을 시작할 때 먼저 **target**을 확인했다.

수치형 데이터와 문자형 데이터는 확인해야 할 통계값이 다르다.

```text
수치형 → mean, min, max, median, count
문자형 → 최빈값, 종류, 개수
```

iris의 target은 문자열인 `species`이다.

```python
iris['species'].mode()
```

`mode()`는 최빈값을 구한다.

```python
iris['species'].value_counts()
```

각 클래스별 데이터 개수를 확인할 수 있다.

```text
setosa        50
versicolor    50
virginica     50
```

고유한 클래스 이름만 확인하려면

```python
iris['species'].unique()
```

클래스 개수를 확인하려면

```python
iris['species'].nunique()
```

를 사용한다.

---

<br>

#### 조건을 이용한 데이터 추출

`sepal_length`가 5보다 작은 데이터만 가져오려면

```python
cond = iris['sepal_length'] < 5

iris[cond]
```

처럼 조건을 만든다.

---

<br>

여러 조건 사용

setosa이면서 `sepal_width`가 3.0인 데이터만 가져와보자.

```python
cond1 = iris['species'] == 'setosa'
cond2 = iris['sepal_width'] == 3.0

iris[cond1 & cond2]
```

여러 조건을 동시에 만족해야 하는 경우 `&`를 사용할 수 있다.

---
<br>

#### isin()

특정 값 여러 개 중 하나에 해당하는지 확인할 때 `isin()`을 사용할 수 있다.

예를 들어 `sepal_width`가 `3.5` 또는 `3.2`이고 species가 `setosa`인 데이터만 가져오려면

```python
cond = (
    iris['sepal_width'].isin([3.5, 3.2])
) & (
    iris['species'] == 'setosa'
)

iris[cond]
```

처럼 작성할 수 있다.

`isin()`을 사용하면

```python
iris['sepal_width'] == 3.5
```

처럼 하나씩 조건을 작성하지 않고 여러 값을 한 번에 확인할 수 있다.

---

<br>

#### iloc과 컬럼 선택

행과 열의 위치를 이용해서 데이터를 가져오려면 `iloc`을 사용할 수 있다.

```python
iris.iloc[1:4, 1:3]
```

```text
   sepal_width  petal_length
1          3.0           1.4
2          3.2           1.3
3          3.1           1.5
```

특정 컬럼만 선택할 수도 있다.

```python
iris[['sepal_length', 'sepal_width']].head()
```

---

<br>

#### groupby()

각 그룹의 통계 데이터를 비교하고 싶을 때 `groupby()`를 사용할 수 있다.

예를 들어 꽃 종류별 `sepal_length` 평균을 구하면

```python
iris.groupby(['species'])['sepal_length'].mean()
```

```text
species
setosa        5.006
versicolor    5.936
virginica     6.588
```

이렇게 각각의 species별 평균을 한 번에 확인할 수 있다.

---

## 여러 통계값 계산하기

`agg()`를 이용하면 여러 통계 함수를 동시에 적용할 수 있다.

```python
iris.groupby(['species'])['sepal_length'].agg([
    'mean',
    'max'
])
```

```text
            mean  max
species
setosa     5.006  5.8
versicolor 5.936  7.0
virginica  6.588  7.9
```

여러 column을 동시에 분석하는 것도 가능하다.

```python
iris.groupby(['species'])[
    ['sepal_length', 'sepal_width']
].agg(['mean', 'max'])
```

즉,

> 각각의 그룹에 대한 통계 데이터를 비교하고 싶을 때 `groupby()`를 사용한다.

---

# 9. map()

이번에는 Titanic 데이터셋을 이용해 `map()`을 실습했다.

```python
import pandas as pd
import seaborn as sns

df = sns.load_dataset('titanic')
```

Titanic 데이터의 target은 `survived`이다.

```python
df['survived'].mean()
```

```text
0.383838...
```

`survived`는

```text
0 → 사망
1 → 생존
```

이므로 평균을 계산하면 전체 생존률을 구할 수 있다.

---

## map을 이용한 데이터 변환

`map()`은 **Series의 각각의 값을 다른 값으로 변환**할 때 사용할 수 있다.

예를 들어

```text
male   → 0
female → 1
```

로 변경해보자.

```python
dict_sex = {
    "male": 0,
    "female": 1
}

df['sex'].map(dict_sex)
```

함수를 직접 만들어서 적용하는 것도 가능하다.

```python
def modify_sex(gender):
    result = 1

    if gender == 'male':
        result = 0

    return result

df['sex'].map(modify_sex)
```

`map()`을 실행하면 Series에 들어있는 값이 하나씩 함수의 매개변수로 전달된다.

```text
male
 ↓
modify_sex('male')
 ↓
0
```

---

<br>

#### 성별 생존률 분석

성별에 따라 생존률이 어떻게 다른지 확인해봤다.

```python
df.groupby(['sex'])['survived'].mean()
```

```text
sex
female    0.742038
male      0.188908
```

Titanic 데이터에서는 여성의 생존률이 남성보다 높게 나타난다.

---


<br>

#### 나이를 이용한 분석

먼저 나이 데이터의 통계값을 확인했다.

```python
df['age'].describe()
```

```text
count    714.000000
mean      29.699118
std       14.526497
min        0.420000
25%       20.125000
50%       28.000000
75%       38.000000
max       80.000000
```

평균 나이를 기준으로 새로운 변수를 만들어봤다.

```python
df['is_adult'] = df['age'] > df['age'].mean()
```

그리고 그룹별 생존률을 확인한다.

```python
df.groupby(['is_adult'])['survived'].mean()
```

```text
is_adult
False    0.370766
True     0.406061
```

---

<br>

#### 객실 등급별 생존률

객실 등급인 `pclass`에 따라서도 생존률을 비교할 수 있다.

```python
df.groupby(['pclass'])['survived'].mean()
```

```text
pclass
1    0.629630
2    0.472826
3    0.242363
```

1등급 객실의 생존률이 가장 높고 3등급으로 갈수록 낮아지는 것을 확인할 수 있다.

---

## 객실 등급 + 성별

groupby에는 여러 개의 기준을 넣을 수도 있다.

```python
df.groupby([
    'pclass',
    'sex'
])['survived'].mean()
```

```text
pclass  sex
1       female    0.968085
        male      0.368852
2       female    0.921053
        male      0.157407
3       female    0.500000
        male      0.135447
```

이렇게 하면 단순히 성별만 비교하는 것이 아니라

```text
객실 등급
   ↓
성별
   ↓
생존률
```

처럼 두 개 이상의 조건으로 데이터를 그룹화할 수 있다.

---

# 10. apply()

`map()`과 `apply()`의 차이도 확인했다.

```text
Series.map()      → Vector에 적용
DataFrame.apply() → Matrix에 적용
```

예를 들어 Titanic 데이터에서 가족 수를 계산하려면 `sibsp`와 `parch` 두 개의 column이 필요하다.

따라서 하나의 Series만 사용하는 것이 아니라 DataFrame의 row 전체를 함수로 전달해야 한다.

```python
def family_cnt(row: dict) -> int:
    return row['sibsp'] + row['parch']
```

```python
df.apply(
    family_cnt,
    axis=1
)
```

`axis=1`을 사용하면 DataFrame의 각 row가 함수로 전달된다.

```python
df['family_cnt'] = df.apply(
    family_cnt,
    axis=1
)
```

---

## 기존 데이터 검증

새롭게 만든 `family_cnt`를 이용해서 기존 `alone` 컬럼이 제대로 만들어져 있는지도 확인해봤다.

```python
df['family_cnt'].map(
    lambda v: False if v else True
)
```

그리고 기존 `alone`과 비교한다.

```python
sum(
    df['alone'] !=
    df['family_cnt'].map(
        lambda v: False if v else True
    )
)
```

결과가 `0`이라면 두 데이터가 모두 동일하다는 뜻이므로 기존 `alone` 컬럼이 정상적으로 만들어져 있다는 것을 확인할 수 있다.

---

# 11. 문제 - 10대, 20대, 30대 생존률 구하기

마지막으로 `map()`과 `groupby()`를 이용해서 Titanic 승객 중 **10대, 20대, 30대의 생존률**을 구해봤다.

처음에는 나이에 직접 조건을 걸려고 했다.

```python
# 10대 20대 30대 생존률 구하기
# isin map groupby

# df['new'] = 10 <= df['age'] < 40
```

하지만 Series 전체에 일반적인 Python 비교 연산을 그대로 적용할 수 없기 때문에 `map()`을 이용해서 각 나이를 연령대로 변환했다.

```python
def age_line(age):
    result = 0

    if 10 <= age < 20:
        result = 10
    elif 20 <= age < 30:
        result = 20
    elif 30 <= age < 40:
        result = 30
    else:
        result = 0

    return result
```

그리고 `age` 컬럼에 함수를 적용한다.

```python
df['cond'] = df['age'].map(age_line)
```

이렇게 하면 나이에 따라서

```text
10 ~ 19세 → 10
20 ~ 29세 → 20
30 ~ 39세 → 30
그 외      → 0
```

으로 분류된다.

이제 `groupby()`를 이용해서 연령대별 생존률을 계산한다.

```python
df.groupby(['cond'])['survived'].mean()
```

```text
cond
0     0.375622
10    0.401961
20    0.350000
30    0.437126
Name: survived, dtype: float64
```

여기서 문제는 `0`이 같이 나온다는 것.

우리가 보고 싶은 것은

```text
10대
20대
30대
```

뿐이다.

이것저것 해보다가 결국 강사님께 질문했는데...

**시리즈라서 슬라이싱 하면 됐다..................**
나 진짜 바보인가..............

```python
df.groupby(['cond'])['survived'].mean()[1:]
```

```text
cond
10    0.401961
20    0.350000
30    0.437126
Name: survived, dtype: float64
```

끝 😇

결과적으로 Titanic 데이터에서

```text
10대 생존률 → 약 40.2%
20대 생존률 → 약 35.0%
30대 생존률 → 약 43.7%
```

로 확인됐다.

오늘 배운 `map()`과 `groupby()`를 같이 사용하면 단순히 데이터를 조회하는 것을 넘어, **기존 데이터를 원하는 기준으로 새롭게 분류하고 그룹별 통계까지 계산할 수 있다는 점**을 확인할 수 있었다.

