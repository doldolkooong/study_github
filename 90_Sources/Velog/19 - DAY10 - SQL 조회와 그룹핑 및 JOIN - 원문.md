---
type: source
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY10-26.08.20"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY10 (26.08.20)"
source_id: f99952bf-0ca9-414d-8130-e5b2eb837abc
source_author: doldolkoong
source_published: 2026-08-20
source_updated: 2026-09-05
archived: 2026-09-08
tags:
  - velog-source
---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY10 (26.08.20)

[Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY10-26.08.20) · [[DAY10 - SQL 조회와 그룹핑 및 JOIN|DAY10 - SQL 조회와 그룹핑 및 JOIN]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY10 26.08.20

**DAY 10**


**📖 오늘 학습 내용**
>1. DCL (Data Control Language)
2. Docker로 MySQL 접속
3. 데이터 조회 (SELECT / WHERE)
4. 정렬 (ORDER BY)
5. SQL 실행 순서
6. 그룹핑 (GROUP BY)
7. 조인 (JOIN)과 서브쿼리

**1. DCL (Data Control Language)**

로컬 호스트의 IP는 `127.0.0.1`이며, 이 매핑은 아래 호스트 파일에 정의되어 있다.

```
C:\Windows\System32\drivers\etc\hosts

# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost
```

MySQL 계정 권한을 다루는 `user` 테이블에서 `Host` 컬럼의 `%`는 이 세상 모든 IP를 의미한다. 즉 `%`로 등록된 계정은 어떤 IP에서 접속해도 허용된다는 뜻이고, `localhost`로 등록된 계정은 로컬에서만 접속할 수 있다.

```
mysql> select host, user from user;
+-----------+------------------+
| host      | user             |
+-----------+------------------+
| %         | root             |
| localhost | mysql.infoschema |
| localhost | mysql.session    |
| localhost | mysql.sys        |
| localhost | root             |
| localhost | urstory          |
+-----------+------------------+
6 rows in set (0.001 sec)
```

**2. Docker로 MySQL 접속**

```bash
sh-5.1# mysql -u root -p
Enter password:
```

`-u root`는 root 계정으로 접속하겠다는 의미이고, `-p`를 붙이면 비밀번호를 별도로 입력받는다.

```sql
use mysql;
```

`use 데이터베이스명`으로 사용할 데이터베이스를 먼저 지정해야 그 안의 테이블을 조회할 수 있다.

**3. 데이터 조회 (SELECT / WHERE)**

```sql
-- 데이터 조회하려면 데이터베이스 정의
use classicmodels;

show tables;

-- row를 기준으로 필터링
SELECT customerName, phone from customers limit 10;

-- where 사용하여 데이터 기준으로 필터링
SELECT customerName, phone, country from customers
where 1=1 and country = 'USA';

-- 여러 줄로 나눠서 사용도 가능
SELECT
	  customerName
	, phone
	, country
from customers
where 1=1
	and country = 'USA';
```

`1=1`은 항상 참(True)이 되는 조건이라, 그 뒤에 `and`로 실제 조건들을 붙여나가기 편하게 하기 위한 관용적인 표현이다. 여기서는 `country = 'USA'`인 데이터만 조회된다.

**4. 정렬 (ORDER BY)**

```sql
-- 오름차순
SELECT
	  customerName
	, phone
	, country
from customers
where 1=1
	and country = 'USA'
order by phone asc
limit 10;

-- 내림차순
SELECT
	  customerName
	, phone
	, country
	, creditLimit
from customers
where 1=1
	and country = 'USA'
order by creditLimit desc
limit 10;
```

**5. SQL 실행 순서**

```
from -> where -> order by -> group by -> select -> limit
```

작성하는 순서와 실제로 DB가 실행하는 순서가 다르다는 걸 배웠다. `from`으로 대상 테이블을 먼저 정하고, `where`로 걸러낸 뒤, 정렬/그룹핑을 거쳐 마지막에 `select`로 원하는 컬럼을 뽑아낸다.

**6. 그룹핑 (GROUP BY)**

```sql
select
	  count(orderNumber)
	, customerNumber
from orders
group by customerNumber
;

select
	  count(orderNumber) as cnt
	, customerNumber
from orders
group by customerNumber
order by cnt desc
;
```

고객 번호(`customerNumber`)별로 묶어서 각 고객이 주문을 몇 건 했는지 세어볼 수 있었다. `as`로 집계 결과에 별칭(`cnt`)을 붙이면 `order by`에서 바로 재사용할 수 있다는 게 편리했다.

**7. 조인(JOIN)과 서브쿼리**

주문이 많은 상위 3명의 고객 정보를 서브쿼리와 조인으로 뽑아봤다.

```sql
select
		t1.customerName
	,	t1.phone
	,	t1.country
	, 	t1.creditLimit
	,   t2.cnt
from customers t1
  join (
  			select
	  				count(orderNumber) as cnt
					, customerNumber
			from orders
			group by customerNumber
			order by cnt desc
			limit 3
) t2
    on t1.customerNumber = t2.customerNumber
;
```

주문 상세(`orderdetails`)에서는 수량 × 단가로 주문별 총 금액을 계산할 수 있다.

```sql
select
	  quantityOrdered * priceEach as totalPrice
	, orderNumber
from orderdetails
order by totalPrice desc
;
```

이 서브쿼리를 주문(`orders`) 테이블과 조인하면 주문별 총 금액을, 다시 `group by`로 묶으면 고객별 총 금액을 구할 수 있다.

```sql
-- 고객별 주문들의 총 금액 조회
SELECT
	  t1.customerNumber 	-- 고객 식별자
	, t1.orderNumber 		-- 주문 식별자
	, t2.totalPrice  		-- 주문별 총 금액
from orders t1
join (
	select
	  	  -- 주문별 총 금액
      	  quantityOrdered * priceEach as totalPrice
    	, orderNumber
	from orderdetails
) t2
on t1.orderNumber = t2.orderNumber
order by totalPrice desc
;

-- 고객별 총 금액 조회
SELECT
	  t1.customerNumber 	-- 고객 식별자
	, sum(t2.totalPrice) as totalPriceBycustomer	-- 고객별 총 금액
from orders t1
join (
	select
	  	  -- 주문별 총 금액
      	  quantityOrdered * priceEach as totalPrice
    	, orderNumber
	from orderdetails
) t2
on t1.orderNumber = t2.orderNumber
group by customerNumber
order by totalPriceBycustomer desc
;
```

마지막으로 여기서 구한 고객별 총 금액 상위 3명을 다시 고객 정보와 조인해서, 결제 금액이 가장 큰 고객이 누구인지까지 한 번에 뽑아봤다.

```sql
select
		t1.customerName
	,	t1.phone
	,	t1.country
	, 	t1.creditLimit
	,   t2.totalPriceBycustomer
from customers t1
  join (
  	SELECT
	  	t1.customerNumber 	-- 고객 식별자
		, sum(t2.totalPrice) as totalPriceBycustomer	-- 고객별 총 금액
	from orders t1
	join (
		select
	  	  -- 주문별 총 금액
      	  quantityOrdered * priceEach as totalPrice
    	, orderNumber
		from orderdetails
	) t2
	on t1.orderNumber = t2.orderNumber
	group by customerNumber
	order by totalPriceBycustomer desc
	limit 3
) t2
    on t1.customerNumber = t2.customerNumber
;
```

서브쿼리를 여러 단계로 겹쳐서 쓰다 보니 처음엔 헷갈렸지만, "주문별 총액 → 고객별 총액 → 상위 3명 → 고객 정보 조인" 순서로 하나씩 쌓아 올린다고 생각하니 훨씬 이해하기 쉬웠다.


