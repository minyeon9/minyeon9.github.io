---
layout: single
title: "SQL - Sub Query"
categoris: ['Programming', 'oracle']
---

#### SUBQUERY
* SELECT 문 안에 또 다른 SELECT 문
* 메인 쿼리(기존 쿼리)를 보조
* 메인 쿼리가 시작되기 전에 한 번만 실행
* 비교연산자의 오른쪽에 기술   
* 
   
```
SELECT 컬럼명
FROM 테이블명
WHERE 컬럼명 = (
    SELECT 컬럼명
    FROM 테이블명
    WHERE 조건
);
```   
   
![Alt text](/assets/images/subquery01.jpg)   
   
CLASS 테이블에서 '이은지' 학생과 동일한 학과에 재학 중인 학생을 조회하려고 한다.   
   
-
   
![Alt text](/assets/images/subquery02.jpg)   
   
1) 우선 '이은지' 학생의 학과를 조회했다.   
   
-
   
![Alt text](/assets/images/subquery03.jpg)   
   
2) '예체능' 학과인 것을 확인하고   
WHERE 절에 조건을 기술하여 '예체능' 학과 학생들을 조회했다.   
   
-
   
![Alt text](/assets/images/subquery04.jpg)   
   
3) WHERE 절에 '이은지' 학생의 학과를 조회했던 쿼리문을   
SUBQUERY로 사용했다. 결과는 2번 이미지와 동일하다.   
   
*** 

#### 단일행 SUBQUERY
* SUBQUERY의 조회 결과가 1개
* 비교 연산자 사용 가능 (=, !=, <>, ^=, >, <, >=, <=, ...)
   
위 예제처럼 SUBQUERY의 조회 결과가 1개일 때를 말한다.   
   
***

#### 다중행 SUBQUERY
* SUBQUERY의 조회 결과가 여러 행
* IN / NOT IN (SUBQUERY) : 여러 개의 결과값 중에서 한 개라도 일치하는 값이 있다면 혹은 없다면 TRUE를 리턴
* ANY : 여러 개의 값들 중에서 한 개라도 만족하면 TRUE, IN과 다르게 비교 연산자를 사용
    * SALARY = ANY(...) : IN과 같은 결과
    * SALARY != ANY(...) : NOT IN과 같은 결과
    * SALARY > ANY(...) : 최소값 보다 크면 TRUE 리턴
    * SALARY < ANY(...) : 최대값 보다 작으면 TRUE 리턴 
* ALL : 여러 개의 값들 모두와 비교하여 만족해야한 TRUE
    * SALARY > ALL(...) : 최대값 보다 크면 TRUE 리턴
    * SALARY < ALL(...) : 최소값 보다 작으면 TRUE 리턴
   
