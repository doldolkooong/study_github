---
type: source
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%84%EC%B2%98%EB%A6%AC"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] 1st 프로젝트 - 데이터 전처리"
source_id: ce96d845-fd04-4ee6-b576-7acd38330002
source_author: doldolkoong
source_published: 2026-08-26
source_updated: 2026-09-01
archived: 2026-09-08
tags:
  - velog-source
---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] 1st 프로젝트 - 데이터 전처리

[Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%84%EC%B2%98%EB%A6%AC) · [[SAFE - 데이터 전처리|SAFE - 데이터 전처리]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

[플레이데이터 SK네트웍스 Family AI 캠프 36기] 1st 프로젝트 - 데이터 전처리

# 1st 프로젝트 - 데이터 전처리

> **📖 오늘 정리 내용**
> 1. 데이터 전처리 방향
> 2. 인구 데이터 전처리
> 3. 자동차·운전면허 데이터 전처리
> 4. 교통사고 데이터 전처리
> 5. 정책 데이터 전처리
> 6. FAQ 데이터 전처리
> 7. 전처리 결과 및 느낀 점

<br>

이전 단계에서 SAFE 서비스에 필요한 데이터를 **인구 / 자동차 / 교통사고 / 교통법규·정책 / FAQ** 5개 카테고리로 정의했다. 이번엔 그 데이터를 실제로 열어보고 DB에 적재할 수 있는 형태로 다듬는 작업을 진행했다.

출처가 행정안전부, KOSIS, 경찰청, 국토교통통계누리, TAAS 등으로 다양하다 보니 파일 형식은 물론 컬럼 구조와 데이터 표현 방식까지 파일마다 제각각이었다. 특히 공공데이터 Excel 파일은 사람이 보기에는 편하지만, 바로 DB에 저장하거나 분석하기에는 아래와 같은 문제들이 있었다.

> - 병합 셀로 인해 반복되는 값이 비어 있음
- 여러 행으로 구성된 다중 헤더
- `계`, `합계`, `총계` 데이터가 실제 데이터와 함께 존재
- `1,234`처럼 숫자가 문자열로 저장됨
- 연도·월·시간대가 가로 방향으로 반복됨
- 같은 의미의 컬럼명이 파일마다 다름
- CSV 파일마다 인코딩 방식이 다름

그래서 이번 단계에서는 **pandas로 원본 데이터를 분석·DB 적재에 적합한 형태로 정제하고 표준화하는 작업**에 집중했다.

<br>

**1. 데이터 전처리 방향**

전처리 과정에서 가장 중요하게 생각한 건, 서로 다른 기관에서 가져온 데이터를 이후 하나의 서비스에서 함께 쓸 수 있도록 **구조를 최대한 일관되게 만드는 것**이었다. 전체 흐름은 다음과 같이 잡았다.

```text
원본 Excel / CSV
        ↓
pandas 데이터 로드
        ↓
필요한 행·열 추출
        ↓
병합 셀 / 결측값 처리
        ↓
합계·소계 등 불필요한 데이터 제거
        ↓
컬럼명 표준화
        ↓
문자열 / 숫자 / 날짜 자료형 변환
        ↓
Wide → Long 구조 변환
        ↓
분석 및 DB 적재용 DataFrame 생성
```

단순히 결측치를 지우는 것보다, **각 데이터가 무엇을 의미하는지 먼저 파악하고 그다음 필요한 값만 남기는 작업**이 훨씬 중요했다.

<br>

**2. 인구 데이터 전처리**

인구 데이터는 **e-나라지표 지역별 인구 데이터**와 **행정안전부 연령별 인구 데이터** 두 가지를 사용했다.

**2-1. 지역별 인구 데이터**

e-나라지표 원본 Excel에는 인구·인구밀도 등이 함께 들어 있었고, 연도별 데이터가 각각 다른 열에 저장되어 있었다. SAFE에서는 지역별 인구 변화와 다른 데이터의 연계가 목적이므로 필요한 지역과 2021~2025년 인구 데이터만 추출했다.

```python
local_people = df.iloc[
    4:,
    [0, 1, 3, 5, 7, 9]
].copy()

local_people.columns = [
    "region",
    "population_2021",
    "population_2022",
    "population_2023",
    "population_2024",
    "population_2025",
]
```

이후 `계`, `총계`, `합계` 같은 집계용 행을 제거하고 지역명을 정리했다. 여기서 가장 중요했던 작업은 **Wide Format을 Long Format으로 변환**하는 것이었다.

```python
local_people = local_people.melt(
    id_vars=["region"],
    var_name="year",
    value_name="population"
)
```

원본 구조가 이랬다면

```text
region | population_2021 | population_2022 | population_2023
서울    | 9500000         | 9400000         | 9300000
```

전처리 후에는 이렇게 바뀐다.

```text
region | year | population
서울    | 2021 | 9500000
서울    | 2022 | 9400000
서울    | 2023 | 9300000
```

이렇게 변환해두면 이후 `region`, `year`를 기준으로 자동차 등록 데이터나 교통사고 데이터와 연계하기 쉬워진다. 실제 코드에서도 `melt()`로 지역별 연도 컬럼을 세로 구조로 바꾸고, 정규표현식으로 연도를 추출한 뒤 인구수를 숫자형으로 변환했다.

**2-2. 연령별 인구 데이터**

행정안전부 데이터에서는 행정구역명이 다음처럼 저장되어 있었다.

```text
서울특별시 (1100000000)
```

분석에는 행정구역 코드가 필요 없어서 정규표현식으로 제거했다.

```python
df["행정구역"] = (
    df["행정구역"]
    .astype(str)
    .str.replace(r"\s*\(\d+\)\s*$", "", regex=True)
    .str.strip()
)
```

또 원본 컬럼명에는 여러 정보가 하나의 문자열에 뭉쳐 있었다.

```text
2026년07월_남_60~69세
```

이걸 `year → 2026`, `gender → 남`, `age_group → 60~69세`로 각각 분리하기 위해 `str.extract()`와 정규표현식을 사용했다.

```python
age_population["year"] = (
    age_population["variable"]
    .str.extract(r"(\d{4})년")[0]
)

age_population["gender"] = (
    age_population["variable"]
    .str.extract(r"월_(계|남|여)_")[0]
)

age_population["age_group"] = (
    age_population["variable"]
    .str.extract(r"월_(?:계|남|여)_(.+)$")[0]
)
```

최종적으로 `region / year / gender / age_group / population` 구조로 통일했다.

<br>

**3. 자동차·운전면허 데이터 전처리**

자동차 관련 데이터는 KOSIS, 경찰청, 국토교통통계누리 등 여러 기관에서 가져와서 파일별 구조 차이가 컸다. 특히 CSV는 파일마다 인코딩이 달라서 한 가지 인코딩만 지정하면 일부 파일을 읽지 못하는 문제가 있었다. 그래서 여러 인코딩을 순서대로 시도하는 공통 함수를 만들었다.

```python
encodings = [
    "utf-8-sig",
    "cp949",
    "utf-8",
    "euc-kr",
]
```

읽기에 성공한 인코딩을 사용하고, 모두 실패하면 오류를 발생시키도록 구성했다.

또 `"1,234"`, `"-"`, 빈 문자열, 결측치처럼 다양한 형태로 존재하는 숫자를 안전하게 정수로 변환하기 위해 `to_int()` 함수를 따로 만들었다.

```python
def to_int(value, default=0):

    if pd.isna(value):
        return default

    value = str(value).replace(",", "").strip()

    if value in ["", "-", "nan", "None"]:
        return default

    try:
        return int(float(value))
    except (ValueError, TypeError):
        return default
```

이렇게 공통 처리 함수를 만들어두니 데이터마다 같은 코드를 반복하지 않아도 됐다.

**3-1. 운전면허 소지자 데이터**

KOSIS 운전면허 데이터는 성별·연령별·지역별로 나뉘어 있었고, 여러 행으로 구성된 헤더와 병합 셀이 존재했다. 예를 들어 성별 데이터에서는 첫 번째 행의 연도 정보를 `ffill()`로 채웠다.

```python
years = df.iloc[0].ffill()
```

병합 셀 때문에 첫 값 이후가 비어 있는 면허 종류도 같은 방식으로 처리했다.

```python
data_df.iloc[:, 0] = (
    data_df.iloc[:, 0]
    .replace("", None)
    .ffill()
    .fillna("")
    .astype(str)
    .str.strip()
)
```

그리고 `총계`, `소계` 데이터를 제외하고 실제 남자·여자 데이터만 남긴 뒤, 최종적으로 `license_main / license_sub / year / gender / count` 구조로 변환했다. 자동차 데이터 전처리에서는 **원본 파일의 다중 헤더를 실제 분석 가능한 컬럼으로 풀어내는 작업**이 핵심이었다.

<br>

**4. 교통사고 데이터 전처리**

이번 프로젝트에서 가장 전처리가 복잡했던 데이터는 TAAS 교통사고 데이터였다. 연령대별·시간대별·기상상태별·사고유형별·월별·지역별 등 여러 기준으로 나뉘어 있었고, 하나의 Excel 안에서도 연도와 시간대가 다중 헤더 형태로 구성된 경우가 많았다.

**4-1. 병합 셀 처리**

TAAS 데이터에서는 같은 연령대에 `사고[건]`, `사망[명]`, `부상[명]`이 묶여 있어서 연령대가 병합 셀로 표현되어 있었다. pandas로 읽으면 병합된 셀의 아래쪽 값은 `NaN`으로 읽히기 때문에 `ffill()`을 사용했다.

```python
age_df["age_group"] = age_df["age_group"].ffill()
```

예를 들어 이런 구조가

```text
65~69세 | 사고[건]
NaN      | 사망[명]
NaN      | 부상[명]
```

이렇게 복원된다.

```text
65~69세 | 사고[건]
65~69세 | 사망[명]
65~69세 | 부상[명]
```

실제 연령대별 사고 전처리에서도 병합 셀을 채운 뒤 `사고`가 포함된 행만 선택하고 `합계` 행은 제외했다.

**4-2. 사고 건수 데이터 필터링**

TAAS 파일에는 사고 건수뿐 아니라 사망자·부상자 데이터가 함께 들어 있는 경우가 있어서, 필요한 데이터만 골라내기 위해 `str.contains()`를 사용했다.

```python
age_df = age_df[
    (age_df["category"]
        .astype(str)
        .str.contains("사고", na=False))
    &
    (age_df["age_group"]
        .astype(str)
        .str.strip() != "합계")
].copy()
```

이를 통해 전체 파일에서 실제 사고 건수 데이터만 추출했다.

**4-3. 숫자 데이터 정제**

공공데이터의 숫자는 `"5,470"`처럼 쉼표가 포함된 문자열인 경우가 많았다. 쉼표를 제거하고 숫자형으로 변환했다.

```python
age_df[col] = (
    age_df[col]
    .astype(str)
    .str.replace(",", "", regex=False)
    .astype(float)
    .astype(int)
)
```

이렇게 해야 이후 합계, 평균, 증감률 등의 계산이 가능해진다.

**4-4. 연도·월·시간대 분리**

지역별·월별 사고 데이터는 연도와 월이 각각 여러 헤더에 나뉘어 있었다. 먼저 연도와 월 정보를 따로 가져왔다.

```python
years = (
    df.iloc[0]
    .replace("", None)
    .ffill()
    .fillna("")
    .astype(str)
    .str.strip()
)

months = (
    df.iloc[1]
    .fillna("")
    .astype(str)
    .str.strip()
)
```

그리고 정규표현식으로 실제 숫자만 추출했다.

```python
year_match = re.search(r"(\d{4})", year_val)
month_match = re.search(r"(\d+)", month_val)
```

최종적으로 아래처럼 DB에서 바로 활용할 수 있는 구조로 변환했다.

```text
sido | sigungu | year | month | accidents
서울 | 종로구   | 2025 | 1     | 18
서울 | 종로구   | 2025 | 2     | 15
```

<br>

**5. 정책 데이터 전처리**

정책 데이터는 사고 데이터와 달리 숫자보다는 **문자열과 날짜 데이터의 표준화**가 중요했다. 여러 정책 파일에서 반복적으로 쓰이는 문자열 정제 작업은 공통 함수로 분리했다.

```python
def clean_string_columns(df, columns):

    for col in columns:
        if col in df.columns:
            df[col] = (
                df[col]
                .fillna("")
                .astype(str)
                .str.strip()
            )

    return df
```

`NaN → ""`, `" 서울 " → "서울"`처럼 데이터를 정리하는 함수다.

**5-1. 컬럼명 표준화**

원본 정책 데이터는 `교육일자`, `지부코드`, `교육반코드`, `예약정원`처럼 한글 컬럼명으로 구성되어 있었다. DB와 Python 코드에서 다루기 쉽도록 아래처럼 변경했다.

```python
df = df.rename(columns={
    "교육일자": "edu_date",
    "지부코드": "branch_name",
    "교육반코드": "course_name",
    "예약정원": "capacity"
})
```

날짜도 `pd.to_datetime()`으로 형식을 통일했다.

```python
df["edu_date"] = pd.to_datetime(
    df["edu_date"],
    errors="coerce"
).dt.strftime("%Y-%m-%d")
```

예약 정원은 숫자형으로 변환하고, 날짜가 없는 행은 제거한 뒤 DB에 필요한 컬럼만 남겼다. 전국 고령운전자 정책 데이터도 `현재 정책/제도 → policy_name`, `시행 상태 → status`, `대상 → target`, `핵심 내용 → content`, `담당기관 → agency`, `출처 URL → source_url`처럼 컬럼명을 통일했다.

<br>

**6. FAQ 데이터 전처리**

FAQ 데이터는 다른 통계 데이터보다 구조가 단순했지만, 검색 기능과 DB 저장을 고려해서 컬럼 구조를 통일했다. 필요한 5개 컬럼을 선택한 뒤 아래처럼 이름을 바꿨다.

```python
faq_df.columns = [
    "no",
    "category",
    "question",
    "answer",
    "source_url"
]
```

카테고리·질문·답변·URL은 공백과 결측값을 정리하고, 질문 번호는 `pd.to_numeric()`으로 숫자형 변환했다.

```python
faq_df["no"] = pd.to_numeric(
    faq_df["no"],
    errors="coerce"
)

faq_df = faq_df.dropna(
    subset=["no"]
)

faq_df["no"] = faq_df["no"].astype(int)
```

마지막으로 질문 내용이 없는 행을 제거해서 실제 검색에 쓸 수 있는 FAQ 데이터만 남겼다.

<br>

**7. 전처리 결과 및 느낀 점**

이번 전처리의 목표는 단순히 빈 값을 지우는 게 아니라, **서로 다른 기관에서 수집한 데이터를 하나의 서비스에서 함께 쓸 수 있는 구조로 통일하는 것**이었다. 전처리 과정에서 주로 사용한 pandas 기능은 다음과 같다.

| 기능 | 사용 목적 |
|---|---|
| `read_excel()` / `read_csv()` | 원본 데이터 로드 |
| `iloc[]` | 필요한 행·열 선택 |
| `ffill()` | 병합 셀로 발생한 결측값 복원 |
| `fillna()` / `dropna()` | 결측값 처리 |
| `rename()` | 컬럼명 표준화 |
| `str.strip()` | 문자열 공백 제거 |
| `str.replace()` | 불필요한 문자 제거 |
| `str.extract()` | 연도·월·성별·연령대 추출 |
| `pd.to_numeric()` | 문자열 → 숫자 변환 |
| `pd.to_datetime()` | 날짜 데이터 표준화 |
| `melt()` | Wide → Long 구조 변환 |
| `reset_index()` | 전처리 후 인덱스 초기화 |

특히 이번 프로젝트에서는 **Wide Format → Long Format 변환과 다중 헤더 처리**가 중요했다. 공공데이터는 사람이 Excel에서 보기 편하도록 만들어진 경우가 많지만, DB에 저장하거나 pandas에서 분석하려면 `지역 × 연도`, `지역 × 월`, `연령대 × 연도`처럼 **한 행이 하나의 관측값을 나타내는 구조**가 훨씬 다루기 편했다. 그래서 전처리 결과를 최대한

```text
지역 | 연도 | 구분 | 값
```

형태로 정규화하고, 이후 MySQL 테이블에 적재할 수 있도록 구성했다.

처음에는 공공데이터니까 파일을 읽고 컬럼명 정도만 손보면 바로 쓸 수 있을 줄 알았다. 하지만 실제로 열어보니 병합 셀, 다중 헤더, 합계 행, 문자열로 저장된 숫자, 파일마다 다른 인코딩과 컬럼 구조 등 파일마다 처리해야 할 부분이 다 달랐다. 특히 TAAS 교통사고 데이터는 연도·시간대·월·사고유형이 여러 행과 열에 걸쳐 표현되어 있어서, 데이터를 읽는 것보다 **원본 Excel의 구조를 먼저 이해하는 과정**이 더 오래 걸렸다.

> **원본 데이터의 의미를 파악하고 → 분석에 필요한 단위로 구조를 다시 설계하는 과정**

이번 전처리를 거치면서, 단순히 pandas 문법을 아는 것보다 이 과정 자체가 데이터 전처리의 핵심이라는 걸 느꼈다.

<br>


