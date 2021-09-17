---
layout: single
title: "변수(Variable)"
categories: ['Programming', 'Java']
---

#### 1. 변수(Variable)란   
메모리(RAM)에 값(Data)을 저장하기 위한 공간

1) 기본형   
[!Alt] (/assets/images/variable01.png)   
   
2) 참조형   
* String   
* 첫 글자는 대문자로   
* new 연산자를 사용하지 않고 객체를 생성할 수 있는 유일한 자료형(new: 객체 생성 연산자)   
   
* * *

#### 2. 자료형   
* 변수 사용 전, 값을 저장   
* 저장하는 값과 할당 받을 메모리의 크기에 따라 선택   
⭐지역변수(method 내 변수, local 변수)는 반드시 초기화 필요(값 할당)   
   
1) 논리형   
* true / false   
   

2) 문자열   
* 단어나 문장   
* " "   
* 보통 String 객체를 이용   
* char 빈 값 저장 불가   
* 공백 저장 필요 시 \u0000 추가(유니코드 형태의 빈 값)   
   
3) 정수형   
* 리터럴이 int 형태로 컴파일   
* long의 리터럴은 맨 뒤에 L(or 소문자) 입력 필수   
    * int 형태로 컴파일 되기 때문에 int 범위를 넘을 경우 에러 발생   
    
4) 실수형   
* double 형태로 컴파일   
* float 리터럴 맨 뒤에 F(or 소문자) 입력 필요   
* double은 리터럴 뒤 D 입력 여부 무관   
   
* * *
#### 3. 변수 명명 규칙   
* 대소문자 구분    
* 숫자로 시작 불가   
* 자료형이 달라도 중복 변수명 사용 불가   
* 특수문자는 _(under bar) / $ (dollar)만 사용 가능   
* 예약어 사용 불가   
    * package, int, break, case, false, void 등   
   
* * *
#### 4. 상수(Constant)
* 수학에서는 변하지 않는 값   
* final 키워드 사용   
* 선언과 동시에 초기화   
* 변수명은 모두 대문자   
* 초기화 이후, 다른 데이터 대입 불가   
* ex) final int AGE; > final 자료형 변수명(대문자);   
``` java
    final int AGE;
```   
   
* * *
#### 5. 데이터 저장 단위비트(Bit)
* 비트(Bit)
* 저장 최소 단위   
    * 2진수 값 하나(0, 1)를 저장하는 메모리 공간   
* 바이트(Byte)   
    * 데이터 처리 또는 문자의 최소 단위   
    * 8개의 bit가 모여 1개의 byte   
       
* * *
#### 6. 대입
* 대입   
    * age = 32;   
* 리터럴(값)   
    * age = 32;   
       
* * *
#### 6. 자료형 범위 값 확인 방법
``` java
	System.out.println("byte : " + Byte.MIN_VALUE + " ~ " + Byte.MAX_VALUE);
    System.out.println("short : " + Short.MIN_VALUE + " ~ " + Short.MAX_VALUE);
    System.out.println("int : " + Integer.MIN_VALUE + " ~ " + Integer.MAX_VALUE);
    System.out.println("long : " + Long.MIN_VALUE + " ~ " + Long.MAX_VALUE);
    System.out.println("float : " + Float.MIN_VALUE + " ~ " + Float.MAX_VALUE);
    System.out.println("double : " + Double.MIN_VALUE + " ~ " + Double.MAX_VALUE);
    System.out.println("char : " + (int)Character.MIN_VALUE + " ~ " + (int)Character.MAX_VALUE);
```   