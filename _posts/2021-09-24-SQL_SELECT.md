---
layout: single
title: "SQL - SELECT"
categoreis: ['Programming', 'Oracle']
---
   
#### SQL
* Structured Query Language
* 관계형 데이터베이스에서 데이터를 조회하거나 조작하기 위해 사용하는 표준 검색 언어
* 원하는 데이터를 찾는 방법이나 절차를 기술하는 것이 아닌 조건을 기술하여 작성   
   
|분류|용도|명령어|
|------|---|---|
|DQL(Data Query Language)|데이터 검색|SELECT|
|DML(Data Manipulation Language)|데이터 조작|INSERT, UPDATE, DELETE|
|DDL(Data Definition Language)|데이터 정의|CREATE, DROP, ALTER|
|TCL(Transaction Control Language)|트랜젝션 제어|COMMIT, ROLLBACK|   
   
***

#### SELECT
* 데이터 조회
* SELECT 구문을 통해 반환된 행 : Result set   
   
``` SQL
SELECT 컬럼명, 컬럼명, ..., 컬럼명
FROM 테이블명;
WHERE 조건식;
```
![Alt text](/assets/images/oracle09.jpg)   
   
* SELECT : 조회하고자하는 컬럼명. 다중 컬럼 조회 시 쉼표로 구분. 마지막 컬럼은 쉼표 생략.
* FROM : 조회 컬림이 포함된 테이블명.
* WHERE : 조회 조건 기술. 여러 개의 조건 포함 가능. 제한 조건은 논리연산자 사용.   
   
***