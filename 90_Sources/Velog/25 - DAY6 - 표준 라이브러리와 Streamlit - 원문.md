---
type: source
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY6-2026.08.13"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY6 (26.08.13)"
source_id: 12bb737b-ff20-4348-8f21-926bb37a2390
source_author: doldolkoong
source_published: 2026-08-14
source_updated: 2026-09-01
archived: 2026-09-08
tags:
  - velog-source
---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY6 (26.08.13)

[Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY6-2026.08.13) · [[DAY6 - 표준 라이브러리와 Streamlit|DAY6 - 표준 라이브러리와 Streamlit]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY6 (26.08.13)


**DAY 6**

> 📖 오늘 학습 내용
> 1. 하나 빼기 게임 구현하기
> 2. 표준 라이브러리 (collections, math, datetime, 텍스트 표준 라이브러리, 정규표현식)
> 3. streamlit

**1. 하나 빼기 게임 구현하기**

기존 가위바위보 게임에 "하나 빼기" 기능을 추가하는 문제를 풀었다.

- computer_choice는 랜덤으로 두 개의 값을 뽑는다.
- user_choice는 입력값을 받아 split으로 나눈다.
- 둘 중 하나를 선택해서 최종 대결을 진행한다. (컴퓨터는 랜덤, 사용자는 입력)
- 비기면 처음부터 다시 시작하고, 승패가 갈리면 종료한다.

```python
import random
import enum

class rsp_choice(enum.Enum):  # 가위, 바위, 보에 값을 넣은 상수 생성
    가위 = 0
    바위 = 1
    보 = 2

def game(final_user_choice, final_computer_choice):
    if final_user_choice not in rsp_choice.__members__:
        print("잘못 입력했습니다. 다시 입력해주세요.")

    # 1일 경우 승, 2일 경우 패, 0일 경우 무승부
    result = (rsp_choice[final_user_choice].value - rsp_choice[final_computer_choice].value) % 3

    if result == 1:
        print("~User의 승리입니다.~")
    elif result == 2:
        print("~Computer의 승리입니다.~")

    return result

while True:
    print("====가위 바위 보!====")
    computer_choice = [random.choice(list(rsp_choice.__members__)) for i in range(2)]
    user_choice = input("가위, 바위, 보 중 두 가지 적어주세요(ex. 가위, 바위): ").split(", ")

    print(f"사용자의 입력 : {user_choice}")
    print(f"컴퓨터의 입력 : {computer_choice}")
    print("====하나 빼기!====")

    final_user_choice = input(f"{user_choice} 중 하나 골라서 적어주세요: ")
    final_computer_choice = random.choice(computer_choice)

    print(f"<user의 선택: {final_user_choice}>")
    print(f"<computer의 선택 : {final_computer_choice}>")

    game_result = game(final_user_choice, final_computer_choice)

    if game_result in (1, 2):
        print("게임 종료")
        break
```

중복되게 여러 개 뽑는 법은 `random.choices([], k=?)`, 중복 안 되게 여러 개 뽑는 법은 `random.sample([], k=?)`를 사용한다.

> 오류 잡는 부분도 추가해봐야겠다.

<br>

**2. 표준 라이브러리**

파이썬에서 기본적으로 제공하는, 개발할 때 자주 사용하는 함수/클래스들을 모아둔 것이 표준 라이브러리다.

**2-1) collections**

수집한 것을 카운트할 때 사용한다.

```python
from collections import Counter

lst = ["aa", "aa", "bb", "aa", "bb", "bb", "tt", "bb"]

counter = Counter(lst)
counter
```
> Counter({'bb': 4, 'aa': 3, 'tt': 1})

```python
dict(counter)
```
> {'aa': 3, 'bb': 4, 'tt': 1}

```python
list(counter.elements())
```
> ['aa', 'aa', 'aa', 'bb', 'bb', 'bb', 'bb', 'tt']

<br>

**2-2) math**

```python
import math

math.pi          # 3.141592653589793
math.log(10)      # 2.302585092994046
math.exp(10)      # e**10
math.pow(2, 4)    # 2의 4제곱 -> 16.0
math.sqrt(100)    # 제곱근 -> 10.0
math.ceil(4.55)   # 올림 -> 5
```

<br>

**2-3) datetime**

```python
from datetime import datetime

now = datetime.now()
now
```
> datetime.datetime(2026, 8, 13, 11, 14, 18, 213508)

년, 월, 일, 시간, 분, 초, 밀리초 순서로 저장된다.

```python
now.strftime("%Y-%m-%d %H:%M:%S")
```
> '2026-08-13 11:17:11'

```python
str_datetime = '2026-08-13 11:17:11'
datetime.strptime(str_datetime, "%Y-%m-%d %H:%M:%S")
```
> datetime.datetime(2026, 8, 13, 11, 17, 11)

`weekday()`를 이용하면 태어난 날이 무슨 요일이었는지도 확인할 수 있다. (0: 월요일 ~ 6: 일요일)

`timedelta`를 쓰면 시간 연산이 쉬워진다.

```python
from datetime import datetime, timedelta

now = datetime.now()
diff = timedelta(days=1, hours=3, minutes=30)

now - diff
```
> datetime.datetime(2026, 8, 12, 8, 8, 24, 413354)

<br>

**2-4) 텍스트 표준 라이브러리**

URL을 인코딩/디코딩할 때는 `urllib.parse`를 사용한다.

```python
from urllib import parse

parse.unquote(naver_str)   # 인코딩된 URL을 디코딩
parse.quote(naver_url)     # URL을 인코딩
```

