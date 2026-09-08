---
type: source
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY-2-26.08.07"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY2 (26.08.07)"
source_id: a37e8aca-b64e-44b9-94ae-acb319174251
source_author: doldolkoong
source_published: 2026-08-07
source_updated: 2026-09-01
archived: 2026-09-08
tags:
  - velog-source
---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY2 (26.08.07)

[Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY-2-26.08.07) · [[DAY2 - Git과 Python 가상환경 및 변수|DAY2 - Git과 Python 가상환경 및 변수]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY 2 (26.08.07)


**📖 DAY2**

오늘은 어제 설치한 개발 환경을 바탕으로 Git과 GitHub의 핵심 개념, 브랜치 전략을 이론적으로 정리하고, Python 가상환경을 pip와 uv 두 가지 방식으로 직접 구축해보는 실습을 진행했다. 마지막으로는 파이썬 기초 문법 중 변수와 상수 개념까지 학습을 이어갔다.
　
 　　
   　
    

**📖오늘 학습 내용**
>1. 복기 (환경 재확인)
2. GitHub 보안 설정
3. Git 핵심 개념
4. 브랜치 전략
5. Python 가상환경 구축 (pip / uv)
6. 실습 문제
7. 파이썬 기초 - 변수와 상수

　
 　　　
#### **1. 🔁 복기 (환경 재확인)**

수업을 시작하기 전, 어제 설치한 Python과 uv가 정상적으로 동작하는지 버전을 확인하며 복습했다.

* 파이썬 버전 확인
``` bash
PS C:\Users\Administrator> python --version
Python 3.13.15
```

* uv 버전 확인

```bash
PS C:\Users\Administrator> uv --version
uv 0.12.2 (46ead6098 2026-08-05 x86_64-pc-windows-msvc)
uv로 관리되고 있는 실제 설치 파이썬 버전 목록 확인
powershell
PS C:\Users\Administrator> uv python list
cpython-3.13.15-windows-x86_64-none   AppData\Local\Programs\Python\Python313\python.exe
cpython-3.12.13-windows-x86_64-none   AppData\Roaming\uv\python\cpython-3.12.13-windows-x86_64-none\python.exe
...
```


#### **2. 🔒 GitHub 보안 설정**

계정 보안 강화를 위해 GitHub의 **Two-factor authentication(2단계 인증)**을 설정했다. 늘 2단계 인증 설정을 안 하고 지내왔는데 협업 시 저장소 접근 권한이 걸려있는 만큼, 계정 탈취를 방지하기 위한 기본적인 보안 조치라는 것을 알 수 있었다.


　
 　　　
    　
     
#### **3. 🌱 Git 핵심 개념**

Git 저장소는 크게 세 가지 영역으로 구성된다는 것을 정리했다.

>- working directory : 실제로 코드를 작성하는 로컬 작업 폴더
- staging area : 영구적으로 저장할 파일과 하지 않을 파일을 구분해두는 임시 공간
- .git directory (repository) : commit 되어 staging area에 올라간 파일만 영구적으로 저장하는 공간. working directory에만 있는 파일은 영구 저장되지 않는다.


코드는 총 세 군데에 복제된다.


>working directory → staging area → .git repository(로컬) → github repository(허브)

origin이 붙으면 GitHub 같은 hub repository를 의미하고, 붙지 않으면 로컬의 .git repository를 의미한다.
커밋 그래프에서 점 하나하나가 하나의 커밋을 의미한다.
아래쪽 화살표는 로컬 Git 기준 커밋 수, 위쪽 화살표는 허브(원격) 기준 커밋 수를 나타낸다.
push = upload (밀다) / pull = download (당기다)

<실습 화면>
![](https://velog.velcdn.com/images/doldolkoong/post/254d9645-639d-4b5a-a4af-eb35f58fcde3/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/d0583eb2-804f-473c-b48f-c2ece119a2d0/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/acfbd1ed-a79f-4d53-883a-9bba7ee4f4aa/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/8f7aa6f0-5590-457b-9331-d67bcd96d030/image.png)
![](https://velog.velcdn.com/images/doldolkoong/post/83907f33-b8cc-4784-97e3-b470112325fe/image.png)


　
 　
  　
   
#### **4. 🌿 브랜치 전략**

대표적인 브랜치 전략 5가지를 정리했다.

>- main	:서비스를 직접 배포하는 브랜치. 함부로 손대면 안 되며, 완벽하게 검증된 코드만 들어간다.
- feature : 기능 개발용 브랜치 (예: feature/login). 최소 하나 이상 존재하며, 무조건 develop에서 분기하고 develop에 다시 머지해야 한다.
- develop :	feature에서 개발된 내용이 모이는 브랜치. 모든 기능이 합쳐졌을 때 이상이 없어야 하며, 여기서 직접 기능 개발을 하면 안 된다. 무조건 main에서 분기해야 한다.
- release : 고객에게 보여지기 전, 실제 운영 데이터로 미리 테스트해보는 브랜치 (stage 브랜치라고도 함).
- hotfix : 배포 후 치명적인 오류가 발생했을 때 최소한의 범위만 수정하기 위한 브랜치.

랜치 생성 및 흐름은 다음과 같이 정리했다.

>main → develop → feature → develop → release (release 단계에서 오류가 발생하면 다시 develop으로, 문제 없으면 main으로)

새 브랜치를 만들 때는 create new branch from 기준이 되는 브랜치를 명확히 지정해야 한다. feature 브랜치는 먼저 hub(원격)에 올라간 뒤, develop과 머지된다. 개발이 끝난 feature 브랜치는 원칙적으로 삭제하고, 최종적으로는 develop과 main만 남기는 것이 원칙이다.


　
 　
  　
   

**5. 🐍 Python 가상환경 구축 (pip / uv)**

VS Code는 프로젝트 폴더 단위로 여는 것이 원칙이며, 레포지토리 1개당 프로젝트 1개로 관리한다는 것을 전제로 실습을 진행했다.

1) pip로 가상환경 구축하기

먼저 requirements.txt에 사용할 패키지(모듈, 명령어들의 집합)와 버전을 명시해두는 방식으로 진행했다.

- 파이썬 버전 확인 후 가상환경 생성

``` bash
PS C:\dev\python\venv1> python --version
Python 3.13.15

PS C:\dev\python\venv1> py -m venv .venv
``` 

- 가상환경 실행 (scripts 폴더의 activate가 실행 키)
``` bash
PS C:\dev\python\venv1> .\.venv\Scripts\activate # 가상환경 실행
(.venv) PS C:\dev\python\venv1>
```


- pip 최신화 후 requirements.txt로 패키지 설치
``` bash
(.venv) PS C:\dev\python\venv1> python -m pip install --upgrade  pip # pip 최신 버전으로 설치
Requirement already satisfied: pip in .\.venv\Lib\site-packages (26.2.1)

(.venv) PS C:\dev\python\venv1> pip install -r .\requirements.txt

Collecting jupyter (from -r .\requirements.txt (line 4))
Collecting pandas (from -r .\requirements.txt (line 5))
Collecting seaborn (from -r .\requirements.txt (line 6))
``` 


2) uv로 가상환경 구축하기 (CRUD로 정리)

**Create**

프로젝트를 초기화할 때 이름 앞에 - _ . 같은 특수문자를 쓰면 오류가 발생한다는 점이 인상 깊었다.

``` bash
PS C:\dev\python\venv2> uv init --name venv-uv --python 3.12
Initialized project `venv-uv` at `C:\dev\python\venv2\venv`
``` 

requirements.txt로 필요한 패키지를 한 번에 추가할 수 있었다
``` bash
PS C:\dev\python\venv2> uv add -r .\requirements.txt

Using CPython 3.12.13
Creating virtual environment at: .venv
Resolved 110 packages in 814ms
Installed 107 packages in 5.32s
 + anyio==4.14.2
 + argon2-cffi==25.1.0
 + ...
 ``` 
 
패키지 제거는 uv remove로 하는데, requirements.txt 파일 자체를 넘기는 방식은 지원하지 않는다는 점을 실습 중 오류로 확인했다.
``` bash
PS C:\dev\python\venv2> uv remove .\requirements.txt
error: invalid value '.\requirements.txt' for '<PACKAGES>...':
URL requirement must be preceded by a package name.
 ``` 
 
설치가 끝나면 pyproject.toml에 jupyter, pandas, seaborn이 정상적으로 기록된 것을 확인할 수 있었다.
 
**Read**

test.py 파일을 만들어 설치한 라이브러리를 불러오고 실행해봤다.
 ```  python
import pandas as pd
import seaborn as sns

print("hello world")
 ``` 
 
가상환경을 활성화한 뒤 실행 정책을 설정하고 스크립트를 실행했다.
  ```  bash
PS C:\dev\python\venv2> (Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned) ; (& c:\dev\python\venv2\.venv\Scripts\Activate.ps1)

(venv-uv) PS C:\dev\python\venv2> & c:\dev\python\venv2\.venv\Scripts\python.exe c:/dev/python/venv2/test.py

hello world
 ``` 
 
가상환경 안에서 실행되고 있다는 점이 핵심 포인트였다.

가상환경 나가기: deactivate 가상환경 들어가기: .\.venv\Scripts\activate

**Delete**

.venv 폴더에서 마우스 우클릭 후 delete로 간단히 삭제할 수 있었다.

- 다시 만들기 (동기화)

pyproject.toml, uv.lock, python-version 파일만 있으면 동일한 가상환경을 다시 만들 수 있다.

 ```  bash
PS C:\dev\python\venv2> uv sync
 ``` 
 
 
 　
  　
   　
    
#### **6. 📝 실습 문제**

문제 1 (제한시간 10분)

프로젝트명: python1 가상환경 이름: venv-python1 파이썬 버전: 3.13 설치 라이브러리: jupyter, pandas, seaborn

 ```  bash
PS C:\dev\python\python1> uv init --name venv-python1 --python 3.13
Initialized project `venv-python1`

PS C:\dev\python\python1> uv add -r .\requirements.txt
Using CPython 3.13.15 interpreter at: C:\Users\Administrator\AppData\Local\Programs\Python\Python313\python.exe
Creating virtual environment at: .venv
Resolved 110 packages in 162ms
Installed 107 packages in 9.02s
 ``` 
  ``` python
import pandas as pd
import seaborn as sns

print("Hello, World!")
 ``` 
 
 
문제 2

프로젝트명: python2 가상환경 이름: venv-python3 파이썬 버전: 3.12 설치 라이브러리: 생략

진행 순서: 폴더 생성 → 폴더 열기 → 터미널 접속 → uv init --name venv_python2 --python 3.12 → requirements.txt 생성(jupyter, seaborn, pandas) → uv add -r .\requirements.txt 실행 → test.py 생성(print("안녕")) → 실행

 ``` bash
PS C:\dev\python\python2> uv init --name venv_python2 --python 3.12
Initialized project `venv-python2`

PS C:\dev\python\python2> uv add -r .\requirements.txt
Using CPython 3.12.13
 ``` 
 
#### **7. 🐣 파이썬 기초 - 변수와 상수**

1) 변수
변수는 변하는 수, 상수는 변하지 않는 수라는 정의부터 시작해서 실제 코드로 차이를 확인했다.

