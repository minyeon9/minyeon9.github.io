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
FROM 테이블명
WHERE 조건식;
```
![Alt text](/assets/images/oracle09.jpg)   
   
* SELECT : 조회하고자하는 컬럼명. 다중 컬럼 조회 시 쉼표로 구분. 마지막 컬럼은 쉼표 생략.
* FROM : 조회 컬림이 포함된 테이블명.
* WHERE : 조회 조건 기술. 여러 개의 조건 포함 가능. 제한 조건은 논리연산자 사용.   
   
***

#### 전체 조회

![Alt text](/assets/images/sql_select01.jpg)   
   
이 테이블을 갖고 실습을 진행했다. 테이블 명은 EMPLOYEE 이다. 
테이블에는 여러 종류의 데이터들이 있고, SELECT를 이용하여 원하는 정보를 조회했다.   
   
``` SQL
-- EMPLOYEE 테이블의 전체 컬럼 조회
SELECT *
FROM EMPLOYEE;
```   
   
별 기호( * )를 사용하여 테이블 내의 전체 컬럼을 조회 할 수 있다.

***

#### 원하는 컬럼 조회
``` SQL
EMPLOYYE 테이블 내의 전체 사원의 사번, 이름, 급여 정보 조회
SELECT EMP_ID, EMP_NAME, SALARY
FROM EMPLOYEE;

-- 소문자 작성도 가능하지만 관례적으로 대문자 사용
-- select emp_id, emp_name, salary
-- from employee;
```   

![Alt text](/assets/images/sql_select02.jpg)   
   

#### 산술 연산
``` SQL
-- EMPLOYEE 테이블의 직원명, 연봉(급여 * 12) 조회
SELECT EMP_NAME, SALARY * 12
FROM EMPLOYEE;
```   
   
![Alt text](/assets/images/sql_select03.jpg)   
   
   
``` SQL
-- EMPLOYEE 테이블 내의 직원명, 급여, 연봉, 보너스가 포함된 연봉(급여 + (보너스 * 급여) * 12) 조회
SELECT EMP_NAME, SALARY, SALARY * 12, (SALARY + (BONUS * SALARY)) * 12
FROM EMPLOYEE;
```   
   
![Alt text](/assets/images/sql_select04.jpg)   

* 산술 연산 시, NULL이 포함된 경우는 무조건 NULL로 조회가 된다.   
      

``` SQL
-- EMPLOYEE 테이블의 직원명, 입사일, 근무일수(오늘 날짜 - 입사일)
SELECT EMP_NAME, HIRE_DATE, SYSDATE - HIRE_DATE
FROM EMPLOYEE;

-- 오늘 날짜 : SYSDATE
```   
   
![Alt text](/assets/images/sql_select05.jpg)   
   
* 숫자가 아니어도 산술 연산이 가능하다.   
* 오늘 날짜 : SYSTDATE   
   
``` SQL
SELECT EMP_NAME, HIRE_DATE, CEIL(SYSDATE - HIRE_DATE)
FROM EMPLOYEE;
```   
   
위에서 계산했을 때는 소수점 아래까지 출력 되었고,   
이번엔 소수점 아래로 올림을 하도록 작성했다.   
   
![Alt text](/assets/images/sql_select06.jpg)   
   
* FLOOR(NUMBER): 소수점 아래 버림
* CEIL(NUMBER): 소수점 아래 올림

***

#### 별칭 지정
``` SQL
SELECT 컬럼 AS 별칭
SELECT 컬럼 AS "별칭(비고)"
SELECT 컬럼 별칭
SELECT 컬럼 "별칭"
```   
   
위에서 했던 연봉 계산 후 조회했을 때의 컬럼처럼 연산이 포함되어 있거나,   
컬럼명이 복잡하거나 한 번에 알아보기 힘들 경우 컬럼에 별칭을 지정해 줄 수 있다.   
   
* 숫자 호 ㄱ은 특수문자가 포함되는 경우에는 (" ") 사용
* AS 생략 가능
   
``` SQL
-- Employee 테이블의 직원명, 급여, 연봉, 보너스가 포함된 연봉(급여 + (보너스 * 급여) * 12) 조회
SELECT EMP_NAME AS 이름, SALARY AS "급여", SALARY*12 연봉, (SALARY + (BONUS * SALARY)) * 12 AS "총 소득(원)"
FROM EMPLOYEE;
```   
   
![Alt text](/assets/images/sql_select07.jpg)  
   
![Alt text](/assets/images/sql_select08.jpg)    
   
별칭 지정시 컬럼에 대한 정보를 한 눈에 인식하기 쉽다.   
특스문자 포함 시에는 꼭 큰 따옴표를 넣어줄 것!   
   
***

#### 리터럴
