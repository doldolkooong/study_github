---
type: source
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY5-26.08.12"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY5 (26.08.12)"
source_id: 8e7da724-03d8-42c9-9580-e5d2208023ce
source_author: doldolkoong
source_published: 2026-08-12
source_updated: 2026-09-01
archived: 2026-09-08
tags:
  - velog-source
---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY5 (26.08.12)

[Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY5-26.08.12) · [[DAY5 - Enum과 클래스 및 모듈|DAY5 - Enum과 클래스 및 모듈]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

### [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY5 (26.08.12)

**DAY 5**


**📖 오늘 학습 내용**
>1. 가위바위보 문제 (enum 활용)
2. 클래스
3. 상속
4. 접근 지정자 (public/private)
5. 데코레이터 (@property)
6. 매직 메서드
7. 디자인 패턴 - 싱글톤
8. 모듈

<br>

**1. 가위바위보 문제 (enum 활용)**

강사님은 enum을 활용해서 가위/바위/보에 값을 부여하고, 두 값의 차이를 3으로 나눈 나머지로 승패를 판단하는 방식으로 코드를 짧게 작성하셨어서 나도 그렇게 작성해봤다.

```python
import random
import enum

class rsp_choice(enum.Enum): # 가위, 바위, 보에 값을 넣은 상수 생성
    가위 = 0
    바위 = 1
    보 = 2

# 게임이 진행되는 함수
def game(user_choice, computer_choice):
    if user_choice not in rsp_choice.__members__: # 사용자가 rsp_choice에서 선택하지 않은 경우 출력
        print("잘못 입력했습니다. 다시 입력해주세요.")

    # 1일 경우 승, 2일 경우 패, 0일 경우 무승부
    result = (rsp_choice[user_choice].value - rsp_choice[computer_choice].value) % 3

    if result == 1:
        print("====User의 승리입니다.=====")
    elif result == 2:
        print("====Computer의 승리입니다.====")

    return result

while True:
    computer_choice = random.choice(list(rsp_choice.__members__)) # rsp_choice에서 computer가 랜덤으로 선택
    user_choice = input("가위, 바위, 보 중 하나 적어주세요: ") # 사용자의 입력 받음

    game_result = game(user_choice, computer_choice)

    print(f"<user의 선택: {user_choice}>")
    print(f"<computer의 선택 : {computer_choice}>")

    # 승패가 결정된 경우
    if game_result in (1, 2):
        print("게임 종료")
        break
```

`(user - computer) % 3` 이라는 식 하나로 승/패/무승부를 다 표현할 수 있다는 게 인상 깊었다.

> 💡 `uv init --app --python 3.12` / `uv init --bare --python 3.12` 로 `src` 폴더 없이 프로젝트를 초기화할 수 있다.


<br>


**2. 클래스**

> - 클래스 : 객체를 만들기 위한 설계도
> - 인스턴스 : 클래스를 메모리에 올린 것(=객체)
> - 속성(attribute) : 클래스 내부 변수
> - 메소드(method) : 클래스 내부 함수
> - self : 인스턴스(객체) 자기 자신을 가리킴

```python
class GrandMother: # 클래스 : 설계도
    family = "grandparents" # 속성 : 클래스 내부 변수

    def print_self(self): # 메소드 : 클래스 내부 함수
        print(self)

LEE = GrandMother() # 인스턴스
```

클래스는 하나지만, 인스턴스는 여러 개 만들 수 있고 각각 독립적으로 존재한다.

```python
type(GrandMother)
> type

type(LEE)
> __main__.GrandMother

LEE.family # 클래스의 변수 호출
> 'grandparents'

LEE.print_self() # 클래스의 함수 호출
> <__main__.GrandMother object at 0x0000023A598FFA10>
```

클래스의 함수는 인스턴스가 아닌 클래스 자체에서 바로 호출하면 self 값이 없어서 에러가 난다.

```python
GrandMother.print_self() # 입력변수 self가 들어가지 않은 상태
> TypeError: GrandMother.print_self() missing 1 required positional argument: 'self'
```

**`__init__` (생성함수)**

인스턴스화를 실행할 때 자동으로 실행되는 특수함수(매직 메소드)로, 메소드에서 사용할 변수들을 정의/선언/초기화한다.

```python
class GrandMother:
    family = "grandparents"

    def __init__(self, p_name: str, p_age: int) -> None:
        print("생성함수 실행했어요")
        self.name = p_name if p_name is not None else "없음"
        self.age = p_age if p_age is not None and isinstance(p_age, int) else 0

    def print_self(self):
        print(self)

    def print_hello(self, p_new_name: str = None) -> None:
        if p_new_name is not None:
            # 값(데이터)가 존재한다면,
            self.name = p_new_name # 수정

        print(f"{self.name}님, (나이 : {self.age})안녕하세요.")
        print("Hello World")

LEE = GrandMother("홍", 33)
> 생성함수 실행했어요

LEE.print_hello("심")
> 심님, (나이 : 33)안녕하세요.
> Hello World

LEE.name
> '심'
```

인스턴스마다 독립적으로 값을 가지므로, `LEE`와 `KIM`을 각각 다른 이름/나이로 생성하면 서로 영향을 주지 않는다.

```python
LEE = GrandMother("히", 56)
KIM = GrandMother("후후후", 99)

LEE.name # '히'
KIM.name # '후후후'
```
<br>

**3. 상속**

부모 클래스(`GrandMother`)를 상속받은 자식 클래스(`Father`)는 부모의 속성과 메소드를 그대로 사용할 수 있다.

```python
LEE = Father(p_name = "홍", p_age = 33)
KIM = GrandMother("신", 35)
```

다만 상속은 단방향이라, 부모는 자식이 새로 정의한 메소드(`print_goodjob` 등)를 사용할 수 없다.

```python
KIM.print_goodjob()
> AttributeError: 'GrandMother' object has no attribute 'print_goodjob'
```

`Father`는 `GrandMother`의 모든 코드를 상속받았지만, `GrandMother`는 `Father`의 상속을 받지 않았기 때문에 발생하는 에러다.

<br>


**4. 접근 지정자**

> - public : 외부에서 접속 가능
> - private : 내부에서만 접속 가능

```python
class Student:
    def __init__(self, name, age):
        self.name = name # public attribute
        self.age = age # public attribute

    def print_message(self): # public method
        print("Hello World")

std = Student("홍길동", 33)
std.name # 외부에서 접속(호출)
> '홍길동'

std.print_message() # 외부에서 함수 호출
> Hello World
```

```python
class Student:
    def __init__(self, name, age):
        self.__name = name # private attribute
        self.age = age # public attribute

    def __print_message(self): # private method
        print("Hello World")

std = Student("홍길동", 33)

std.__name # 외부에서 접속(호출)
> AttributeError: 'Student' object has no attribute '__name'

std.print_message() # 외부에서 함수 호출
> AttributeError: 'Student' object has no attribute 'print_message'

std.age
> 33
```

`__`가 붙은 속성/메소드는 클래스 외부에서 직접 접근하면 `AttributeError`가 발생한다.


<br>

**5. 데코레이터 (`@property`)**

private 변수를 안전하게 조회/수정/삭제하기 위해 `@property`, `@name.setter`, `@name.deleter`를 사용한다.

```python
class Student:
    def __init__(self, name): # 생성
        print("생성")
        self.__name = name

    @property # 조회
    def name(self): # private 변수를 호출하는 함수
        print("조회")
        return self.__name

    @name.setter
    def name(self, new_name): # 수정
        print("수정")
        self.__name = new_name

    @name.deleter
    def name(self): # 삭제
        print("삭제")
        del self.__name

std = Student("홍길동")
> 생성

std.name = '심'
> 수정

std.name # 업데이트
> 조회
> '심'
```

이렇게 하면 `std.name`처럼 마치 일반 속성처럼 접근하면서도, 내부적으로는 조회/수정/삭제 로직을 커스터마이징할 수 있다.

<br>


**6. 매직 메서드**

파이썬 내장 객체(`int` 등)도 `__add__`, `__str__` 같은 매직 메서드로 동작이 정의되어 있다는 걸 `dir(int)`로 확인했다.

```python
class MyDataset:

    def __init__(self, data):
        print("생성함수야~~~")
        self.data = data

    def __call__(self, param): # 객체를 함수처럼 쓸 수 있게 해주는 거
        print(f"{param} 데이터가 들어왔어요!")
        return len(self.data)

    def __getitem__(self, idx: int):
        print(f"{idx}가 들어왔어요~~")
        return self.data[idx]

    def __len__(self):
        print("코딩ㅋㅋ")
        return len(self.data)

    def __str__(self):
        print("안녕이다")
        return "매직 메소드"

dt = MyDataset(list(range(50, 100))) # __init__ 호출
> 생성함수야~~~

dt("홍길동") # __call__ 호출
> 홍길동 데이터가 들어왔어요!
> 50

dt[-1] # __getitem__ 호출
> -1가 들어왔어요~~
> 99

len(dt) # __len__ 호출
> 코딩ㅋㅋ
> 50

str(dt) # __str__ 호출
> 안녕이다
> '매직 메소드'
```

매직 메서드를 정의하면 내가 만든 객체도 파이썬 내장 함수/연산자처럼 자연스럽게 다룰 수 있다는 걸 배웠다.

<br>

**7. 디자인 패턴 - 싱글톤**

같은 클래스를 여러 번 인스턴스화해도 항상 같은 객체를 반환하도록 만드는 패턴이다.

```python
import random

class Database:
    _instance = None

    def __init__(self):
        self.id = random.randint(0, 10000)
        print(f"Instance ID: {self.id}")

db1 = Database()
db2 = Database()

db1.id == db2.id
> Instance ID: 419
> Instance ID: 485
> False
```

그냥 `__init__`만 있으면 호출할 때마다 새로운 인스턴스가 생겨서 싱글톤이 되지 않는다.

**`__new__`를 이용한 방법**

```python
import random

class Database:
    _instance = None # class attribute

    def __init__(self): # private
        self.id = random.randint(0, 10000)
        print(f"Instance ID: {self.id}")

    # __new__()는 __init__() 전에 실행하는 함수
    def __new__(cls, *args, **kwargs): # 객체가 실행되기 전에, 변수 몇 개가 들어올지 몰라서 가변 파라미터
        if cls._instance is None: # 만약 _instance가 초기값이면(한번도 인스턴스화 된 적이 없다면)
            cls._instance = super(Database, cls).__new__(cls, *args, **kwargs)

        return cls._instance # 기존 생성된 _instance 리턴

db1 = Database()
db2 = Database()

print(db1.id, db2.id)
db1 == db2
> Instance ID: 4118
> Instance ID: 427
> 427 427
> True
```

`_instance`가 없을 때만 새로 만들고, 이미 있으면 기존 걸 리턴하도록 해서 진짜 싱글톤을 구현했다.

**메타클래스를 이용한 방법**

```python
import random

class Singleton(type):
    _instances = {}

    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super(Singleton, cls).__call__(*args, **kwargs)

        return cls._instances[cls]

class Database(metaclass=Singleton):

    def __init__(self): # private
        self.id = random.randint(0, 10000)
        print(f"Instance ID: {self.id}")

db1 = Database()
db2 = Database()

print(db1.id, db2.id)
> Instance ID: 1203
> 1203 1203
```

<br>

**8. 모듈**

기능별로 파일을 나눠서 관리하고, 필요한 곳에서 `import`해서 재사용하는 방법을 익혔다.

```bash
!mkdir common
```

```python
%%writefile common/utils.py

def add(num1: int, num2: int) -> int:
    return num1 + num2

def sub(num1: int, num2: int) -> int:
    return num1 - num2
> Writing common/utils.py
```

만든 파일 불러오기

```python
from common.utils import add, sub

add(1, 3)
sub(3, 7)
> 4
> -4
```

주피터에서는 파일을 수정한 뒤에는 커널을 재시작해야 변경 사항이 반영된다 (모듈은 최초 import 시 캐싱됨).

main 파일 만들기

```python
from common.ai.ml import get_model
from common.samples import get_happy
from common.utils import add, sub

def main():
    print(f"model name : {get_model()}")

if __name__ == "__main__":
    main()
```

```bash
python app.py
> model name : Qwen Model
```

**🤔💭 KPT**

👍Keep
enum, 클래스, 상속, 접근 지정자, 데코레이터, 매직 메서드, 싱글톤, 모듈 등 다양한 개념을 코드와 함께 학습했다. 단순히 코드를 따라 작성하는 것보다 각 기능이 어떻게 동작하는지 이해하려고 노력했다.

😂Problem
아직 함수 부분을 공부하고 있는 단계라 함수의 기본 개념이 완전히 익숙하지 않은 상태에서 클래스와 객체지향 개념까지 배우면서 다소 어렵게 느껴졌다. self, __init__, __new__처럼 기존에 사용하던 함수와 다른 형태의 개념을 이해하는 데 시간이 필요했다.

🔥Try
먼저 함수의 기본 개념과 사용법을 확실하게 익힌 후 클래스와 메서드의 관계를 연결해서 이해할 예정이다.오늘 배운 클래스와 객체지향 개념은 간단한 예제를 반복해서 작성하면서 자연스럽게 익숙해지도록 연습할 예정이다.