- 변수 선언과 호출/변경
 ```  python
#변수명 = 변수 값
name = "홍길동"
name
>'홍길동'
name = "심사임당"
name
> '심사임당'
 ``` 
 
2) 상수
상수는 보통 대문자로 작성한다. 하지만 파이썬은 문법적으로 상수를 강제하지 않기 때문에, 값을 재할당해도 오류 없이 바뀌어버린다는 점이 흥미로웠다.

```  python
PI = 3.14
PI
> 3.14

PI = "홍길동"  # 값을 변경해도 오류 없이 바뀜 → 진짜 상수가 아니라는 뜻
PI
> '홍길동'
 ``` 
 
진짜 "바꿀 수 없는 값"을 만들고 싶다면 enum.Enum을 상속받아 집합 상수로 선언하면 된다는 것을 배웠다.
```  python
import enum

# enum.Enum 클래스를 상속받아 상수 선언 (집합 상수)
class RAINBOW(enum.Enum):
    RED = "빨강"
    ORANGE = "주황"
    YELLOW = "노랑"
    GREEN = "초록"
    BLUE = "파랑"
    NABY = "남색"
    PURPLE = "보라"

RAINBOW.RED          # 조회
RAINBOW.RED.value    # 상수 값 조회

RAINBOW.RED.value = "블랙"  # 값 변경 시도 → 오류 발생
 ``` 
 
