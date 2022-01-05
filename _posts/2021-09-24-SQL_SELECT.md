---
layout: single
title: "SQL DML - SELECT"
categoreis: ['Oracle']
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
* 컬럼을 가공 처리하여 조회
* SELECT 구문을 통해 반환된 행 : Result set   
   
```
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
   
```
-- EMPLOYEE 테이블의 전체 컬럼 조회
SELECT *
FROM EMPLOYEE;
```   
   
별 기호( * )를 사용하여 테이블 내의 전체 컬럼을 조회 할 수 있다.

***

#### 원하는 컬럼 조회
```
EMPLOYYE 테이블 내의 전체 사원의 사번, 이름, 급여 정보 조회
SELECT EMP_ID, EMP_NAME, SALARY
FROM EMPLOYEE;

-- 소문자 작성도 가능하지만 관례적으로 대문자 사용
-- select emp_id, emp_name, salary
-- from employee;
```   

![Alt text](/assets/images/sql_select02.jpg)   
   
***

#### 산술 연산
* 컬럼 값에 대해 산술 연산한 결과 조회   
   
```
-- EMPLOYEE 테이블의 직원명, 연봉(급여 * 12) 조회
SELECT EMP_NAME, SALARY * 12
FROM EMPLOYEE;
```   
   
![Alt text](/assets/images/sql_select03.jpg)   
   

-
   

```
-- EMPLOYEE 테이블 내의 직원명, 급여, 연봉, 보너스가 포함된 연봉(급여 + (보너스 * 급여) * 12) 조회
SELECT EMP_NAME, SALARY, SALARY * 12, (SALARY + (BONUS * SALARY)) * 12
FROM EMPLOYEE;
```   
   
![Alt text](/assets/images/sql_select04.jpg)   
   
* 산술 연산 시, NULL이 포함된 경우는 무조건 NULL로 조회가 된다.   
   
-
     

```
-- EMPLOYEE 테이블의 직원명, 입사일, 근무일수(오늘 날짜 - 입사일)
SELECT EMP_NAME, HIRE_DATE, SYSDATE - HIRE_DATE
FROM EMPLOYEE;

-- 오늘 날짜 : SYSDATE
```  

     
![Alt text](/assets/images/sql_select05.jpg)   
   
* 숫자가 아니어도 산술 연산이 가능하다.   
* 오늘 날짜 : SYSTDATE   

-

   
```
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
* 컬럼의 별칭을 지정   
   
```
SELECT 컬럼 AS 별칭
SELECT 컬럼 AS "별칭(비고)"
SELECT 컬럼 별칭
SELECT 컬럼 "별칭"
```   
   
위에서 했던 연봉 계산 후 조회했을 때의 컬럼처럼 연산이 포함되어 있거나,   
컬럼명이 복잡하거나 한 번에 알아보기 힘들 경우 컬럼에 별칭을 지정해 줄 수 있다.   
   
* 숫자 혹은 특수문자가 포함되는 경우에는 (" ") 사용   
* AS 생략 가능   
   
-


