---
layout: single
title: "Stream API - 중간 처리"
categories: ['Java']
---

#### Filtering
* 중간 처리 기능
* 요소를 걸러내는 역할
    * distinct() : 중복 제거. Stream의 경우 Object.equals() 메서드가 true를 리턴할 경우 동일 객체로 판단
    * ilter(Predicate) : 매개값으로 전달되는 Predicate가 false를 리턴하는 요소 제거
   
***

```
List<String> names = Arrays.asList("김", "이", "박", "김", "최");
		
Stream<String> stream = names.stream();

stream.forEach(s -> System.out.print(s + " ")); // 김 이 박 김 최
```   
   
***

#### 중복 제거
* 위에 코드를 사용하여 중복 제거 하기
* distinct() 메서드 사용
   
```
List<String> names = Arrays.asList("김", "이", "박", "김", "최");
		
Stream<String> stream = names.stream();

stream.distinct().forEach(s -> System.out.print(s + " ")); // 김 이 박 최
```
   
두 개였던 '김' 중 마지막 요소가 삭제되었다.   
   
***

#### 필터링
* filter() 메서드 사용
* startWith() 메서드 사용
    * startsWith("포") : 포로 시작하는 요소 찾기
    
```
List<String> fruits = Arrays.asList("사과", "포도1", "복숭아", "포도2", "딸기");
Stream<String> stream = fruits.stream();

stream.filter(f -> f.startsWith("포")).forEach(f -> System.out.println(f));

// forEach는 최종 처리 메서드이기 때문에 다시 사용할 경우 새로 stream 받기
fruits.stream()       // 새로 stream을 받고
        .distinct()   // 중복 제거하고
        .filter(f -> f.startsWith("복")).forEach(f -> System.out.println(f));
        // 출력하기 : 복숭아
```
   
***

#### Mapping
* 중간 처리 기능
* stream의 요소를 다른 요소르 대체하는 작업
* mapXXX() : 대체될 새로운 Stream 생성
* flatMapXXX() : 하나의 요소를 복수의 요소들로 구성된 새로운 Stream 생성
* asDoubleStream() : IntStream, LongStream을 DoubleStream으로 변환하여 리턴 
* asLongStream() : IntStrema, DoubleStream을 LongStream으로 변환하여 리턴
* boxed() : int, long, double을 Integer, Long, Double로 박싱하여 Stream 생성
   
***

#### mapXXX()
* 대체될 새로운 Stream 생성
   
```
List<Student> list = Arrays.asList(
    new Student("이원석", 20, "남자", 100, 100),
    new Student("하윤기", 22, "남자", 90, 80),
    new Student("이정현", 24, "남자", 80, 70)
);
```
   
-
   
```
list.stream()
    .map(student -> student.getName()) // student를 대체하는 새로운 요소 생성(이름만 리턴하도록)
    .forEach(name -> System.out.print(name + " "));
    // 출력 결과: 이원석 하윤기 이정현
```
   
-
   
```
// 수학점수 평균 구하기
double avg = list.stream()
                .mapToInt(student -> student.getMath())
                .average()
                .getAsDouble();
System.out.println("수학점수 평균 : " + avg);
// 출력 결과: 수학점수 평균 : 90.0
```
   
***

#### flatMapXXX()
* 하나의 요소를 복수의 요소들로 구성된 새로운 Stream 생성
   
```
List<String> list = Arrays.asList("Java11 Lambda", "StreamAPI Filtering Mapping");

list.stream()
    .flatMap(str -> Arrays.stream(str.split(" "))) // 공백을 기준으로 문자열 자르기
    .forEach(str -> System.out.print(str + " "));
    // 출력 결과: Java11 Lambda StreamAPI Filtering Mapping
```
   
***

#### asDoubleStream()
* IntStream, LongStream을 DoubleStream으로 변환하여 리턴
   
```
int[] array = {1, 2, 3, 4, 5};

// asDoubleStream()
Arrays.stream(array)
        // asDoublueStream() 사용 전에 forEach() 사용 시 정수 반환
        .asDoubleStream() // 정수을 실수로 변환
        .forEach(value -> System.out.print(value + " "));
        
        // 출력 결과: 1.0 2.0 3.0 4.0 5.0 

// boxed()
Arrays.stream(array)
        .boxed()
        .forEach(value -> System.out.print(value + " "));

        // 출력 결과: 1 2 3 4 5
```   
   
