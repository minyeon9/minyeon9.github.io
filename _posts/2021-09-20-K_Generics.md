---
layout: single
title: "제네릭스(Generics)"
categories: ['Programming', 'Java']
---
   
#### 제네릭스(Generics)
* JDK 1.5부터 제공
* 컴파일 시 타입 체크
    * 타입 체크 강화와 타입의 안정성을 향상
* 타입 변수
* 타입 변환 생략이 가능하기 때문에 간결한 코드 작성 이점   
   
``` java
ArrayList<Book> list1 = new ArrayList<Book>(); // 참조변수와 생성자의 타입이 일치 필수
ArrayList<Book> list2 = new ArrayList<>() // 생성자에 타입 변수는 생략 가능. JDK 1.7부터 제공
```   
   
``` java
ArrayList list = new ArrayList();
list add(10);
list add(20);
list add("30"); // String

Integer i = (Integer)list.get(2);
// String 30인데 Integer로 형 변환해도 컴파일러 에러 체크 누락
// 실행 시 에러 발생(ClassCastException)

System.out.println(list);
```   
   
``` java
ArrayList<Integer> list = new ArrayList();
list add(10);
list add(20);
// list add("30"); // String Error. 타입 체크 강화
list add(30); // 컴파일 시 에러 발생 > 수정

Integer i = list.get(2); // 이미 Integer 타입으로 선언했기 때문에 형 변환 생략 가능


System.out.println(list);
```   
   
위에서 컴파일러가 체크하지 못한 타입 제한을 강화하기 위해 아래 코드처럼 제네릭스 사용   
   

***
#### 타입 변수
* 클래스 작성 시 Object 타입 대신 타입 변수<E>를 선언해서 사용
* 객체 생성 시 타입 변수<E> 대신 실제 타입을 지정(대입)   
   
```java
ArrayList<E> list = new ArrayList();

// 실제 타입 대입
ArrayList<WatingList> list = new ArrayList<WatingList>();
```   
   
``` java
ArrayList<Tv> list = new ArrayList<Tv>();
list.add(new Tv());
// list.add(new Audio()); // Tv 타입 변수를 선언했기 때문에 Tv 타입의 객체만 저장 가능
```   
   
***
#### 멀티 타입 파라미터
* 두 개 이상의 파라미터 사용 가능
* 각 타입 파라미터는 콤마(,)로 구분   
   
***
#### 제네릭스 타입과 다형성
* 참조 변수와 생성자에 대입 된 타입 일치 필수   
   
``` java
List<Tv> list = new ArrayList<Tv>(); // 다형성은 가능
List<Tv> list = new LinkedList<Tv>();  // 다형성은 가능
```   
   
``` java
ArryaList<Tv> list = new ArrayList<Tv>(); // 일치
ArryaList<Product> list = new ArrayList<Tv>(); // error 불일치
```   
   
* 매개 변수의 다형성도 성립   
   
``` java
ArrayList<Product> list = newArrayList<Product>();

list.add(new Product());
list.add(new Tv()); // Tv, Audio 모두 Product의 자식 객체
list.add(new Audio());
```   
   
``` java
Product p = list.get(0);
Tv t = (Tv)list.get(1); // list.get -> Proudct 타입이기 때문에 형 변환 필요
```   
   
***
#### 제네릭스 타입의 상속과 구현
* 제네릭스 타입을 부모클래스로 사용해야할 경우 타입 파라미터는 자식 클래스에도 작성 필수   
   
``` java
public class ChildProduct<T, M> extends Product<T, M> {…}
public class ChildProduct<T, M, C> extends Product<T, M>> {…}
```   
   
***
#### 타입 제한
* extends로 대입할 수 있는 타입을 제한   
   
``` java
class FruitBox<T extends Fruit> { // Fruit의 자손만 타입으로 지정 가능
		...
}

FruitBox<Apple> appleBox = new FruitBox<Apple>(); // 가능
FruitBox<Toy> appleBox = new FruitBox<Toy>(); // 불가
```   
   
* 상위 타입은 클래스, 인터페이스 가능
* 인터페이스도 extends 키워드 사용   
   
***
#### 제네릭스의 제약
* 타입 변수에 대입은 인스턴스 별로 다르게 가능   
   
``` java
Box<Apple> appleBox = new Box<Apple>();
Box<Grape> appleBox = new Box<Grape>();
```

* static 멤버에 타입 변수 사용 불가
    * 모든 인스턴스의 공통이기 때문
* 객체, 배열 생성 시 타입 변수 사용 불가. 타입 변수로 배열 선언은 가능
    * new 연산자는 객체 타입이 확정 되어 있어야 함   
   
```java
T[] itemArr; // T 타입의 배열을 위한 참조 변수 가능

T[] toArray() {
    T[] tempArr = new T[itemArr.length]; // 제네릭스 배열 생성 불가
}
```   
   
***
#### 와일드 카드 <?>
* 하나의 참조 변수로 대입 된 타입이 다른 객체를 참조 가능(다형성 이용)
   
``` java
ArrayList<? extendes Product> list = new ArrayList<Tv>(); // Product의 자손 객체인 Tv
ArrayList<? extendes Product> list = new ArrayList<Audio>();
```   
   
    * <? extends T>  와일드 카드의 상한 제한. T와 그 자손들만 가능   
       
``` java
ArrayList<? extends Product> list1 = new ArrayList<Product>();
ArrayList<? extends Product> list2 = new ArrayList<Tv>();
ArrayList<? extends Product> list3 = new ArrayList<Audio>();
```   
   
   * <? super T>  와일드 카드의 하한 제한. T와 그 조상들만 가능   
   
```java
ArrayList<? super Tv> list4 = new ArrayList<Tv>();
ArrayList<? super Tv> list5 = new ArrayList<Product>();
// ArrayList<? super Tv> list6 = new ArrayList<Audio>(); // Audio는 Tv와 형제 관계이기 때문에 불가
```   
   
   * <?>  제한 없음. 모든 타입 가능. <? extends Object>와 동일   
      
* 메서드의 매개 변수에도 사용 가능   
``` java
public Juice method1(FruitBox<? extends Fruit> box) {
		...
}
```   
   
***
#### 제네릭스 메서드
* 제네릭스 타입이 선언 된 메서드(타입 변수는 메서드 내에서만 유효)
* 메서드를 호출할 때마다 타입 대입 필요   
   
***
#### 제네릭스 타입의 형 변환
* 제네릭스 타입과 원시 타입 간의 형 변환은 바람직 하지 않음   
   
***
#### 제네릭스 타입의 제거
* 컴파일러가 제네릭스 타입을 제거하고 필요한 곳에 형 변환 연산자를 넣음
    * 하위 호환성을 위해(안전성)   
       
***