> AttributeError: <enum 'Enum'> cannot set attribute 'value'
상수는 변경할 수 없다는 뜻이다.

일반 변수처럼 대문자로만 선언하는 건 "관례"일 뿐 강제력이 없지만, enum.Enum을 쓰면 실제로 값 변경 시 AttributeError가 발생해 진짜 의미의 상수를 만들 수 있다는 차이를 명확히 이해할 수 있었다.


**트러블 슈팅**

1. uv remove requirements.txt
uv remove는 파일을 삭제하는 명령이 아니기 때문에 안에 라이브러리를 작성 해놨어도 라이브러리 삭제가 안됨. uv remove는 패키지를 프로젝트 의존성에서 제거하는 명령임.

-> remove jupyter

라이브러리 하나씩 삭제해야 된다.

- 수정 전
```  bash
uv remove requirements.txt
``` 

- 수정 후
``` bash
uv remove jupyter
uv remove seaborn
uv remove pandas
``` 

2. uv 생성 할 때 파일명 앞에 .이 들어갈 수 없다.

- 수정 전
```  bash
PS C:\dev\python\venv2> uv init --name .venv-uv --python 3.12
``` 

- 수정 후
```  bash
PS C:\dev\python\venv2> uv init --name venv-uv --python 3.12
``` 

