# Structured Query Language

# 목차

1. [create and choice database](#1-create-and-choice-database)
2. [create table](#2-create-table)
3. [insert data](#3-insert-data)
4. [find data](#4-find-data)
5. [find data with condition](#5-find-data-with-condition)
6. [update data](#6-update-data)
7. [delete data](#7-delete-data)
8. [sorting](#8-sorting)
9. [grouping and total](#9-grouping-and-total)
10. [JOIN](#10-join)
11. [조건 연산자](#11-조건-연산자)
12. [BETWEEN](#12-between)
13. [LIKE](#13-like)
14. [IN](#14-in)
15. [서브쿼리](#15-서브쿼리)
16. [테이블 별칭](#16-테이블-별칭)
17. [중복 행 제거](#17-중복-행-제거)
18. [NULL 값 처리](#18-null-값-처리)
19. [인덱스](#19-인덱스)
20. [쿼리 실습 1](#20-쿼리-실습-1)
21. [트랜잭션](#21-트랜잭션)
22. [쿼리 실습 2](#22-쿼리-실습-2)
23. [유저 및 권한 관리](#23-유저-및-권한-관리)
24. [집합 연산자](#24-집합-연산자)
25. [피벗 (PIVOT) 및 언피벗(UNPIVOT)](#25-피벗-pivot-및-언피벗-unpivot)
26. [LIKE 연산자와 와일드카드](#26-like-연산자와-와일드카드)
27. [CASE 문](#27-case-문)
28. [서브쿼리에서 TOP N](#28-서브쿼리에서-top-n)
29. [날짜 및 시간 함수](#29-날짜-및-시간-함수)
30. [데이터 유형 변환](#30-데이터-유형-변환)

## 1. create and choice database
```
데이터 베이스 생성:

CREATE DATABASE database_name;

데이터베이스 선택:

USE database_name;
```
## 2. create table

```
테이블 생성: CREATE TABLE table_name(
		column1 datatype,
		column2 datatype,
		...
		);
```

## 3. insert data
데이터 삽입: 

```
INSERT INTO table_name(column1, column2, ...)
VALUES (value1, value2, ...) 
```

## 4. find data
모든 데이터 조회: 
```
SELECT * FROM table_name;
```

특정 열 데이터 조회: 

```
SELECT column1, column2, ... FROM table_name;
```

## 5. find data with condition:

WHERE 절 사용: 

```
SELECT * FROM table_name
WHERE condition;
```

## 6. update data

데이터 업데이트: 

```
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE contidion;
```

## 7. delete data

데이터 삭제:

```
DELETE FROM table_name
WHERE condition;
```

## 8. sorting

오름차순 정렬: 

```
SELECT * FROM table_name
ORDER BY column_name ASC;
```

내림차순 정렬: 

```
SELECT * FROM table_name
ORDER BY column_name DESC;
```

## 9. grouping and total

그룹화: 

```
SELECT column1, COUNT(column2) FROM table_name
GROUP BY column1;
```

집계함수: 

```
SELECT AVG(column_name) FROM table_name;
```

## 10. JOIN

INNER JOIN: 

```
SELECT column1, column2, ...
FROM table1
INNER JOIN table2 ON table1.column_name = table2.column_name;
```

LEFT JOIN: 

```
SELECT column1, column2, ...
FROM table1
LEFT JOIN table2 ON table1.column_name = table2.column_name;
```

## 11. 조건 연산자:

```
=
<> !=
<
>
<=
>=
BETWEEN(특정 범위 내)
LIKE (부분 문자열 매칭)
IN (값이 목록에 포함)
```

## 12. BETWEEN

특정 범위 내의 값을 선택

```
SELECT * FROM products
WHERE price BETWEEN 500 AND 1000;
```

## 13. LIKE

부분 문자열 매칭:

```
SELECT * FROM products
WHERE product_name LIKE '%Smart';
```

## 14. IN:

목록에 값 포함 유무

```
SELECT * FROM products
WHERE price IN (300, 600);
```

## 15. 서브쿼리

단일 행 서브쿼리: 

```
SELECT column1
FROM table1
WHERE column2 = (SELECT column2 FROM table2 WHERE condition);
```

다중 행 서브쿼리:

```
SELECT column1
FROM table1
WHERE column2 IN (SELECT column2 FROM table2 WHERE condition);
```

## 16. 테이블 별칭

```
Table1 (t1)
+--------+--------+
| column1| column |
+--------+--------+
| Data1  | Value1 |
| Data2  | Value2 |
| Data3  | Value3 |
+--------+--------+
```
```
Table2 (t2)
+--------+--------+
| column2| column |
+--------+--------+
| DataA  | Value1 |
| DataB  | Value2 |
| DataC  | Value3 |
+--------+--------+
```
테이블 별칭 사용:

```
SELECT t1.column1, t2.column2
FROM tables AS t1
JOIN tables2 AS t2 ON t1.column = t2.column;
```

```
Result
+--------+--------+
| column1| column2|
+--------+--------+
| Data1  | DataA  |
| Data2  | DataB  |
| Data3  | DataC  |
+--------+--------+
```

## 17. 중복 행 제거

중복 행 제거:

```
SELECT DISTINCT column1, column2 FROM table_name;
```

## 18. NULL 값 처리

```
table_name
+--------+--------+
| column1| column2|
+--------+--------+
| Data1  | Value1 |
| Data2  | NULL   |
| Data3  | Value3 |
| Data4  | NULL   |
| Data5  | Value5 |
+--------+--------+
```

NULL 값 확인:

```
SELECT column1 FROM table_name WHERE column2 IS  NULL;
```

```
Result
+--------+
| column1|
+--------+
| Data2  |
| Data4  |
+--------+
```

NULL 값 대체:

```
SELECT column1, COALESCE(column2, 'N/A') AS column2_alias FROM table_name;
```

```
Result
+--------+-------------+
| column1| column2_alias|
+--------+-------------+
| Data1  | Value1      |
| Data2  | N/A         |
| Data3  | Value3      |
| Data4  | N/A         |
| Data5  | Value5      |
+--------+-------------+
```

## 19. 인덱스

인덱스 생성:

```
CREATE INDEX index_name ON table_name (column1, column2,...)
```

## 20. 쿼리 실습 1

```
products
+-----------+--------------+-------------+-------+
| product_id| product_name | category_id | price |
+-----------+--------------+-------------+-------+
| 1         | Laptop       | 1           | 800   |
| 2         | Smartphone   | 2           | 500   |
| 3         | Tablet       | 1           | 300   |
+-----------+--------------+-------------+-------+
```

```
categories
+-------------+------------------+
| category_id | category_name    |
+-------------+------------------+
| 1           | Electronics      |
| 2           | Mobile Devices    |
| 3           | Home Appliances   |
+-------------+------------------+
```

```
SELECT products.*, categories.category_name
FROM products
JOIN categories ON products.category_id = categories.category_id
WHERE products.category_id = 1;
```
```
+-----------+--------------+-------------+-------+------------------+
| product_id| product_name | category_id | price | category_name    |
+-----------+--------------+-------------+-------+------------------+
| 1         | Laptop       | 1           | 800   | Electronics      |
| 3         | Tablet       | 1           | 300   | Electronics      |
+-----------+--------------+-------------+-------+------------------+
```
## 21. 트랜잭션: 

트랜잭션 시작:

```
START TRANSACTION;
```

트랜잭션 커밋:

```
COMMIT;
```

트랜잭션 롤백:

```
ROLLBACK;
```

22. 쿼리 실습 2

```
users
+---------+----------+
| user_id | username |
+---------+----------+
| 1       | user1    |
| 2       | user2    |
+---------+----------+
```

```
account
+---------+---------+
| user_id | balance |
+---------+---------+
| 1       | 500     |
| 2       | 800     |
+---------+---------+
```

```
-- 트랜잭션 시작
START TRANSACTION;

-- 사용자 계정에서 100만큼 돈 인출
UPDATE account SET balance = balance - 100 WHERE user_id = 1;

-- 사용자 정보 갱신
UPDATE users SET username = 'newuser1' WHERE user_id = 1;

-- 트랜잭션 커밋
COMMIT;
```

```
-- 트랜잭션 시작
START TRANSACTION;

-- 사용자 계정에서 100만큼 돈 인출
UPDATE account SET balance = balance - 100 WHERE user_id = 1;

-- 사용자 정보 갱신 (여기서 에러 발생)

-- 트랜잭션 롤백
ROLLBACK;
```

## 23. 유저 및 권한 관리

유저 생성:

```
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
```

권한 부여:

```
GRANT SELECT, INSERT ON database_name.table_name TO 'username'@'localhost';
```

권한 취소:

```
REVOKE SELECT ON database_name.table_name FROM 'username'@'localhost';
```

## 24. 집합 연산자

```
table1
+--------+
| column1|
+--------+
| Data1  |
| Data2  |
| Data3  |
```

```
table2
+--------+
| column1|
+--------+
| Data2  |
| Data3  |
| Data4  |
```

```
UNION(중복 행 제거)
SELECT column1 FROM table1
UNION
SELECT column1 FROM table2;
```

```
+--------+
| column1|
+--------+
| Data1  |
| Data2  |
| Data3  |
| Data4  |
```
```
UNION ALL(중복 행 포함)
SELECT column1 FROM table1
UNION ALL
SELECT column1 FROM table2;
```
```
+--------+
| column1|
+--------+
| Data1  |
| Data2  |
| Data3  |
| Data2  |
| Data3  |
| Data4  |
```

## 25. 피벗 (PIVOT) 및 언피벗(UNPIVOT)

```
| category | value |
|----------|-------|
| A        | 10    |
| B        | 20    |
| C        | 30    |
```

```
PIVOT:
SELECT *
FROM(
	SELECT category, value FROM table_name
) AS SourceTable
PIVOT(
	SUM(value) FOR category IN ([Category1], [Category2], [Category3])
) As PivotTable;
```

```
| A  | B  | C  |
|----|----|----|
| 10 | 20 | 30 |

```
```
UNPIVOT:
SELECT category, value
FROM (
	SELECT [Category1], [Category2], [Category3] FROM table_name
) AS SourceTable
UNPIVOT(
	value FOR category IN ([Category1], [Category2], [Category3])
) AS UnpivotedTable;
```
```
| category | value |
|----------|-------|
| A        | 10    |
| B        | 20    |
| C        | 30    |
```

## 26. LIKE 연산자와 와일드카드:

와일드카드 사용:

```
-- '%'는 0개 이상 문자와 매치
SELECT * FROM table_name WHERE column1 LIKE 'pattern%';
-- '_'는 정확히 1개의 문자와 매치
SELECT * FROM table_name WHERE column1 LIKE 'a_';
```

## 27. CASE 문


CASE 문 사용:

```
SELECT column1,
	CASE
		WHEN condition1 THEN 'Value1'
		WHEN condition2 THEN 'Value2'
		ELSE 'DefaultValue'
	END AS new_column
FROM table_name;
```

## 28. 서브쿼리에서 TOP N

서브쿼리에서 TOP N:

```
| column1 | column2 |
|----------|----------|
| A        | Data1    |
| B        | Data2    |
| C        | Data3    |
| D        | Data4    |
| E        | Data5    |
```

```
| column1 | column3 |
|----------|---------|
| A        | 10      |
| B        | 15      |
| C        | 5       |
| D        | 20      |
| E        | 12      |
```

```
SELECT column1, column2
FROM table_name
WHERE column1 IN (SELECT TOP 5 column1 FROM another_table ORDER BY column3 DESC);
```
```
| column1 | column2 |
|----------|----------|
| D        | Data4    |
| A        | Data1    |
| B        | Data2    |
| E        | Data5    |
| C        | Data3    |
```
## 29. 날짜 및 시간 함수

현재 날짜 및 시간:

```
SELECT CURRENT_DATE, CURRENT_TIME, CURRENT_TIMESTAMP;(날짜, 시간, 날짜와 시간)
```

날짜 및 시간 연산:

```
SELECT column1, column2, column3 + INTERVAL 7 DAY AS new_data
FROM table_name;
```

## 30. 데이터 유형 변환

데이터 유형 변환:
```
SELECT CAST(column1 AS VARCHAR(255)) AS new_column
FROM table_name;
```

