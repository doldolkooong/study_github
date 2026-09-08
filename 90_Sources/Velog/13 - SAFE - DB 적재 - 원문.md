---
type: source
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-DB-%EC%A0%81%EC%9E%AC"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] 1st 프로젝트 - DB 적재"
source_id: 70171360-d3e3-4416-af50-eef3ad083285
source_author: doldolkoong
source_published: 2026-08-26
source_updated: 2026-09-02
archived: 2026-09-08
tags:
  - velog-source
---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] 1st 프로젝트 - DB 적재

[Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-1st-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-DB-%EC%A0%81%EC%9E%AC) · [[SAFE - DB 적재|SAFE - DB 적재]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

[플레이데이터 SK네트웍스 Family AI 캠프 36기] 1st 프로젝트 - 데이터 전처리 & DB 적재

# 1st 프로젝트 - 데이터 전처리 & DB 적재

> **📖 오늘 정리 내용**
> 1. 데이터 전처리 방향
> 2. 인구 데이터 전처리
> 3. 자동차 데이터 전처리
> 4. 교통사고 데이터 전처리
> 5. 정책 데이터 전처리
> 6. FAQ 데이터 전처리
> 7. MySQL 데이터 적재
> 8. 전처리 및 적재 결과

<br>

이전 단계에서는 SAFE에서 사용할 데이터를 **인구 / 자동차 / 교통사고 / 정책 / FAQ**로 구분하고, 각각 어떤 데이터를 사용할지 정의했다. 문제는 수집한 공공데이터를 그대로 사용할 수 없었다는 점이다.

데이터 출처가 행정안전부, KOSIS, 경찰청, 국토교통통계누리, TAAS 등으로 다양하다 보니, 같은 Excel·CSV 형식이라도 실제 내부 구조는 파일마다 전부 달랐다. 공공데이터를 하나씩 열어보며 다음과 같은 문제들을 발견했다.

> - 병합 셀로 인해 일부 값이 비어 있음
- 실제 데이터보다 위에 제목이나 설명 행이 존재함
- `계`, `합계`, `총계` 등 분석에 불필요한 집계 행이 포함됨
- 숫자가 `"1,234"`와 같은 문자열 형태로 저장됨
- 연도, 월, 시간대가 여러 열에 걸쳐 반복됨
- 데이터마다 컬럼명이 다름
- 날짜 및 숫자의 자료형이 일정하지 않음

그래서 이번 단계에서는 pandas로 데이터를 정제하고, 이후 분석과 MySQL 적재가 가능하도록 데이터 구조를 표준화하는 작업을 진행했다. 전체 처리 과정은 다음과 같이 잡았다.

```text
Excel / CSV 원본 데이터
        ↓
pandas 데이터 로드
        ↓
필요한 행 / 열 추출
        ↓
결측치 및 병합 셀 처리
        ↓
합계 / 불필요 데이터 제거
        ↓
컬럼명 및 자료형 표준화
        ↓
Wide → Long 구조 변환
        ↓
전처리된 DataFrame
        ↓
SQLAlchemy
        ↓
MySQL 적재
```

<br>

**1. 데이터 전처리 방향**

이번 전처리에서 가장 중요하게 생각한 부분은, 서로 다른 구조를 가진 공공데이터를 이후 하나의 서비스에서 사용할 수 있는 형태로 통일하는 것이었다. 단순히 `NaN`을 지우는 게 아니라 데이터의 의미를 먼저 확인한 뒤 필요한 값만 추출하고, DB 테이블 구조에 맞는 형태로 변환했다.

주로 사용한 pandas 기능은 다음과 같다.

| 기능 | 활용 |
|---|---|
| `pd.read_excel()` | Excel 데이터 로드 |
| `pd.read_csv()` | CSV 데이터 로드 |
| `iloc` | 필요한 행과 열 추출 |
| `ffill()` | 병합 셀로 인한 결측값 처리 |
| `fillna()` | 결측값 대체 |
| `dropna()` | 필요 값이 없는 행 제거 |
| `rename()` | 컬럼명 표준화 |
| `str.strip()` | 문자열 공백 제거 |
| `str.replace()` | 쉼표 및 불필요 문자열 제거 |
| `str.extract()` | 연도, 성별, 연령대 등 추출 |
| `pd.to_numeric()` | 문자열 데이터를 숫자로 변환 |
| `pd.to_datetime()` | 날짜 데이터 표준화 |
| `melt()` | Wide Format을 Long Format으로 변환 |
| `reset_index()` | 전처리 후 인덱스 초기화 |

<br>

**2. 인구 데이터 전처리**

인구 데이터는 크게 **지역별 전체 인구**와 **지역별 연령대·성별 인구** 두 가지 형태로 구성했다. 최종적으로 MySQL에서는 다음과 같은 구조로 저장하도록 설계했다.

```text
local_population
--------------------------------
region
year
population

age_population
--------------------------------
region
year
gender
age_group
population
```

원본 파일의 형태가 서로 달라도 최종적으로는 지역과 연도를 기준으로 조회할 수 있는 구조로 통일한 것이다. 이 구조는 이후 자동차 등록대수나 교통사고 발생건수와 인구 데이터를 연결하기 위한 것이다. 실제 적재 코드에서도 `local_population`, `age_population` 두 테이블을 만들고 각각 전처리 함수와 연결했다.

**Wide → Long 변환**

공공데이터에서는 연도가 다음처럼 열로 구성된 경우가 많았다.

```text
지역 | 2021 | 2022 | 2023 | 2024 | 2025
서울 | ...  | ...  | ...  | ...  | ...
부산 | ...  | ...  | ...  | ...  | ...
```

이 형태는 사람이 Excel에서 보기엔 편하지만, 연도별 조회나 DB 저장에는 적합하지 않다. 그래서 `melt()`를 이용해 다음과 같이 변환했다.

```text
지역 | 연도 | 인구수
서울 | 2021 | ...
서울 | 2022 | ...
서울 | 2023 | ...
```

이렇게 한 행이 하나의 관측값을 나타내는 **Long Format**으로 데이터를 통일했다.

<br>

**3. 자동차 데이터 전처리**

자동차 데이터는 단순 등록대수뿐 아니라 운전면허와 자진반납 데이터까지 함께 다뤘다. 전처리한 데이터는 다음과 같이 구분했다.

> - 운전면허 소지자 - 성별
- 운전면허 소지자 - 연령별
- 운전면허 소지자 - 지역별
- 운전면허 자진반납 - 2023
- 운전면허 자진반납 - 2025
- 경찰청 운전면허 지역/성별/종별
- 자동차 등록 - 연도별
- 자동차 등록 - 지역/월별

실제 DB 적재 단계에서도 총 8개의 테이블로 나누어 관리했다.

운전면허 데이터는 원본 Excel에 병합 셀이 많아서 `ffill()`로 누락된 값을 위쪽 값으로 채우는 방식으로 처리했다. 예를 들어 원본이 다음과 같다면

```text
1종 | 대형
    | 보통
    | 소형
```

pandas에서는 빈 셀이 `NaN`으로 읽히기 때문에 다음과 같이 변환했다.

```text
1종 | 대형
1종 | 보통
1종 | 소형
```

이후 면허 종류, 연도, 성별, 연령, 지역 등의 정보를 각각 독립적인 컬럼으로 구성했다. 자동차 등록 데이터도 차량 종류와 용도를 별도 컬럼으로 분리해서

```text
year
vehicle_type
vehicle_usage
count
```

또는

```text
month
sido
sigungu
vehicle_type
vehicle_usage
count
```

형태로 구성했다. 실제 MySQL 테이블도 동일한 구조로 정의했다.

<br>

**4. 교통사고 데이터 전처리**

5개 데이터 카테고리 중 가장 전처리가 복잡했던 데이터가 교통사고 데이터였다. TAAS 데이터를 다음과 같이 세분화해서 사용했다.

> - 가해운전자 연령대별 사고
- 가해운전자 시간대별 사고
- 기상상태별 사고
- 고령운전자 사고유형 × 시간대
- 고령운전자 월 × 시간대
- 고령운전자 지역 × 월
- 연령대별 전체 교통사고
- 지역별 전체 교통사고

실제 적재 코드에서도 각 데이터에 대응하는 8개의 전처리 함수를 별도로 연결했다.

**병합 셀 처리**

TAAS Excel에서는 동일한 연령대나 지역의 값이 병합 셀로 표현된 경우가 많았다. 예를 들어

```text
65~69세 | 사고[건]
         | 사망[명]
         | 부상[명]
```

처럼 구성되어 있는데, Excel에서는 하나의 셀처럼 보이지만 pandas에서는 아래 행들이 결측값으로 들어온다. `ffill()`을 이용해

```text
65~69세 | 사고[건]
65~69세 | 사망[명]
65~69세 | 부상[명]
```

형태로 복원했다.

**사고 / 사망 / 부상 분리**

지역별·연령대별 데이터에서는 단순 사고 건수만 저장하지 않고 `accidents / deaths / injuries` 세 지표를 함께 쓸 수 있도록 구성했다. 최종적으로 지역별 사고 데이터는

```text
sido
sigungu
year
accidents
deaths
injuries
```

연령대별 사고 데이터는

```text
age_group
year
accidents
deaths
injuries
```

형태로 구성했고, DB 테이블도 이 구조를 그대로 사용하도록 설계했다. DB 적재 직전에도 필요한 컬럼이 실제 DataFrame에 존재하는지 검사하고, `year`, `accidents`, `deaths`, `injuries`를 다시 숫자형으로 변환하도록 했다. 전처리 결과가 예상한 스키마와 다른 상태로 DB에 들어가는 걸 막기 위한 안전장치였다.

<br>

**5. 정책 데이터 전처리**

정책 데이터는 교통사고처럼 복잡한 숫자 데이터보다는 **문자열과 날짜를 표준화하는 작업**이 중심이었다. 정책 데이터는 총 4가지로 구성했다.

> - 고령운전자 교통안전교육 예약
- 전국 고령운전자 정책
- 지역 특화 고령운전자 정책
- 지역별 운전면허 자진반납 정책

실제 MySQL에서도 이를 각각 독립적인 테이블로 구성했다.

**컬럼명 표준화**

예를 들어 교육 예약정보는 원본 컬럼 `교육일자 / 지부코드 / 교육반코드 / 예약정원`을 `edu_date / branch_name / course_name / capacity`로 변경했다. 정책 데이터도 `정책명 → policy_name`, `시행 상태 → status`, `대상 → target`, `담당기관 → agency`, `출처 URL → source_url`처럼 Python과 DB에서 쓰기 쉬운 이름으로 표준화했다.

날짜 데이터는 `pd.to_datetime()`으로 변환하고, 문자열 데이터는 `fillna()`, `astype(str)`, `str.strip()` 등으로 결측값과 불필요한 공백을 정리했다. 전처리가 끝난 4개의 DataFrame은 각각 `education_reservation`, `old_driver_policy`, `region_old_driver_policy`, `return_license_policy` 테이블과 연결된다.

<br>

**6. FAQ 데이터 전처리**

FAQ 데이터는 다른 데이터보다 구조가 단순했지만, 웹 서비스에서 검색할 수 있도록 컬럼 구조를 통일했다. 최종적으로 `no / category / question / answer / source_url`로 구성했다. `no`는 정수형으로 변환하고, 카테고리·질문·답변의 결측값과 불필요한 공백을 정리했다. FAQ는 이후 사용자가 카테고리를 선택하거나 질문을 검색할 수 있도록 별도의 `traffic_faq` 테이블에 저장했다.

<br>

**7. MySQL 데이터 적재**

전처리가 끝난 데이터를 파일로 다시 저장하는 대신, **MySQL에 바로 적재하는 구조**로 구현했다. DB 연결은 SQLAlchemy의 `create_engine()`과 PyMySQL 드라이버를 사용했다.

```python
url = (
    f"mysql+pymysql://{DB_USER}:{DB_PASSWORD}"
    f"@{DB_HOST}:{DB_PORT}/{DB_NAME}"
    f"?charset=utf8mb4"
)
```

DB 접속 정보는 코드에 직접 작성하지 않고 `.env`에서 가져오도록 구성했다. 전체 적재 과정은 공통적으로 다음 순서로 구현했다.

```text
MySQL 연결
    ↓
CREATE TABLE IF NOT EXISTS
    ↓
기존 데이터 TRUNCATE
    ↓
전처리 함수 실행
    ↓
빈 DataFrame 검사
    ↓
컬럼 및 자료형 확인
    ↓
DataFrame.to_sql()
    ↓
MySQL INSERT
```

예를 들어 자동차 데이터에서는 테이블과 전처리 함수를 딕셔너리로 연결했다.

```python
tables = {
    "license_holder_gender": license_holder_gender_data,
    "license_holder_age": license_holder_age_data,
    "license_holder_region": license_holder_region_data,
    "return_driver_license_2023": return_driver_license_2023_data,
    "return_driver_license_2025": return_driver_license_2025,
    "driver_license_region": driver_license_region_data,
    "car_registration_year": car_registration_data,
    "car_registration_region": car_registration_region_data,
}
```

이후 반복문에서 각 전처리 함수를 실행하고, 결과 DataFrame을 대응하는 테이블에 저장했다. 실제 적재는 pandas의 `to_sql()`을 사용했다.

```python
df.to_sql(
    name=table_name,
    con=engine,
    if_exists="append",
    index=False,
    chunksize=1000,
)
```

`chunksize=1000`으로 설정해서 데이터를 1,000행 단위로 나누어 INSERT하도록 했다. 자동차뿐 아니라 인구, 사고, 정책, FAQ 적재 코드에서도 동일한 패턴을 사용했다.

<br>

**8. 전처리 및 적재 결과**

최종적으로 데이터 처리 구조를 다음과 같이 구성할 수 있었다.

```text
[공공데이터]
Excel / CSV
      ↓
[data_process]
pandas 전처리
      ↓
결측치 처리
병합 셀 처리
컬럼 표준화
자료형 변환
Wide → Long 변환
      ↓
[load_data]
전처리 함수 실행
      ↓
SQLAlchemy
      ↓
[MySQL]
인구 / 자동차 / 사고 / 정책 / FAQ
```

처음에는 공공데이터니까 Excel이나 CSV를 pandas로 불러온 뒤 컬럼명 정도만 손보면 바로 쓸 수 있을 거라 생각했다. 하지만 실제로는 병합 셀, 다중 헤더, 합계 행, 문자열 형태의 숫자, 서로 다른 데이터 구조 때문에 각 파일의 구조를 먼저 파악하는 과정이 필요했다.

특히 이번 작업을 하면서, 데이터 전처리는 단순히 결측치를 제거하는 과정이 아니라

> **원본 데이터의 의미를 파악하고, 분석과 서비스에서 사용하기 좋은 구조로 다시 설계하는 과정**

이라는 점을 알게 됐다. 또한 전처리 함수와 DB 적재 코드를 분리하면서, `data_process → 데이터 정제 및 구조 변환`, `load_data → 테이블 생성 및 DB 적재`로 역할을 나눌 수 있었다.

<br>


