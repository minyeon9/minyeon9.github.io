---
layout: single
title: "Stream API"
categories: ['Java']
---

#### Stream API
* 자바 8부터 추가된 기능
* 컬렉션(배열)의 저장 요소를 하나씩 참조하여 람다식으로 처리 가능한 반복자
* Iterator와의 비슷한 역할
    * 차이점
        * 람다식으로  처리 코드 제공
        * 내부 반복자 사용하여 병렬 처리(Thread), 중간 처리, 최종 처리 수행 가능 
            * 중간 처리: 반복, 매핑, 필터링, 정렬 등 수행 / 리턴 타입은 Stream
            * 최종 처리: 반복, 카운팅, 평균, 총합 등의 집계 처리 수행 / 리턴 타입은 기본 타입이거나 OptionalXXX
    
***

#### Stream 종류
* java.util.stream 패키지에 존재
* BaseStream 인터페이스를 부모로하여 자손 인터페이스가 상속 관계를 이루고 있음
* Stream, IntStream, LongStream, DoubleStream
   
***

#### Stream 생성 방법
* 컬렉션으로부터 Stream 얻기
* 배열로부터 Stream 얻기
* 숫자 범위로 Stream 얻기
   
***

#### 컬렉션으로부터 Stream 얻기
* 컬렉션에 stream() 메서드 사용
    * java.util.Collection.stream()
   
```
// package stream.model.vo;

public class Student {
	private String name;
	private int age;
	private String gender;
	private int math;
	private int english;
}
```
   
-
   
```
List<Student> list = Arrays.asList(
    new Student("김김김", 20, "남자", 100, 100),
    new Student("이이이", 22, "남자", 90, 80),
    new Student("박박박", 24, "남자", 80, 70)
);

// 기존 방식의 for문 사용
for (Student student : list) { // list를 student에 하나씩 대입
    System.out.println(student);
}

// Stream 사용
Stream<Student> stream = list.stream();
stream.forEach((s) -> {System.out.println(s);});

// 위에 두 줄을 줄여서 이렇게 쓸 수 있음
list.stream().forEach(s -> System.out.println(s));
```   
   
#### 배열로부터 Stream 얻기
* Array.stream(배열) 메서드 사용 또는 각 스트림(Stream, IntStream, ...)의 of() 메서드 사용
   
```
String[] names = {"김김김", "이이이", "박박박"};

Stream<String> stream = Arrays.stream(names);
// of() 메서드 사용
Stream<String> stream = Stream.of(names);

stream.forEach(s -> System.out.println(s));
```
   
***

#### 숫자 범위로 Stream 얻기
* IntStream의 range(), rangeClose() 메서드를 사용하여 첫번째 매개값부터 두번째 매개값까지, 혹은 이전까지 제공하는 Stream을 얻어올 수 있다
   
```
// 첫번째 매개값 ~ 두번째 매개값 이전까지
IntStream stream = IntStream.range(1, 10);
stream.forEach(i -> System.out.print(i + " ")); // 1 2 3 4 5 6 7 8 9

// 첫번째 매개값 ~ 두번째 매개값까지
stream = IntStream.rangeClosed(1, 10);
stream.forEach(i -> System.out.print(i + " "));
```   
   
-
   
```
// 합계 구하기
int sum = stream.peek(i -> System.out.print(i + " ")).sum();

System.out.println(sum);
```
   
forEach() / sum()은 최종처리 메서드이기 때문에   
close 되어 사용이 끝나면 다시 stream을 사용할 수 없다.   
컬렉션(배열)로부터 다시 스트림을 얻어와야한다.   
   
***

