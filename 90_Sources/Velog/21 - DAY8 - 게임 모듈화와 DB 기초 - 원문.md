---
type: source
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY-8-2026.08.18"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY 8 (26.08.18)"
source_id: 050f2c7d-a6ca-42dd-8dd4-6ebf4be5dae5
source_author: doldolkoong
source_published: 2026-08-19
source_updated: 2026-09-01
archived: 2026-09-08
tags:
  - velog-source
---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY 8 (26.08.18)

[Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY-8-2026.08.18) · [[DAY8 - 게임 모듈화와 DB 기초|DAY8 - 게임 모듈화와 DB 기초]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY 8 (26.08.18)

>** 📖 오늘 학습 내용**
> 1. 묵찌빠, 가위바위보, 하나빼기 모듈로 다시 만들기
> 2. 데이터베이스 기초 (리눅스 파일 시스템, 데이터 유형, Docker, SQL, 데이터 모델링)

<br>

**1. 묵찌빠 / 가위바위보 / 하나빼기 모듈화**

기존에 만들었던 게임들을 각각 모듈(함수/파일)로 분리하여 재사용성과 가독성을 높이는 리팩토링 작업을 진행했다.

```python
# 예시 구조
# rock_paper_scissors.py
# muk_jji_ppa.py
# one_less.py
# main.py 에서 각 모듈 import 하여 실행
```

> 각 게임 로직을 독립된 모듈로 분리하면 유지보수와 테스트가 훨씬 쉬워진다.

<br>

**2. 데이터베이스**

**리눅스 파일 시스템 기초**
- 파일/폴더 이름이 `.`으로 시작하면 숨김 파일(폴더)
- `.` : 현재 폴더
- `..` : 부모 폴더
- `./.venv` → 현재 폴더의 숨김 폴더인 venv

<br>

중간에 실업급여 강의 들으러 가야 해서 못 들은 부분이 있다...


**데이터 유형**
- 정형 데이터: 엑셀 등 2차원 데이터 (표, 축 → 그래프로 시각화)
- 반정형 데이터: 이메일, XML, HTML, JSON
- 정형 데이터를 분석하고 부족한 부분은 비정형 데이터로 보완하여 분석

<br>

**Docker**
```bash
docker-compose up -d
```
- DBeaver 설치하여 DB 클라이언트로 활용

<br>

**DBMS 종류**
1. RDBMS
2. NoSQL DBMS

<br>

**ERD & 데이터 모델링**
- ERD: RDBMS에 데이터를 저장할 때 사용하는 데이터 모델링 기법

<br>

**SQL 구성**
- DDL (Data Definition Language): 테이블 정의, 수정, 삭제
- DML (Data Manipulation Language): 데이터 삽입, 조회, 수정, 삭제
- DCL (Data Control Language): 보안, 무결성, 회복 제어

<br>

**데이터 모델링 순서**
1. 요구사항 정의서 작성
   - 개요, 이해관계자, 기능적 요구사항, 비기능적 요구사항, 제약사항, 예상 결과
2. 개념적 데이터 모델링 (ERD 작성)
   - 예: 음식, 주문 횟수 등 엔티티/속성 정의

<br>