```
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
* 임의로 지정된 문자열(' ')을 SELECT 절에서 사용 시 테이블 내에 존재하는 데이터처럼 조회 가능
* Result set의 모든 행에 반복적으로 출력됨   
   
```
-- Employee 테이블의 직원번호, 직원명, 급여, 단위(원) 조회
SELECT EMP_ID, EMP_NAME, SALARY, '원' AS "단위(원)"
FROM EMPLOYEE;
```   
   
![Alt text](/assets/images/sql_select09.jpg)    
   
SELECT 절에 **단위(원)**으로 별칭을 지정한 **원**이 테이블 내에 존재하는 데이터처럼 반복 출력 되었다.   
   
***

#### DISTINT
* 컬럼의 중복 값을 한 번만 표시할 때 사용
* 셀렉트 문에서 한 번만 사용 가능   
   
```
-- EMPLOYEE 테이블의 직급 코드 조회
SELECT DISTINCT JOB_CODE
FROM EMPLOYEE;
```   
   
![Alt text](/assets/images/sql_select10.jpg)    
   
같은 직급 코드를 갖는 행은 중복이지만   
**DISTINCT**를 이용하여 여러 직급 코드를 한 번씩만 조회한다.   
   
***

#### WHERE
* 검색할 컬럼의 조건을 설정
* WHERE절을 만족하는 결과만 조회
* 연산자 사용 가능
   
```
SELECT 컬럼, 컬럼, ..., 컬럼
FROM 테이블명
WHERE 조건식;
```   
   
***
#### 비교 연산자
* 비교 결과는 논리 결과(TRUE / FALSE / NULL)로 출력
* 비교하는 컬럼의 값과 표현식이 동일한 데이터 타입일 때 가능
   
|연산자|설명|
|---|---|
|=|같다|
|> , <|크다 / 작다|
|>= , =<|크거나 같다 / 작거나 같다|
|<> , != , ^=|같지 않다|
|BETWEEN AND|특정 범위에 포함되는지 비교|
|LIKE / NOT LIKE|문자 패턴 비교|
|IS NULL / IS NOT NULL|NULL 여부 비교|
|IN / NOT IN|비교 값 목록에 포함/미포함 되는지 여부 비교|
   
   
##### 같다
```
SELECT *
FROM EMPLOYEE
WHERE DEPT_CODE = 'D9';
```   
   
![Alt text](/assets/images/sql_select11.jpg)    
   
* 동등 비교
* Java에서 ( == )를 사용했던 것과 헷갈리지 말쟈 !   
   
-

##### 같지 않다
```
-- EMPLOYEE 테이블 내에서 부서 코드가 D9가 아닌 사원의 사번, 사원명, 부서 코드 조회
SELECT EMP_ID, EMP_NAME, DEPT_CODE
FROM EMPLOYEE
WHERE DEPT_CODE <> 'D9';

