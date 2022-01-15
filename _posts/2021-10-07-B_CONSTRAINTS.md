---
layout: single
title: "SQL - CONSTRAINTS"
categories: ['Oracle']
---

#### 제약 조건(CONSTRAINTS)
* 지정한 타입의 데이터만 저장하기 위해 테이블 작성 시, 각 컬럼에 대한 조건 설정
* 데이터 무결성 보장 목적(데이터의 정확성과 일관성을 유지)   
   
***
   
#### NOT NULL
* 특정 컬럼에 값을 저장하거나 수정할 때 NULL 값을 허용하지 않도록 제한
* 컬럼 레벨에서만 제한 가능
* 해당 컬럼에 반드시 값이 기록되어야 하는 경우 사용
* NOT NULL이 설정된 컬럼에 NULL 값이 입력될 경우 행 삽입 불가   
   
***
   
#### UNIQUE
* 중복 제한
   
***
   
#### PRIMARY KEY
* 테이블에서 한 행의 정보를 식별하기 위한 고유 식별자(Identifer) 역할
* 컬럼의 고유 식별자로 사용하기 위  NULL / 중복을 제한
* 자동으로 해당 컬럼에 NOT NULL + UNIQUE 제약 조건 설정
* 한 테이블에 한 개만 설정 가능
    * 한 개 이상의 컬럼을 묶어서 PRIMARY KEY로 제약 조건 설정 가능(복합키)   

***
   
#### FOREIGN KEY
* 참조되는 테이블의 컬럼의 값이 존재할 경우 허용
* 두 개의 테이블 연결 할 경우 사용
* 외래키 / 참조키
* 참조할 테이블의 참조할 컬럼명을 생략할 경우 PRIMARY KEY 컬럼이 자동으로 참조할 컬럼이 됨
* 참조 무결성을 위한 제약조건   
   
***
   
#### CHECK
* 저장 가능한 데이터 값의 범위나 조건을 지정하여 설정한 값만 허용   
   
***
   
#### 제약 조건 설정 방법
**1) 컬럼레벨**   
   
```
CRATE TABLE 테이블명 (
    컬럼명 자료형(크기) [CONSTRAINT 제약조건명] 제약조건,
    ...
		...
);
```   
   
**2) 테이블 레벨**   
   
```
CRATE TABLE 테이블명 (
    컬럼명 자료형(크기),
    ...
    [CONSTRAINT 제약조건명] 제약조건 (컬럼명)
);
```   
   
***

#### SUBQUERY를 이용한 테이블 생성
* SELECT 문의 조회 결과로 테이블 생성
* 컬럼명과 데이터 타입, 값이 복사 / 제약 조건은 NOT NULL만 복사
   
![Alt text](/assets/images/order_by01.jpg)  
   
-
   
![Alt text](/assets/images/order_by02.jpg)  
   
위 이미지에 있는 'CLASS' 테이블을 복사한다.   
실습을 위해서 제약조건을 추가했다.   
      
###### 1) 전체 복사
   
```
CREATE TABLE 테이블명
AS SELECT * FROM 복사할 테이블명;
```   
   
![Alt text](/assets/images/order_by03.jpg)  
   
컬럼명, 데이터 값이 복사 되었다.   
   
-
   
![Alt text](/assets/images/order_by04.jpg)  
   
데이터 타입.. 복사된 건 캡쳐를 못 했지만..   
NOT NULL 제약 조건까지 잘 복사된 걸 확인할 수 있다.   
   
***
   
###### 2) 구조만 복사
   
```
CREATE TABLE 테이블명
AS SELECT *
	 FROM 복사할 테이블명
	 WHERE 1 = 0;
```   
   
* WHERE 1 = 0;
    * 모든 컬럼에 만족하는 값이 없기 때문에 구조만 복사 됨(FALSE)

이번에는 데이터 값을 제외한 것들을 복사하는 방법이다.   
   
![Alt text](/assets/images/order_by05.jpg)  
   
전체 복사와 동일하고 WHERE절에 추가된 것만 다르다.   
조건(WHERE)에 FALSE 만 들어가면 되기 때문에   
1 = 2; 아무거나 해도 된다.   
   
***