*** 

#### Sorted
* 최종 처리 전, 중간 단계에서 요소를 정렬하여 최종 처리 순서 변경
* Stream<T> : 요소 객체가 Comparable을 구현하지 않을 경우 예외 발생
* IntStream, LongStream, DoubleStream : 오름차순으로만 정렬
   
![Alt text](/assets/images/java/streamAPI/streamAPI01.jpg)   
   
String 클래스를 확인해보면 Comparable 메서드가 구현되어 있다.
   
***

#### 요소가 객체일 경우의 정렬
* Comparable 구현 내용에 따라 정렬
   
```
names.stream()
    .sorted()
    // .sorted((n1, n2) -> n1.compareTo(n2))
    // .sorted(Comparator.naturalOrder())
    .forEach(name -> System.out.print(name + " "));
    // 출력 결과: 김 박 이 최

// 반대로 정렬
names.stream()
    // .sorted((n1, n2) -> n2.compareTo(n1)) // n2를 기준으로 compareTo
    .sorted(Comparator.reverseOrder())
    .forEach(name -> System.out.print(name + " "));
    // 출력 결과: 최 이 박 김
```   
   
***

#### 요소가 기본 자료형일 경우 정렬
* 기본 자료형의 Stream은 오름차순으로 정렬
   * 내림차순으로 정렬하고 싶을 경우: 객체로 생성(boxed) 후 Comparator의 reverseOrder() 사용
    
```
Arrays.stream(new int[] {5, 2, 4, 3, 1})
        .sorted()
        .forEach(value -> System.out.print(value + " "));
		// 출력 결과: 1, 2, 3, 4, 5
		
// 내림차순으로 정렬
Arrays.stream(new int[] {5, 2, 4, 3, 1})
        .boxed() // Integer 객체로 변환. Integer에도 Comparable() 메서드가 구현되어 있음
        .sorted(Comparator.reverseOrder())
        .forEach(value -> System.out.print(value + " "));
        // 출력 결과: 5, 4, 3, 2, 1

// boxed 사용하여 객체로 만든 것을 다시 정수형으로 변경하고 싶을 때
Arrays.stream(new int[] {5, 2, 4, 3, 1})
        .boxed()
        .sorted(Comparator.reverseOrder())
        .mapToInt(value -> value.intValue())
        .forEach(value -> System.out.print(value + " "));
        // 출력 결과: 5, 4, 3, 2, 1
```
   
***

#### Looping
* 요소 전체 반복
    * peek()
        * 중간 처리 단계에서 전체 요소를 반복하면서 추가 작업을 위해 사용
        * 최종 처리 메서드가 호출 되여야 동작(모든 중간 처리 메서드가 이렇게 처리됨)
    * forEach()
        * 최종 처리 단계에서 전체 요소를 반복하면서 추가 작업을 위해 사용
        * 최종 처리 메서드이기 때문에 이후에 sum()과 같은 다른 최종 처리 메서드 호출 불가
    
***

### peek()
* 중간 처리 단계에서 전체 요소를 반복하면서 추가 작업을 위해 사용
* 최종 처리 메서드가 호출 되여야 동작(모든 중간 처리 메서드가 이렇게 처리됨)
   
```
int[] values = {1, 2, 3, 4, 5};

Arrays.stream(values)
        .filter(value -> value % 2 == 0)
        .peek(value -> System.out.print(value + " "))
        .sum(); // 최종처리 필수
// 출력 결과: 2 4


// forEach()를 사용할 경우
Arrays.stream(values)
        .filter(value -> value % 2 == 0)
        .forEach(value -> System.out.print(value + " "));
        // forEach()는 반환값이 없기 때문에 최총 처리 메서드 불필요
```
   
peek(), forEach()의 차이점!
   
-
   
```
int[] values = {1, 2, 3, 4, 5};
int sum = 0;

sum = Arrays.stream(values)
            .filter(value -> value % 2 == 0)
            .peek(value -> System.out.print(value + " "))
            .sum();
System.out.println("sum: " + sum);

// 출력 결과: sum: 6
```
   
최종 처리 메서드 sum()도 같이 사용해 보기.
   
***
