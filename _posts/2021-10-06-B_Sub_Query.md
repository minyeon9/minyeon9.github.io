---
layout: single
title: "SQL - SUBQUERY"
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
   
위의 '이은지' 학생 예제처럼 SUBQUERY의 조회 결과가 1개일 때를 말한다.  
위에서는 비교연산자 중 = 기호를 사용하여 조회했다.    
   
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
   
![Alt text](/assets/images/subquery05.jpg)   
   
학과별 최고 점수를 를 조회했다.   
이미지처럼 여러 행의 결과가 조회되는 것이 **다중행 SUBQUERY**이다.   
이 쿼리문을 SUBQUERY로 이용하여 학과별 최고 점수를 받은 학생의 정보를 조회할 것이다.   
   
-
   
![Alt text](/assets/images/subquery06.jpg)   
   
IN 을 사용하여 위에서 조회했던 점수들을 조건절에 기술하여 조회했다.   
   
-
   
![Alt text](/assets/images/subquery07.jpg)   
   
점수들을 직접 기술하는 것이 아닌
1) 최고 점수를 조회하여
2) 그 쿼리문을 SUBQUERY로 사용하는 메인 쿼리를 작성했다.
   
***
   
#### 다중열 SUBQUERY
* SUBQUERY의 조회 결과가 한 행, 여러 컬럼
   
위의 '이은지' 학생과 동일한 학과생 조회를 예로 들 수 있다.   
여기서 예제는 패스.   
   
***

#### 다중행 다중열 SUBQUERY
* SUBQUERY의 조회 결과가 여러 행, 여러 컬럼

이건 학과별 최고 점수를 받은 학생의 조회 결과 예시를 확인할 것..!   
이것도 예제 패스.   
   
***

#### 인라인 뷰(INLINE VIEW)
* FROM 절에 테이블 대신 SUBQUERY를 사용
* ROWNUM : Oracle에서 제공하는 컬럼, 조회 결과에 1부터 순서 부여
   
```
SELECT 컬럼명
FROM (
    SELECT 컬럼명
    FROM 테이블명
    ORDER BY 컬럼명
)
WHERE 조건;
```   
   
학생들의 시험 점수를 높은 순으로 5개까지 조회하려 한다.   
   
![Alt text](/assets/images/subquery08.jpg)   
   
조회 결과를 보면 ROWNUM의 순서가 뒤죽박죽인 것을 볼 수 있다.   
조회 결과를 출력할 때의 순서 때문인데   
* 순서가
    * 1) FROM 
    * 2) SELECT
    * 3) WHERE 순이다.   
   
이런 문제를 해결하기 위해 인라인 뷰를 사용한다.   
   
-
   
![Alt text](/assets/images/subquery09.jpg)   
   
FROM 절에 위에서 사용했던 쿼리문을 테이블처럼 사용했다.   
FROM 절의 우선 순위가 제일 높기 때문에   
FROM 절에 쓰인 SUBQUERY를 먼저 실행하고, 그 후에 정렬을 하기 때문에   
만족하는 결과가 출력 되었다.   
   
SUBQUERY를 테이블처럼 사용하기 때문에   
메인 쿼리에서 더 많은 컬럼명을 작성하여도   
SUBQUERY에 기술된 컬럼 외에는 조회되지 않는 것도 알아둘것.   
  
***

#### WITH
* SUBQUERY에 이름을 부여하고 인라인 뷰로 사용 시, SUBQUERY의 이름으로 FROM 절에서 사용
* 같은 SUBQUERY를 여러 번 사용 시 중복 작성 방지
* 빠른 실행 속도가 장점   
   
```
WITH 별칭 AS (
    SELECT 컬럼명
    FROM 테이블명
    ORDER BY 컬럼명
)

SELECT 컬럼명
FROM 테이블명
WHERE 조건;
```   
   
![Alt text](/assets/images/subquery10.jpg)   
   
조회 결과는 동일하지만 SUBQUERY를 여러 번 작성해야할 때 사용한다.   
일종의 COMMON이라고 보면 되나..   
   
WITH가 따로 분리된 구문이 아니기때문에   
;(세미콜론)은 뒤에 붙는 것도 기억하자.     
   
***

#### RANK() OVER / DENSE_RANK() OVER
* 분석함수
* 순위 정렬
* RANK() OVER : 동일한 순위 이후의 등수를 동일한 인원수만큼 건너뛰고 순위 계산 (ex. 공동 1위가 2명일 경우 다음 순위는 3위)
* DENSE_RANK() OVER : 동일한 순위 이후의 등수는 무조건 1씩 증가 (ex. 공동 1위가 2명일 경우 다음 순위는 2위)
   
```
RANK() OVER(ORDER BY 컬럼명)

DENSE_RANK() OVER(ORDER BY 컬럼명)
```   
   
![Alt text](/assets/images/subquery11.jpg)   

CLASS 테이블에서 SCORE를 순위에 따라 정렬하여 조회하려고 한다.   
이 때 동점을 가진 학생이 2명인데   
1) RANK() OVER   
2) DENSE_RANK() OVER 두 가지를 사용하여 비교해볼 것이다.   
   
-
    
![Alt text](/assets/images/subquery12.jpg)   
   
1) RANK() OVER 사용 시, 동일한 순위의 행이 있을 경우   
동일 순위의 행 수만큼 더하여 다음 순위를 산정한다.   
   
-
   
![Alt text](/assets/images/subquery13.jpg)   

2) DENSE_RANK() OVER 사용 시, 동일한 순위의 행이 있어도
순위가 순차적으로 증가한다.   
   
***