<br>

**2-5) 정규표현식**

패턴이 명확하고 비교적 단순할 때 사용한다. (전화번호, 이메일, 주민등록번호, 날짜 등) 반대로 XML, HTML(BeautifulSoup으로 처리), JavaScript처럼 구조가 복잡한 경우에는 사용을 피하는 게 좋다.

- `\d` : 숫자와 매치
- `\D` : 숫자가 아닌 것과 매치
- `\s` : whitespace 문자와 매치
- `\S` : whitespace가 아닌 문자와 매치
- `\w` : 문자 + 숫자와 매치 `[a-zA-Z0-9_]`
- `\W` : 문자 + 숫자가 아닌 문자와 매치

```python
import re

txt = "a1b2c3d4e5f6g7h8i9j0"

pat = re.compile("[a-zA-Z]")  # a부터 z 사이의 문자만 추출
pat.findall(txt)
```
> ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']

```python
pat = re.compile("[0-9]")  # 숫자만 추출
pat.findall(txt)
```
> ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0']

<br>

**3. streamlit**

`streamlit`은 웹/앱을 빠르게 만들 수 있는 라이브러리다. 다음 프로젝트에서는 백엔드는 FastAPI, 프론트엔드는 streamlit으로 구성할 예정이다.

`requirements.txt`
```
streamlit             # 웹/앱 라이브러리
pandas                # 데이터 분석용 라이브러리
numpy                 # 데이터 분석용 라이브러리
matplotlib             # 시각화용 라이브러리
seaborn                # 시각화용 라이브러리 (matplotlib 기반)
finance-datareader     # 금융 데이터 다운로드 라이브러리
```

```
uv add -r .\requirements.txt

# 가상환경 들어가기
.\.venv\Scripts\activate

# 잘 깔렸는지 확인
streamlit hello
```

실행 후 `streamlit run ex01.py`를 입력하면 로컬 서버가 켜지고, 코드를 수정하면 실시간으로 반영되는 게 신기했다. `ctrl + c`로 서버를 끌 수 있다.

<br>

**1) 마크다운, 제목/헤더**

```python
import streamlit as st

st.title("이 몸은 제목이시다 ㅋㅋ")
st.header("내가 머리글이다 :sparkles:")
st.caption("캡션 :bulb:")

st.code("""
def get_hello():
    print("hello, world")
""", language="python")

st.text("나는 텍스트야.")
st.markdown(":green[$x^2 = e^{i\\pi} + 1 = 0$]")
st.text_input("텍스트 입력하라고!!!!!!!!!!!!!!!!! : ")
```

py 파일이 HTML로 변환되어 네트워크를 통해 웹으로 전달되고, 브라우저가 이를 렌더링해서 보여주는 방식이라고 한다. 이모지는 emojidb.org에서 찾아 쓸 수 있다.

<br>

** 2) 데이터프레임 표시**

```python
import streamlit as st
import pandas as pd
import numpy as np

df = pd.DataFrame(
    {
        "name": ["Roadmap", "Extras", "Issues"],
        "url": [
            "https://roadmap.streamlit.app",
            "https://extras.steramlit.app",
            "https://issues.streamlit.app"
        ],
        "stars": [np.random.randint(0, 1000) for _ in range(3)],
        "views_history": [
            [np.random.randint(0, 5000) for _ in range(30)] for _ in range(3)
        ]
    }
)

st.title("DataFrame")
st.dataframe(
    df,
    column_config={
        "name": "App Name",
        "url": st.column_config.LinkColumn("App URL"),
        "stars": st.column_config.NumberColumn("GitHub Stars", format="%d 💀"),
        "views_history": st.column_config.LineChartColumn("Views history", y_min=0, y_max=5000)
    },
    hide_index=True
)
```

`df.style.highlight_max(axis=0)`처럼 스타일을 입힐 수도 있다. (row가 axis=0, column이 axis=1)

<br>

** 3) 버튼, 폼, 링크 버튼**

```python
import streamlit as st

st.button("Reset", type="primary")  # primary는 빨간색으로 표시

if st.button("Say hello"):
    st.write("그만눌러;;;;")
```

```python
with st.form(key="my_form"):
    text_input = st.text_input(label="이름 적으라고").strip()
    submit_button = st.form_submit_button(label="Submit")

if submit_button and text_input:
    st.write(f"안녕하시오... {text_input}")
```

```python
st.link_button("go naver", "https://www.naver.com")
```

<br>

** 4) 멀티페이지**

`pages` 폴더 안에 페이지 파일을 넣어두면 streamlit이 자동으로 페이지를 연결해준다.

```python
# page01.py
import streamlit as st
st.title("Page 01")

# page02.py
import streamlit as st
st.title("Page 02")
```

---

🤔💭 KPT

> 👍Keep
> 앞으로 발표는 마크다운 파일을 PDF로 변환하여 보여주며 할 거라고 하셨다. 마크다운 언어도 공부 한번 해봐야겠다. 스트림릿을 이용한 웹페이지 만들기를 했는데 실시간으로 자동 변경되는 게 신기했다.

> 😂Problem
가위바위보 문제를 해결하면서 사용자 입력에 대한 오류 처리를 고려하지 않은 것이 문제였다. 다양한 잘못된 입력이 들어오는 상황을 생각하고 예외 처리를 추가해야겠다

> 🔥Try
발표 자료를 직접 만들어보면서 제목, 목록, 표, 코드 블록 등 기본적인 마크다운 문법을 공부해보기.
가위바위보 오류 잡는 거 해결하기