-- WHERE DEPT_CODE != 'D9';
-- WHERE DEPT_CODE ^= 'D9';
```   
   
![Alt text](/assets/images/sql_select12.jpg)   
   
* 부서 코드 D9를 제외한 컬럼 조회
* 3가지 연산자 모두 사용 가능     
   
-
   
##### 크거나 같다 / 작거나 같다
```
-- EMPLOYEE 테이블 내에서 급여가 400만원 이상인 직원의 직원명, 부서 코드, 급여 조회
SELECT EMP_NAME, DEPT_CODE, SALARY
FROM EMPLOYEE
WHERE SALARY >= 4000000;
```   
   
![Alt text](/assets/images/sql_select13.jpg)     
    
-
   
```
SELECT EMP_NAME, SALARY, SALARY * 12 AS "연봉", HIRE_DATE
FROM EMPLOYEE
WHERE (SALARY * 12) >= 50000000;
```   
   
![Alt text](/assets/images/sql_select14.jpg)   
   
별칭 지정, 비교 연산자까지 사용하여 조회한 결과.   
   
##### BETWEEN AND
* 비교하려는 값의 범위를 지정
* 하한값 이상 상한값 이하인 경우 TRUE 리턴 
   
```
-- EMPLOYEE 테이블 내에서 급여 300만원 이상, 600만원 이하인 직원의 사번, 직원명, 부서 코드, 급여 조회
SELECT EMP_ID, EMP_NAME, DEPT_CODE, SALARY
FROM EMPLOYEE
WHERE SALARY BETWEEN 3500000 AND 6000000;
```   
   
![Alt text](/assets/images/sql_select18.jpg)  

급여가 300 - 600만원 사이인 직원 조회한 결과.   
지정한 값의 경계도 포함 되는 걸 볼 수 있다.   
기호로 표현하면 **3,000,000 <= SALARY => 6,000,000** 이렇게 된다.   
    
-
   
```
-- EMPLOYEE 테이블 내에서 입사일이 90/01/01 - 01/01/01 사이인 사원의 입사일 조회
SELECT EMP_NAME, HIRE_DATE
FROM EMPLOYEE
WHERE HIRE_DATE BETWEEN '90/01/01' AND '01/01/01';
```   
   
![Alt text](/assets/images/sql_select19.jpg)  
   
숫자가 아닌 데이터에도 사용이 가능하다.   
입사일 범위를 지정하고 조회한 결과이다.   
   
***

#### 논리 연산자
* 여러 개의 제한 조건 결과를 하나의 논리 값으로 반환   
   
|연산자|설명|
|---|---|
|AND|여러 조건이 동시에 TRUE일 경우에만 TRUE값 반환|
|OR|여러 조건들 중에 어느 하나의 조건만 TRUE이면 TRUE값 반환|
|NOT|조건에 대한 반대 값으로 반환(NULL 제외)|   
    
* AND : ~이고, 그리고
* OR : ~이거나, 또는   
   
-
   
**AND 연산 결과**   
   
|TRUE|FALSE|NULL|
|---|---|---|---|
|TRUE|TRUE|FALSE|NULL|
|FALSE|FALSE|FALSE|FALSE|
|NULL|NULL|FALSE|NULL|   
   
-
   
**OR 연산 결과**   
   
|TRUE|FALSE|NULL|
|---|---|---|---|
|TRUE|TRUE|TRUE|TRUE|
|FALSE|TRUE|FALSE|NULL|
|NULL|TRUE|NULL|ULL|   
   
-
   
##### AND

```
-- EMPLOYEE 테이블 내에서 부서 코드가 D6이고 급여가 300만원 이상인 직원의 사번, 직원명, 부서 코드, 급여 조회
SELECT EMP_ID, EMP_NAME, DEPT_CODE, SALARY
FROM EMPLOYEE
WHERE DEPT_CODE = 'D6' AND SALARY >= 3000000;
```   
   
![Alt text](/assets/images/sql_select15.jpg)   
   
AND 연산자를 사용하여 두 개의 조건이 모두 만족하는 컬럼만 조회.   
   
-
   
##### OR
   
```
-- EMPLOYEE 테이블 내에서 직급 코드(JOB_CODE)가 j2이거나 급여가 400만원 이상인 직원의 직급 코드, 급여 조회
SELECT JOB_CODE, SALARY
FROM EMPLOYEE
WHERE JOB_CODE = 'J2' OR SALARY >= 4000000;
```   
   
![Alt text](/assets/images/sql_select16.jpg)   
   
직급 코드가 J2 이거나 급여가 400만원 이상인 직원의 정보를 조회하기 때문에   
둘 중 하나의 조건만 만족해도 조회가 가능하다.   
   
***

#### 연결 연산자
* 여러 컬럼을 하나의 컬럼처럼 연결하거나, 컬럼과 리터럴을 연결   
   
```
-- EMPLOYEE 테이블 내에서 사번, 사원명, 급여를 연결해서 조회
SELECT EMP_ID || EMP_NAME || SALARY AS "연결연산자"
FROM EMPLOYEE;
```   
   
![Alt text](/assets/images/sql_select17.jpg)   
   
원래는 각각의 컬럼으로 정렬 되어있던 데이터들이 하나의 컬럼으로 연결되어 조회된다.   
    
***

#### LIKE
* 비교하려는 컬럼 값이 지정된 패턴에 만족할 경우 TRUE 리턴
*  패턴: & / _  와일드 카드로 사용
    * & : 0개 이상
        * WHERE 비교대상컬럼 LIKE '문자%' : '문자'로 시작하는 행 조회
        * WHERE 비교대상컬럼 LIKE '%문자' : '문자'로 끝나는 행 조회
        * WHERE 비교대상컬럼 LIKE '%문자%' : '문자'로 시작하고 '문자'로 끝나는 행 조회
    * _ : 1개
        * WHERE 비교대상컬럼 '_문자' : '문자'앞에 오는 한 글자가 있는 행 조회
        * WHERE 비교대상컬럼 '__문자' : '문자'앞에 오는 두 글자가 있는 행 조회   
    
##### 와일드 카드 &
   
```
-- EMPLOYEE 테이블 내에서 성이 전인 사원의 사원명, 급여, 입사일 조회
SELECT EMP_NAME, SALARY, HIRE_DATE
FROM EMPLOYEE
WHERE EMP_NAME LIKE '전%';
```   
   
![Alt text](/assets/images/sql_select20.jpg)   
   
사원명 중 전으로 시작하는 이름을 가진 직원을 조회했다.   
%는 원하는 글자 뒤가 몇글자인지 상관 없이 조회한다.   
   
-
   
   
```
-- EMPLOYEE 테이블 내에서 '하'가 포함된 이름을 가진 사원의 사원명, 주민번호, 부서코드 조회
SELECT EMP_NAME, EMP_NO, DEPT_CODE
FROM EMPLOYEE
WHERE EMP_NAME LIKE '%하%';
```  
   
![Alt text](/assets/images/sql_select21.jpg)    
   
%는 몇글자이든 상관이 없기 때문에 앞, 뒤의 글자수는 체크하지 않고,   
그냥 이름 중간에 '하'가 들어가 있으면 조회한다.   
   
-
   
```
-- EMPLOYEE 테이블 내에서 성이 '김'이 아닌 사원의 사번, 사원명, 입사일 조회
SELECT EMP_ID, EMP_NAME, HIRE_DATE
FROM EMPLOYEE
WHERE EMP_NAME NOT LIKE '김%';
-- WHERE NOT EMP_NAME LIKE '김%';
```   
   
![Alt text](/assets/images/sql_select24.jpg)    
   
성이 '김'이 아닌 사원 조회!
NOT만 추가해주면 되는데, 위치는 조건을 설정할 컬럼 명 앞이나 LIKE 앞에 붙이면 된다.   
   
   
##### 와일드 카드 _
   
```
-- EMPLOYEE 테이블 내에서 전화번호 중 4번째 자리가 '9'로 시작하는 사원의 사원명, 전화번호, 이메일 조회
SELECT EMP_NAME, PHONE, EMAIL
FROM EMPLOYEE
WHERE PHONE LIKE '___9%';
```   
   
![Alt text](/assets/images/sql_select22.jpg)    
   
언더바( _ )의 개수로 글자 수를 체크한다.   
결국에는 010 뒤에 오는 숫자가 9인 번호를 갖는 사원의 정보를 조회한다.   
   
9 뒤에 % 기호는 몇글자인지 체크하지 않기 때문에   
혹시나.. 예를 들어.. 010-123-4567 이런 번호 형태를 갖는 정보도 조회할 수 있다.   
   
9 뒤에 % 기호를 붙이지 않으면   
9로 끝나는 숫자의 정보를 조회한다.   
검색하려는 조건에 맞게 사용하면 되고 여기서는 필요해서 붙여주었다.   
   
-
   
##### ESCAPE 문자 포함
* 와일드카드와 데이터가 구분되지 않을 경우 사용
   
```
-- EMPLOYEE 테이블 내에서 이메일 중 '_' 앞 글자가 3자리인 사원의 사번, 사원명, 이메일 조회
SELECT EMP_ID, EMP_NAME, EMAIL
FROM EMPLOYEE
WHERE EMAIL LIKE '___\_%' ESCAPE '\';
```   
   
위 처럼 이메일에 언더바( _ )가 포함되어 있고   
언더바 앞의 글자수를 체크할 때는 와일드 카드( _ )를 사용해야하는데   
어떤 게 데이터 이고 와일드 카드인지 구분할 수 없기 때문에   
데이터에 있는 언더바( _ )를 ESCAPE 문자로 등록하여 사용한다.   
   
![Alt text](/assets/images/sql_select23.jpg)    
   
여기서는 백스페이스 뒤에 있는 언더바를 데이터로 인식하도록 ESCAPE 문자로 지정했다.
백스페이스 대신 다른 기호를 사용해도 된다.   
중요한 건 ESCAPE로 지정한 기회 뒤에 오는 문자가 데이터라는 것!   
이거 약간 설명하기 어렵..네..   
   
***
   
#### IS NULL / IS NOT NULL
* NULL 여부를 비교하는 연산자
* NULL은 비교 연산자로 비교 불가   
   
```
-- EMPLOYEE 테이블 내에서 보너스를 받지 않는 사원의 사번, 사원명, 급여 조회
SELECT EMP_ID, EMP_NAME, SALARY, BONUS
FROM EMPLOYEE
WHERE BONUS IS NULL;
```   
   
![Alt text](/assets/images/sql_select25.jpg)    
   
***

#### IN
* 일치하는 값이 있을 때 TRUE 리턴
   
```
WHERE 비교대상컬럼 IN('값', '값', ..., '값')
```   
   
-

   
```
-- EMPLOYEE 테이블 내에서 D1,D2,D3 부서원의 사원명, 부서코드, 급여 조회
SELECT EMP_NAME, DEPT_CODE, SALARY
FROM EMPLOYEE
WHERE DEPT_CODE IN('D1', 'D2', 'D3');
```   
   
![Alt text](/assets/images/sql_select26.jpg)    
   
괄호 안에 있는 조건을 만족하는 컬럼이 있는 행을 모두 조회한다.   
   
***

#### 연산자 우선 순위   
     
|우선 순위|연산자|
|---|---|
|1|산술 연산자|
|2|연결 연산자|
|3|비교 연산자|
|4|IS NULL / IS NOT NULL , LIKE , IN / NOT IN|
|5|BETWEEN AND / NOT BETWEEN AND|
|6|논리 연산자 – NOT|
|7|논리 연산자 – AND|
|8|논리연산자 – OR|   
   

***
