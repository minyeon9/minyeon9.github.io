---
layout: single
title: "다형성(Polymorphism)"
categories: ['Java']
---
   
#### 다형성(Polymorphism) 
여러가지 타입의 자식 객체를 부모클래스 타입 하나로 다룰 수 있는 기술.   
( == 조상 타입의 참조 변수로 자손 타입 객체를 다루는 것.)   
   
***   
#### 클래스 형 변환
* 반드시 상속 관계에 있는 클래스 사이에서만 형 변환 가능
* 형제 관계의 클래스는 형 변환 불가
* Up Casting
    * 부모 타입의 참조형 변수가 모든 자식 타입의 객체 주소를 받을 수 있음
* Down Casting
    * 자식 객체의 주소를 받는 부모 참조형 변수를 가지고 자식의 멤버를 참조
    * 강제 형 변환 필요   
   
***
#### instanceof 연산자
* 어떤 객체를 참조하고 있는지 확인할 때 사용하는 연산자
    * 클래스 타입이 맞으면 true, 아니면 false 반환   
   
``` java
class Fruit {}
class Apple extends Fruit {}

public class InstansofTest {
	public static void main(String[] args) {
		Fruit fruit = new Fruit();
		Apple apple = new Apple();
		
		System.out.println(apple instanceof Fruit); // true
	}
}
```   
   
***
#### 객체 배열과 다형성
* 다형성을 이용하여 상속 관계에 있는 부모클래스 타입에 여러 종류의 자식 객체 저장   
   
``` java
Car[] carArr = new Car[3];

carArr[0] = new Sonata();
carArr[1] = new Avante();
carArr[2] = new Grandure();

// Car[] carArr = { new Sonata(), new Avante(), new Grandure() };
```   
   
***
#### 매개변수와 다형성
* 메서드 호출 시 부모 타입의 변수 하나만 사용하여 자식 타입의 객체를 받을 수 있음    
   
***
#### 바인딩
* 실행할 메서드 코드와 호출하는 코드를 연결
* 정적 바인딩
    * 컴파일링 또는 링크 시에 확정
    * 실행 이전에 값이 확정
    * static으로 선언 된 것   
* 동적 바인딩
    * 컴파일 시 바인딩된 메서드를 실행할 당시의 객체 타입을 기준으로 바인딩 되는 것
    * 정적으로 바인딩 된 메서드보다 오버라이딩 된 메서드를 우선적으로 실행
    * 실행 이후에 값이 확정   
   
***