uv init --name에서 지정하는 프로젝트 이름(project name) 은 단순한 폴더명이 아니라, Python 패키지의 배포 이름(package/project name) 으로 사용되므로 .(점)으로 시작하는 이름은 허용되지 않음을 알게됨.

　
 　　
   　
    
    　
     　
      
#### **🤔💭 KPT**

**👍Keep**

Git의 브랜치 전략을 단순히 외우기보다 "왜 develop에서 직접 기능 개발을 하면 안 되는지", "왜 feature는 항상 develop에서 분기해야 하는지"처럼 각 규칙의 이유를 함께 정리하려고 한 점은 계속 유지하고 싶다.

**😂Problem**
Git 브랜치 전략(main, develop, feature)의 역할과 브랜치 생성 및 Merge 순서를 이해하는 데 어려움이 있었다. VS Code와 GitHub를 연동하여 브랜치를 생성하고 Push, Merge하는 전체 과정이 아직 익숙하지 않았다.

**🔥Try**

pip 기반 가상환경과 uv 기반 가상환경의 명령어를 표로 따로 정리해서 비교해볼 예정이다. 또한 오늘 배운 브랜치 전략을 작은 개인 프로젝트에 직접 적용해보며 익숙해지는 연습을 해봐야겠다.

　
 　
  　
#### **😊오늘 하루 한줄평**

학부생 때는 pip를 사용해 라이브러리를 하나하나 설치하고 설치하는 데만 시간을 많이 할애했었는데 uv를 사용하여 설치하니 너무 신기했다.


