---
type: source
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY15-2026.08.31"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY18 (2026.08.31)"
source_id: 3acc9a69-30e2-4de1-ba02-616b450b47a0
source_author: doldolkoong
source_published: 2026-09-01
source_updated: 2026-09-01
archived: 2026-09-08
tags:
  - velog-source
---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY18 (2026.08.31)

[Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY15-2026.08.31) · [[DAY18 - Matplotlib과 Seaborn 시각화|DAY18 - Matplotlib과 Seaborn 시각화]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY18 (2026.08.31)

**DAY 15**

> 📖 오늘 학습 내용
> 1. SSH 설정
> 2. 데이터 시각화를 해야 하는 이유 (앤스콤 4분할 그래프)
> 3. `.info()`, `.unique()`, `.nunique()`
> 4. Matplotlib 기본 구조 (Figure, Axes)
> 5. 선 그래프(Line Plot)
> 6. 막대그래프(Bar Plot)
> 7. 산점도(Scatter Plot)
> 8. Seaborn (Relational / Distribution / Categorical Plot)
> 9. Box Plot 구조와 이상치
> 10. Sweetviz (Automated EDA)

---

**1. SSH 설정**

SSH는 Secure Shell의 약자로, 네트워크를 통해 다른 컴퓨터나 서버에 안전하게 접속하기 위한 프로토콜이다. GitHub에서는 SSH Key를 등록하면 매번 아이디나 비밀번호를 입력하지 않고도 Git 저장소와 통신할 수 있다.

```text
내 컴퓨터 → Private Key → SSH 인증 → GitHub에 등록된 Public Key 확인 → 인증 성공
```

`git clone git@github.com:username/repository.git`, `git pull`, `git push` 같은 명령어를 사용할 때 인증에 쓰인다.

SSH Key는 두 종류로 구성된다.

- Private Key: 내 컴퓨터에 보관, 절대로 외부에 공개하면 안 됨
- Public Key: GitHub 등에 등록, 공개되어도 괜찮음

*자세한 부분은 따로 올릴 거임

---

**2. 데이터 시각화를 해야 하는 이유**

데이터 분석에서는 평균, 분산, 표준편차, 상관계수 같은 **통계량만 확인하면 데이터의 실제 모습을 놓칠 수 있다.** 이를 보여주는 대표적인 예가 **앤스콤 4분할 그래프(Anscombe's Quartet)**다.

앤스콤 데이터는 4개의 데이터셋으로 구성되어 있는데, 각 데이터셋의 평균, 분산, 표준편차, 상관계수, 선형 회귀선 등 통계적 특성이 거의 동일하다. 하지만 실제 데이터를 그래프로 그려 보면 완전히 다른 모양을 가지고 있다.

> 통계량이 같다고 해서 데이터의 분포와 형태까지 같은 것은 아니다. 따라서 데이터 분석에서는 **통계량 + 시각화**를 함께 확인해야 한다.

Seaborn에서 앤스콤 데이터를 불러와 확인할 수 있다.

```python
import seaborn as sns

Anscombe = sns.load_dataset('anscombe')
Anscombe.info()
```

그룹별 통계량을 확인하면:

```python
Anscombe.groupby(['dataset'])[['x', 'y']].agg(['mean', 'std', 'var'])
```

`groupby(['dataset'])`로 `dataset`(I, II, III, IV 4개) 기준 그룹화하고, `[['x', 'y']]`로 x, y 컬럼만 선택한 뒤 `.agg(['mean', 'std', 'var'])`로 각 데이터셋의 평균/표준편차/분산을 계산한다. 이 값들이 거의 동일해도 실제 분포는 완전히 다르기 때문에, 데이터 분석의 기본 흐름은 다음과 같이 정리할 수 있다.

```text
데이터 불러오기 → 데이터 구조 확인 → 기초 통계 확인 → 데이터 시각화
→ 이상치/분포/관계 확인 → 데이터 전처리 → 분석 또는 모델링
```

---

**3. `.info()`에서 봐야 하는 정보**

`df.info()`는 EDA를 시작할 때 가장 먼저 사용하는 함수 중 하나로, 데이터프레임의 전체적인 구조를 확인할 때 사용한다.

1. **학습 데이터 수 확인**: `RangeIndex: 891 entries, 0 to 890`이면 총 891개의 Row가 있다는 뜻이다.
2. **컬럼 개수 확인**: `Data columns (total 15 columns)`이면 15개의 변수가 존재한다. 머신러닝에서는 Target(예측하고 싶은 값)과 Feature(Target을 예측하기 위해 사용하는 값)로 나누는데, 모든 컬럼을 무조건 Feature로 쓰는 건 아니고 중복/불필요/데이터 누수를 유발하는 변수는 제거할 수 있다.
3. **결측치 확인**: 전체 891개 중 `age`가 714 non-null이면 891 - 714 = 177개의 결측치가 존재한다.
4. **데이터 타입 확인**: `int64`, `float64`, `object/str`, `category`, `bool` 등을 확인할 수 있다. 단, 타입만 보고 수치형/범주형을 결정하면 안 된다. `pclass = 1, 2, 3`은 `int64`지만 실제 의미는 1등석/2등석/3등석이므로 범주형으로 해석할 수 있다.
5. **Memory Usage 확인**: `memory usage: 80.7 KB`처럼 DataFrame이 메모리를 얼마나 사용하는지 확인할 수 있다. 데이터가 매우 크면 데이터 타입 변경, 불필요한 컬럼 삭제, category 타입 사용 등으로 메모리 사용량을 줄일 수 있다.

---

**4. `.unique()`와 `.nunique()`**

`df['컬럼명'].unique()`는 해당 컬럼에 어떤 고유한 값들이 존재하는지 확인한다.

```python
df['sex'].unique()
```
> ['male', 'female']

범주형 데이터를 분석할 때 어떤 범주가 있는지, 오타가 있는지, 이상한 값이 들어가 있는지 확인할 수 있다. 예를 들어 지역 데이터가 "서울", "부산", "인천", "seoul", "서울시"처럼 들어있다면 같은 지역인데 표현이 다를 가능성이 있다.

`.unique()`는 문자열 데이터에서만 쓰는 건 아니고 숫자형 데이터에서도 사용할 수 있다.

```python
df['pclass'].unique()
```
> [3, 1, 2]

고유값 자체가 아니라 **고유값의 개수만** 확인하고 싶다면 `.nunique()`를 사용한다.

```python
df['sex'].nunique()
```
> 2

즉 `unique()`는 값 확인, `nunique()`는 값의 종류 개수 확인이다.

---

**5. Matplotlib 기본 구조**

Matplotlib은 Python에서 가장 기본적으로 사용하는 데이터 시각화 라이브러리다.

```python
import matplotlib.pyplot as plt
```

`koreanize_matplotlib`은 Matplotlib에서 한글 폰트 깨짐 문제를 편리하게 해결해주는 라이브러리로, import만 해도 한글 폰트 설정을 자동으로 적용해준다.

```python
import koreanize_matplotlib
```

Seaborn은 Matplotlib을 기반으로 만들어진 시각화 라이브러리로, Matplotlib보다 비교적 간단한 코드로 통계적인 그래프를 만들 수 있다.

```python
import seaborn as sns
```

그래프를 그리는 과정은 그림 그리는 것과 비슷하게 생각할 수 있다.

```text
Figure → 도화지
Axes → 도화지 안의 실제 그래프 영역
plot → 그래프를 그림
show → 화면에 출력
```

```python
plt.figure()
```
> `<Figure size 640x480 with 0 Axes>`
![](https://velog.velcdn.com/images/doldolkoong/post/8619bfcf-7c78-4d21-b305-109c31feeae4/image.png)


`Figure`는 전체 도화지를 의미하며, 아직 그래프를 그리지 않았기 때문에 `0 Axes`로 표시된다. `plt.axes()`는 그래프를 그릴 좌표평면을 만든다.

```text
Figure
└── Axes
    └── 실제 그래프
```

`plt.show()`는 지금까지 만든 그래프를 화면에 출력한다.

---

**6. 선 그래프(Line Plot)**

```python
import numpy as np

np.arange(2, 7)
```
> array([2, 3, 4, 5, 6])

`arange(start, stop)`은 지정한 범위의 숫자를 생성하며, `stop`은 포함되지 않는다.

```python
plt.plot(np.arange(2,7))
plt.show()
```

![](https://velog.velcdn.com/images/doldolkoong/post/ce585c4d-e036-4477-bfa8-5036722cf71b/image.png)

`y` 값만 넣으면 Matplotlib이 자동으로 `x` 값을 만든다. 즉 `plt.plot([2, 3, 4, 5, 6])`은 내부적으로 `x = [0, 1, 2, 3, 4]`, `y = [2, 3, 4, 5, 6]`처럼 사용된다.

**하나의 그래프에 여러 선 그리기**: 하나의 Axes에 `plot()`을 여러 번 사용하면 여러 개의 선을 같이 그릴 수 있다.

```python
plt.plot(np.arange(2,7))
plt.plot(np.arange(5))
plt.show()
```

![](https://velog.velcdn.com/images/doldolkoong/post/cc733f79-3957-4161-80dc-b9607a84cef5/image.png)

**Figure 크기 변경**: `figsize=(15,5)`는 도화지 크기를 조절한다 (15=가로, 5=세로, 단위 inch).

```python
plt.figure(figsize=(15,5))
plt.plot(np.arange(2,7))
plt.plot(np.arange(5))
plt.show()
```
![](https://velog.velcdn.com/images/doldolkoong/post/975815c8-4397-4309-8033-e7e1f394efc8/image.png)


**subplots()**로 하나의 도화지에 여러 그래프를 배치할 수 있다.

```python
fig, ax = plt.subplots(2, 2, figsize=(15,5))
```

![](https://velog.velcdn.com/images/doldolkoong/post/84c9ce10-1017-462d-8a53-7b628a75295b/image.png)



2 Row, 2 Column이므로 총 4개의 그래프 영역이 생긴다. `fig`는 전체 도화지, `ax`는 각각의 그래프 영역을 의미한다.

```python
ax[0,0].plot(np.arange(5))          # 왼쪽 위
ax[0,1].plot(np.arange(5))          # 오른쪽 위, plot 두 번 → 선 두 개
ax[0,1].plot(np.arange(2,7))

x = range(0,10)
y = np.exp(x)                        # 지수함수 eˣ
ax[1,0].plot(x,y)

x = range(1, 1000)
y = np.log1p(x)                      # 로그함수 log(1+x)
ax[1,1].plot(x,y)

plt.show()

```

![](https://velog.velcdn.com/images/doldolkoong/post/f7b07fd3-17dd-430c-9e3d-7fc58b08d05b/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/0106bd70-625c-4d1b-8365-bd256cd5a8de/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/beac0db3-8c7b-4b5c-af12-4eafd3c5c608/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/04dc2ddf-4cf2-4c32-b763-ca226ec7dd53/image.png)


**로그를 사용하는 이유**: 로그는 값의 범위가 매우 큰 데이터를 압축할 때 유용하다. 예를 들어 10, 100, 1,000, 10,000, 1,000,000처럼 값의 차이가 매우 큰 경우 로그를 적용하면 범위가 줄어든다. 로그의 중요한 성질은 `log(a × b) = log(a) + log(b)`, 즉 **곱셈을 덧셈 형태로 바꿀 수 있다**는 것이다 (반대로 `log(a+b)`가 `log(a)×log(b)`가 되는 건 아니다).

데이터 분석에서 로그 변환을 사용하는 이유:
1. 값의 범위 축소
2. 큰 값의 영향 감소
3. 심하게 오른쪽으로 치우친 데이터 완화
4. 이상치 영향 일부 감소
5. 지수적인 관계를 비교적 선형적인 관계로 변경

연봉, 매출, 집값처럼 일부 큰 값 때문에 오른쪽 꼬리가 길어지는 데이터에 로그 변환을 활용할 수 있다.

**제목 설정**: `fig.suptitle()`은 Figure 전체의 제목, `ax.set_title()`은 개별 그래프의 제목을 설정한다.

```python
fig.suptitle("도화지 제목")
ax[0,1].set_title("그래프 제목")
```
![](https://velog.velcdn.com/images/doldolkoong/post/c3379388-a24a-484f-997a-7f891da8fb43/image.png)


![](https://velog.velcdn.com/images/doldolkoong/post/187450cf-034c-4a57-aa04-fb336076ce5f/image.png)

---

**7. 막대그래프(Bar Plot)**

```python
plt.bar()
```

막대그래프는 일반적으로 **범주별 수치 값을 비교**할 때 사용한다. 연도별 매출, 지역별 인구, 성별 평균 점수, 상품별 판매량 등을 표현할 수 있다. 일반적으로 X축은 범주형 데이터, Y축은 수치형 데이터를 사용한다.

```python
x = np.arange(3)
x_names = ['2020', '2021', '2022']
y = [100, 400, 800]

plt.bar(x,y)
plt.xticks(x, x_names)
plt.show()
```
![](https://velog.velcdn.com/images/doldolkoong/post/cdc3e1f3-3f60-4cc5-847c-ef832caed0f7/image.png)

실제 x 데이터는 0, 1, 2지만 `plt.xticks(x, x_names)`로 화면에는 2020, 2021, 2022로 표시할 수 있다.

**막대 색 지정**:

```python
colors = ['red', 'green', 'blue']
plt.bar(x, y, color=colors)
```

![](https://velog.velcdn.com/images/doldolkoong/post/2635b13a-d9e9-44af-8260-2bc2e4350670/image.png)


막대그래프는 범주끼리 비교하는 것이 핵심이다.

---

**8. 산점도(Scatter Plot)**

산점도는 **두 개의 수치형 변수 사이의 관계를 확인**할 때 사용한다. 키↔몸무게, 광고비↔매출, 공부시간↔시험점수, 총 결제금액↔팁 같은 관계를 확인할 수 있다.

```python
num = 50
x = np.random.randn(num)
y = np.random.randn(num)

plt.scatter(x,y)
plt.show()
```

![](https://velog.velcdn.com/images/doldolkoong/post/278b326e-d9ac-4351-a2ae-5e5a648deb43/image.png)

`np.random.randn()`은 표준정규분포를 따르는 랜덤한 값을 생성한다. 산점도로는 양의 관계, 음의 관계, 관계 없음, 곡선 관계, 군집, 이상치 등을 눈으로 확인할 수 있다.

**점 크기·색·투명도 조절**:

```python
area = (30 * np.random.rand(num)) ** 2
color = np.random.rand(num)

plt.scatter(x, y, s=area, c=color, alpha=0.5, cmap='cool')
plt.colorbar()
plt.show()
```


![](https://velog.velcdn.com/images/doldolkoong/post/099436e1-cf01-45f5-a4a7-a7108f1e6009/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/541ee46d-1291-4c02-9c86-cb89e50af14c/image.png)


- `s=area`: 점 크기 조절 (size)
- `c=color`: 숫자값에 따라 점 색상 지정
- `alpha=0.5`: 투명도 설정 (0=완전 투명, 1=완전 불투명). 점들이 많이 겹치는 산점도에서 데이터가 몰려 있는 영역을 확인하기 쉬워짐
- `cmap='cool'`: 숫자값에 따른 색상 범위(Colormap) 설정
- `plt.colorbar()`: 색상↔숫자값 관계를 보여주는 색상 막대 표시

---

**9. Seaborn**

Seaborn 그래프는 크게 세 가지로 분류할 수 있다.

- Relational Plot: 변수 사이의 관계 (scatter, line)
- Distribution Plot: 데이터의 분포 (histogram, KDE, ECDF)
- Categorical Plot: 범주형 데이터의 분포 또는 범주형↔수치형 관계 (strip, swarm, box, violin, bar, count, point)

```python
sns.set_theme(style="darkgrid")
```

`set_theme()`으로 Seaborn 그래프의 기본 스타일을 지정할 수 있다.

**Relational Plot — Tips 데이터**:

```python
tips = sns.load_dataset("tips")
tips.info()
```

`total_bill`(총 결제금액), `tip`(팁), `sex`(성별), `smoker`(흡연 여부), `day`(요일), `time`(식사 시간), `size`(인원 수) 컬럼으로 구성되어 있다.

```python
sns.relplot(data=tips, x='total_bill', y='tip', kind='scatter',
            hue='smoker', style='time', size='size', sizes=(15,200), alpha=0.5)
```

![](https://velog.velcdn.com/images/doldolkoong/post/208c9a34-f9a9-42ce-b31a-afcbde21007f/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/14a96161-e3c6-43eb-a051-e3f72f29b9a6/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/9aac6b08-553b-4633-8230-cfcdf9ea17af/image.png)![](https://velog.velcdn.com/images/doldolkoong/post/3a103c0e-e711-4172-bebe-37468e62b635/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/f8e69bd5-bdb7-4898-b059-c30ac9bdccb5/image.png)



- `hue='smoker'`: 흡연 여부에 따라 색을 다르게 표시 (범주형 변수를 색으로 구분)
- `style='time'`: 범주에 따라 점의 모양을 다르게 표시 (○, X 등)
- `size='size'`, `sizes=(15,200)`: `size` 컬럼값에 따라 점 크기를 다르게, 점의 최소/최대 크기 설정
- `alpha=0.5`: 투명도 설정

즉 hue=색, style=모양으로 이해하면 되고, 하나의 그래프에서 X 위치, Y 위치, 색, 모양, 크기 등 여러 정보를 동시에 표현할 수 있다.

**Line Plot — FMRI 데이터**:

```python
fmri = sns.load_dataset("fmri")
sns.relplot(data=fmri, x="timepoint", y='signal', kind='line', hue='event', style='region')
```

시간(`timepoint`)에 따른 신호(`signal`) 변화를 확인하며, `hue='event'`(색), `style='region'`(선 스타일)로 구분한다.

```python
sns.relplot(data=fmri, x="timepoint", y='signal', kind='line', row='event', col='region')
```
![](https://velog.velcdn.com/images/doldolkoong/post/2c9098ca-e078-45cc-a80d-2f09c30c0d53/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/090587bc-4487-4fb1-81ab-c23841b574a2/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/ba5f8b7e-1856-467a-913c-91dc09d7b746/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/7b752e70-9434-4814-8007-d092870c83fc/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/d84c210b-bafd-43e3-adda-b5898402e5e2/image.png)



`col`은 가로 방향, `row`는 세로 방향으로 그래프를 분리한다. 범주별 관계를 여러 그래프로 비교할 때 유용하다.

**Distribution Plot — Penguins 데이터**:

```python
penguins = sns.load_dataset("penguins")

sns.displot(data=penguins, x='flipper_length_mm', bins=20)
```

`bins=20`은 전체 범위를 20개 구간으로 나눠 Histogram을 그린다.

막대그래프와 히스토그램의 차이: Bar Plot은 X축이 범주형, Y축이 집계된 수치인 반면(예: 서울 100, 부산 80), Histogram은 X축이 연속형 수치, Y축이 해당 구간에 포함된 데이터 개수다(예: 170~175cm → 30명). 그래서 Histogram은 막대가 붙어 있고, Bar Plot은 서로 다른 범주라 막대가 떨어져 있다.

```python
sns.displot(data=penguins, x='flipper_length_mm', hue='species', multiple='stack')
sns.displot(data=penguins, x='flipper_length_mm', hue='species', multiple='dodge')
sns.displot(data=penguins, x='flipper_length_mm', col='species')
```

- `multiple='stack'`: 각 범주의 Histogram을 겹치지 않고 위로 쌓아서 표현
- `multiple='dodge'`: 각 범주의 막대를 옆으로 나란히 배치
- `col='species'`: 종별로 Histogram을 각각 분리해서 표시

```python
sns.displot(data=penguins, x='flipper_length_mm', kind='kde')
```

KDE(Kernel Density Estimation)는 Histogram의 분포를 부드러운 곡선으로 표현하는 방식이다. KDE의 Y축은 단순한 개수가 아니라 **확률밀도(Probability Density)**를 나타내기 때문에 Y값을 바로 확률로 해석하면 안 되고, 곡선 아래 전체 면적이 1이 되도록 정규화된 밀도로 이해해야 한다.

```python
sns.displot(data=penguins, x='bill_length_mm', y='bill_depth_mm')
sns.displot(data=penguins, x='bill_length_mm', y='bill_depth_mm', kind='kde')
```
![](https://velog.velcdn.com/images/doldolkoong/post/90d8b6cf-d280-4911-84a6-7a71082202db/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/7c675a74-cd47-4e88-a442-b34288ae3d2c/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/54c8baed-8fdd-490b-8279-6980dec7fa5b/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/214bb50c-c433-49b0-9bf7-5f283fc9e7c7/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/6b1d2f56-9303-47b4-960d-f9249ce95e37/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/4832f4a6-88a7-4919-950d-38f8c7c4d8e5/image.png)


X, Y를 동시에 지정하면 두 수치형 변수의 분포를 2차원 형태로 볼 수 있고, 특정 영역에 데이터가 얼마나 몰려 있는지 확인할 수 있다.

**Categorical Plot — Tips 데이터**:

```python
sns.catplot(data=tips, x='day', y='tip')
```

`catplot()`의 기본 `kind`는 `strip`이다. 요일별(day, 범주형) tip(수치형)의 분포를 확인할 수 있다.

```python
sns.catplot(data=tips, x='day', y='tip', kind='swarm')
```

Swarm Plot은 각 데이터 점이 서로 겹치지 않도록 옆으로 배치해서, 범주별 데이터가 어디에 많이 몰려 있는지 보기 편하다. 다만 데이터 수가 매우 많으면 점이 많아져 보기 어려울 수 있다.

```python
sns.catplot(data=tips, x='day', y='total_bill', kind='box')
```
![](https://velog.velcdn.com/images/doldolkoong/post/731ce1c0-6759-4f5d-9830-a9c132a88772/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/685dfc6c-d51e-4517-8e5d-ea6fc1ab420c/image.png)


Box Plot은 데이터의 분포와 이상치를 확인하는 데 매우 많이 사용된다.

---

**10. Box Plot 구조**

```text
      이상치
        ●
        |
     ───────     ← 위쪽 수염
        |
    ┌───────┐
    │       │
    │-------│     ← 중앙값 Median
    │       │
    └───────┘
        |
     ───────     ← 아래쪽 수염
        |
        ●
      이상치
```

박스는 일반적으로 25%~75% 구간을 나타낸다 (Q1=25%, Q2=50%=Median, Q3=75%). 박스 안의 선은 중앙값(Median)으로 50% 지점을 의미한다.

**IQR(Interquartile Range)**은 `Q3 - Q1`, 즉 75% 지점에서 25% 지점을 뺀 값으로 데이터의 중앙 50%가 분포하는 범위를 나타낸다.

Box Plot에서는 일반적으로 `Q1 - 1.5 × IQR` ~ `Q3 + 1.5 × IQR` 범위를 벗어나는 데이터를 이상치 후보로 표시한다. 단, 수염 밖에 있다고 무조건 잘못된 데이터인 건 아니다. Box Plot에서 표시되는 이상치는 통계적으로 다른 데이터들과 멀리 떨어져 있는 관측값 후보일 뿐이며, 실제로 삭제할지는 데이터의 의미를 확인한 뒤 결정해야 한다.

Box Plot을 이용하면 한 번에 중앙값, 분포, 사분위수, IQR, 이상치 후보를 확인할 수 있어서 EDA에서 매우 많이 사용한다.
![](https://velog.velcdn.com/images/doldolkoong/post/39ebce55-cdc8-4261-84ae-4f2735ac0b27/image.png)


---

**11. Sweetviz (Automated EDA)**

```python
import sweetviz as sv
import seaborn as sns

df = sns.load_dataset('titanic')
df = df[['survived', 'pclass', 'sex', 'age', 'sibsp', 'parch', 'fare', 'embarked']]
```

분석에 사용할 컬럼만 선택한 뒤 `FeatureConfig`로 세부 설정을 지정할 수 있다.

```python
feature_config = sv.FeatureConfig(
    skip="fare",
    force_cat=['survived']
)
```

- `skip="fare"`: `fare` 컬럼을 분석에서 제외
- `force_cat=['survived']`: `survived`는 실제 타입은 숫자(0/1)지만 의미상 범주형(사망/생존)이므로, Sweetviz가 수치형으로 해석하지 않도록 강제로 범주형 지정

```python
report = sv.analyze(source=df, feat_cfg=feature_config)
report.show_notebook()
```

Sweetviz가 DataFrame을 자동으로 분석해서 데이터 타입, 분포, 결측치, 최솟값/최댓값, 평균, 범주 개수, Feature 관계, 상관관계 등을 시각적인 Report로 보여주고, `show_notebook()`으로 Jupyter Notebook에서 결과를 확인할 수 있다.

Sweetviz는 정확히는 AutoML 도구라기보다 **Automated EDA 도구**에 가깝다. AutoML(Automated Machine Learning)은 데이터 전처리, Feature 선택, 모델 선택, Hyperparameter 탐색, 모델 학습/평가 등을 자동화하는 것을 말하는데, Sweetviz는 그중에서도 모델링 전 EDA를 자동화하는 도구라고 이해하면 된다.

![](https://velog.velcdn.com/images/doldolkoong/post/0f5c5848-b8b6-422d-b780-716f0817f738/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/7dac2bd3-4ff8-48ec-b9f0-04b375991fd7/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/f0852770-b5c3-4244-b041-4b6cb7f52031/image.png)



---

**핵심 정리**

**1. 데이터는 통계만 보면 안 된다.** 앤스콤 4분할 데이터처럼 평균, 분산, 표준편차, 상관계수, 회귀선이 같더라도 실제 데이터 모양은 완전히 다를 수 있다. 통계량 + 시각화를 반드시 같이 확인해야 한다.

**2. `.info()`에서 확인할 것**: 전체 데이터 수, 컬럼 수, Non-Null 개수, 결측치, 데이터 타입, Memory Usage.

**3. 그래프 선택 기준**:

```text
두 수치형 변수 관계? → Scatter Plot
시간에 따른 변화? → Line Plot
범주별 값 비교? → Bar Plot
수치형 데이터 분포? → Histogram / KDE
범주별 수치형 데이터 분포? → Box Plot / Swarm Plot
```

**Matplotlib 구조**: Figure(전체 도화지) → Axes(실제 그래프가 들어가는 좌표 영역) → Graph

**Seaborn 구조**: Relational Plot(scatter, line) / Distribution Plot(hist, kde) / Categorical Plot(strip, swarm, box, violin, bar, count)

데이터 시각화의 목적은 예쁜 그래프를 만드는 것이 아니라 **숫자만으로는 발견하기 어려운 데이터의 특징과 문제점을 찾는 것**이다. 그래프를 통해 분포, 추세, 상관관계, 이상치, 군집, 범주별 차이 등을 확인하고, 이후 전처리 / Feature Engineering / 통계 분석 / 머신러닝 방향을 결정할 수 있다. 결국 EDA는 데이터 확인 → 통계량 확인 → 시각화 → 해석까지가 한 세트라고 볼 수 있다.
