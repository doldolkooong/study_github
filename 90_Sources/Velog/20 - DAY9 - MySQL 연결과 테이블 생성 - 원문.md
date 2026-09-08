---
type: source
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY9-26.08.19"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY9 (26.08.19)"
source_id: d2e28ca6-f17a-4e21-b252-b7e45dbb96d3
source_author: doldolkoong
source_published: 2026-08-20
source_updated: 2026-09-05
archived: 2026-09-08
tags:
  - velog-source
---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY9 (26.08.19)

[Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY9-26.08.19) · [[DAY9 - MySQL 연결과 테이블 생성|DAY9 - MySQL 연결과 테이블 생성]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY9 (26.08.19)

**DAY 9**

📖 오늘 학습 내용
> 1. VSCode + Docker로 MySQL 재설치
> 2. DBeaver 연결 설정 (allowPublicKeyRetrieval)
> 3. 데이터베이스/테이블 생성
> 4. 데이터 삽입 (INSERT), AUTO_INCREMENT

**1. VSCode + Docker로 MySQL 재설치**

기존 DB 컨테이너를 삭제하고 다시 설치했다.

```bash
# 기존 컨테이너 삭제
docker-compose down

# 컨테이너 다시 생성 및 실행
docker-compose up -d
```

컨테이너가 정상적으로 떴는지 `docker` 명령어로 확인한 뒤 DBeaver로 이동해서 연결을 진행했다.

**2. DBeaver 연결 설정**

New Connection > MySQL 선택 후 username, password 입력.

파일 설치 후 `Edit > Connection settings > Driver properties`에서 **allowPublicKeyRetrieval** 옵션을 설정해줘야 연결이 된다.

- `root` 계정: `root@MySQL`, 기본 DB는 `sys`
- 로컬 `urstory` 계정: `urstory@MySQL`, 기본 DB는 `examplesdb`

접속 구조: `MySQL > DB1 > 테이블 > 데이터`

**3. 테이블 생성**

MySQL은 줄바꿈을 인식하지 못하고, 세미콜론(`;`)으로 구문을 구분한다.

```sql
-- 생성된 데이터베이스 사용
use examplesdb;

-- 기존 테이블이 존재한다면 삭제
drop table if exists usertb;

-- 테이블 생성
create table usertb(
    id int not null comment '사용자 식별자',
    name varchar(10) default '없음' comment '사용자 이름',
    addr varchar(500) not null default '없음' comment '사용자 집주소'
) comment = '사용자 테이블';
```

- `varchar` → 문자열 타입
- `comment` → 컬럼/테이블에 대한 주석

```sql
-- 테이블 조회
show tables;
```

**4. 데이터 생성 및 조회**

```sql
-- 데이터 조회
select
      id
    , name
    , addr
from usertb
;

-- 데이터 추가
insert into usertb
(id, name, addr)
values
(1, '돌돌쿵', '인천 남동구'),
(2, '바보', '부산 서면')
;
```

`id`를 매번 직접 넣지 않도록 `auto_increment`와 `primary key`를 적용해서 테이블을 다시 만들었다.

```sql
create table usertb(
    id int auto_increment comment '사용자 식별자',
    name varchar(10) default '없음' comment '사용자 이름',
    addr varchar(500) not null default '없음' comment '사용자 집주소',
    primary key(id) -- 식별자 생성 (not null, unique)
) comment = '사용자 테이블';

insert into usertb
(name, addr)
values
('돌돌쿵', '인천 남동구'),
('바보', '부산 서면')
;
```

`primary key`로 지정하면 `not null` + `unique` 제약이 자동으로 적용되고, `auto_increment`로 id 값이 자동 채번된다.

🤔💭 KPT

👍Keep
- 

😂Problem
- 

🔥Try
-
