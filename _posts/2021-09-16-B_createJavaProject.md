---
layout: single
title: "Java Project 생성"
categories: ['Programming', 'Java']
---
#### 1. eclips JAVA 설정
![Alt text](/assets/images/create_java_project01.png)   
eclipse 오른 쪽 상단에 있는 버튼[open perspective] 클릭 - java 선택   
이 버튼의 기능은 선택한 언어에 적합한 eclipse 뷰 레이아웃을 제공하는 것이다.   
우리는 java 언어를 사용하기 때문에 java로 선택했다.   
선택 하면 처음 eclipse를 열었을 때와는 조금 다른 레이웃으로 변경 된다.   
* * *
#### 2. JREs 확인
[Window] - [Preference] - 'Installed JREs' 검색 - 사용할 버전이 맞는지 확인.   
원하는 버전이 없을 경우: [Add] - [Standard VM] - 경로 선택   
* * *
#### 3. Project 생성
![Alt text](/assets/images/create_java_project02.png)   
[file] -[new] - [java project]   
1) project name 설정   
2) JRE 확인   
3) Create module-info.java file 체크 해제: 이게 뭔지 잘 모르겠어서 검색해봤는데.. 그래도 모르겠다. JDK 9 버전 이상 어쩌고 저쩌고 하는데...ㅠㅠ   

* * *

#### 4. Java 구성 순서와 구조
1) Package   
* class 묶음   
* sub package 포함 가능   
* .(dot)으로 구분   
* 소스 파일 내 첫 줄에 단 한 번만 선언   
* 일반적으로 하나의 단어로 지정   
   
2) Import   
* 사용하려는 class가 속한 package 지정 시 사용   
* import문을 사용하여 class를 불러올 때 package명 생략 가능   
* java.lang package의 class는 import문 없이 사용 가능   
*  String / Object / System 등   
   
3) Class   
* method를 포함   
* 모든 코드는 class 내에 작성   
* class가 모여 하나의 java 애플리케이션을 구성   
* class를 통해 객체를 생성   
* class명과 file명은 동일   
* 여러개의 method를 포함 가능   
* class명은 대문자로 시작(카멜케이스)   
   
4) Method   
* class의 기능을 구현하는 블럭   
* 실행 mothod(main method)   
  * public static void main(String[] args)   
  * java.exe가 class를 실행 시킬 때 가장 먼저 실행   
  * main 이름 변경 불가   
  * 모든 class에 존재할 필요는 없으나 반드시 하나의 class 내에는 존재   
* method명은 소문자로 시작(카멜케이스)   
   
***
#### 5. Class 생성
![Alt text](/assets/images/create_java_project03.png)    
[file] -[new] - [class]   
![Alt text](/assets/images/create_java_project04.png)    
src 폴더 내에 생성   
1) project 경로 확인   
2) package name 설정(대문자로 시작)   
3) class name 설정(소문자로 시작)   
4) modifiers - public 체크   
   
***
#### 6. 출력 method
* 변수 / 문자 / 숫자 / 논리 값을 출력   
* System.out.print()   
* System.out.println()   
  * 줄바꿈 처리   
   
***
#### 7. 주석(Comment)   
* 코드에 대한 설명이나 정보 작성   
* /* */ : 범위 주석   
* // : 한 줄 주석   
* /** */ : 도큐먼트 주석(javadoc.exe를 통해 API 도큐먼트 생성 시 사용)   
   
***
#### 8. 숫자 / 문자 출력 및 연산
1) 숫자   
  - 따옴표 미 사용
```java
public void printTest() {
      System.out.println(123); // 정수
      System.out.println(3.14); // 실수
}
```   
   
2) 문자
  - ' ' : 한 글자   
  - " " : 한 글자 / 문자열 / 빈 값   
```java
public void printTest() {
      System.out.println('가'); // 한 글자
      System.out.println("Hello World!"); // 문자열
}
```   
   
3) 연산
* 숫자 + 숫자   
* 숫자 + 문자(순서 변경 가능)   
* 문자 + 문자   
```java
public void printTest() {
    System.out.println(1 + 3); // 4
    System.out.println('a' + 1); // 아스키코드 값 + 1 = 98
    System.out.println("a" + 1); // 문자 a + 1 = a1
    System.out.println("Hello" + (1 + 5)); // Hello6
    System.out.println("Hello" + 1 + 5); // Hello15
    System.out.println("Hi" + " " + ""); // 공백 가능
}
```   
***
   


오늘 되게 많이 배웠구나.   
수업 때는 강사님이 하라는대로 하다보니.. 쉬웠는데,   
혼자 하다보니 막히는 부분이 많네.   
   
아직은 package / class / method도 헷갈리고,   
import문 작성하는 것도 너무 헷갈린다.   
   
정리를 해도 이렇게 헷갈리는데 안 했으면 어쩔뻔.ㅠㅠ   
    
   
내일도 정신 바짝 차리고 !!   
   
      
         
***