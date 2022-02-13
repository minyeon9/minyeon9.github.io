---
layout: single
title: "Stream API - 최종 처리"
categories: ['Java']
---

#### Mathcing
* 최종 처리 단계에서 요소들이 특정 조건에 만족 여부 확인
    * true / false 리턴
* allMatch() : 모든 요소가 매개값으로 주어진 Predicate의 조건에 만족하는지
* anyMatch() : 최소 하나의 요소가 매개값으로 주어진 Predicate의 조건에 만족하는지
* nonMatch() : 모든 요소가 매가값으로 주어진 Predicate의 조건에 만족하지 않는지
   
```
int[] values = {2, 4, 6};
boolean result = false;

result = Arrays.stream(values)
        .allMatch(value -> value % 2 == 0); // 모두 만족
System.out.println(result); // true

result = Arrays.stream(values)
        .anyMatch(value -> value % 3 == 0); // 6 하나만 만족
System.out.println(result); // true

result = Arrays.stream(values)
        .noneMatch(value -> value % 4 == 0); // 만족하는 값 없음
System.out.println(result); // false
```
   
***

#### 실습 문제
```
List<Student> list = Arrays.asList(
    new Student("이원석", 20, "남자", 100, 100),
    new Student("하윤기", 18, "여자", 90, 80),
    new Student("이정현", 27, "남자", 80, 70)
);
boolean result = false;
```
   
-
   
**20살 이상인 사람이 모두 남자인지 확인**
   
```
result = list.stream()
            .filter(student -> student.getAge() >= 20)
            .allMatch(student -> student.getGender().equals("남자"));
System.out.println(result); // true
```
   
-
   
**남자 중 평균이 90점 이상인 사람이 한 명 이상인지 확인**
   
```
result = list.stream()
            .filter(student -> student.getGender().equals("남자"))
            .anyMatch(student -> ((student.getMath() + student.getEnglish()) / 2) >= 90);
System.out.println(result); // true
```   
   
***

#### Aggregate
* 최종 처리 기능
* 기본 집계 : 요소의 카운팅, 합계, 평균, 최대값, 최소값 등과 같이 하나의 값으로 산출
    * count() : 개수 리턴
    * findFirst() : 첫번쨰 요소
    * max() : 최대 요소
    * min() : 최소 요소
    * average() : 평균
    * sum() : 합계
* 커스텀 집계 : 스트림에서 기본 집계 메서드 제공하지만 다양한 집계 결과물을 만들 수 있도록 reduce() 메서드를 제공
    * 매개 타입으로 XXXOperator
* Optional 클래스 : 스트림의 최종 결과 값을 저장하는 객체. 값의 존재 여부 확인, 값이 존재하지 않을 경우 디폴트 값 설정 가능한 각체
    * get(): 지정되어 있는 값을 얻을 때 사용
    * isPresent() : 값이 저장되어 있는지 확인
    * orElse() : get()과 동일하게 저장되어 있는 값을 얻을 때 사용. 값이 저장되어 있지 않을 경우 디폴트 값 설정 가능
    * ifPresent(Consumer) : 값이 저장되어 있을 경우 Consumer에서 값을 처리
   
***

#### 기본 집계
* 요소의 카운팅, 합계, 평균, 최대값, 최소값 등과 같이 하나의 값으로 산출
* count() : 개수 리턴
* sum() : 합계
* average() : 평균
* max() : 최대 요소
* min() : 최소 요소
* findFirst() : 첫번쨰 요소
   
***

**count()**
   
```
// 2의 배수의 개수
long count = Arrays.stream(values)
                    .filter(value -> value % 2 == 0)
                    .count();
System.out.println(count); // 출력 결과: 3
```
   
![Alt text](/assets/images/java/streamAPI/streamAPI02.jpg)   
   
count는 long 타입의 자료형을 반환하는 것을 확인.
   
***

**sum()**
   
```
// 2의 배수의 합
int sum = Arrays.stream(values)
                .filter(value -> value % 2 == 0).sum();
System.out.println(sum); // 출력 결과: 12
```
   
***

**average()**
   
```
// 2의 배수 평균
OptionalDouble average = Arrays.stream(values)
                                .filter(value -> value % 2 == 0)
                                .average();
System.out.println(average.getAsDouble()); // optional 사용 시 get을 이용하여 가져오기
// 출력 결과: 4.0 
```
   
***

**max()**
   
```
// 2의 배수 중 최대값
OptionalInt max = Arrays.stream(values)
                        .filter(value -> value % 2 == 0)
                        .max();
System.out.println(max.getAsInt()); // 출력 결과: 6
```
   
***

**min()**
   
```
// 2의 배수 중 최소값
OptionalInt min = Arrays.stream(values)
                        .filter(value -> value % 2 == 0)
                        .min();
System.out.println(min.getAsInt()); // 출력 결과: 2
```
   
***

**findFirst()**
   
```
// 첫번째 요소
OptionalInt findFirst = Arrays.stream(values).filter(value -> value % 2 == 0).
                                findFirst();
System.out.println(findFirst.getAsInt());
```   
   
***

#### Optional
* 스트림의 최종 결과 값을 저장하는 객체. 값의 존재 여부 확인, 값이 존재하지 않을 경우 디폴트 값 설정 가능한 각체
* get(): 지정되어 있는 값을 얻을 때 사용
* isPresent() : 값이 저장되어 있는지 확인
* orElse() : get()과 동일하게 저장되어 있는 값을 얻을 때 사용. 값이 저장되어 있지 않을 경우 디폴트 값 설정 가능
* ifPresent(Consumer) : 값이 저장되어 있을 경우 Consumer에서 값을 처리
   
***

**빈 값 처리 방법 1**
* if문 사용
   
```
// 값이 없는 빈 객체
List<Integer> values = new ArrayList<>();
// values.add(1);
// values.add(4);

OptionalDouble average = values.stream()
                                .mapToInt(value -> value.intValue()) // 객체를 일반 자료형으로 바꿈
                                .average();
System.out.println(average); // 출력 결과: OptionalDouble.empty

if(average.isPresent()) {
    System.out.println("평균: " + average.getAsDouble());
} else {
    System.out.println("데이터가 없음");
}
```   
   
값의 존재 여부 확인.   
값이 없는데 .average()를 실행시킬 경우 에러를 뱉는다. 나눌 수가 없기 때문에.   
그럴 때 OptionalDouble을 사용한다. 값이 없을 경우에 에러를 출력하지 않고   
OptionalDouble.empty를 출력한다.   
   
위에 add()를 사용하여 값을 넣어줬을 경우에는 평균값을 구해주고   
주석으로 가리고 실행시켜볼 경우에는 OptionalDouble.empty가 출력된다.   
   
***

**빈 값 처리 방법 2**
* default값 설정
   
```
double avg = values.stream()
                .mapToInt(value -> value.intValue())
                .average()
                .orElse(0.0); // 값이 있을 경우 문제가 없고, 값이 없다면 여기 설정한 값을 defualt 값으로 설정
System.out.println(avg); // 출력 0.0
```
***

**빈 값 처리 방법 3**
* 집계 값을 처리하는 Consumer 등록
   
```
List<Integer> values = new ArrayList<>();
values.add(1);
values.add(4);

values.stream()
        .mapToInt(value -> value.intValue())
        .average()
        .ifPresent(d -> System.out.println(d)); // 값이 없을 경우에는 실행되지 않는다.

// 출력 결과: 2.5
// add() 해주지 않을 경우 실행되지 않는다.
```    
   
***

#### 커스텀 집계
* 스트림에서 기본 집계 메서드 제공하지만 다양한 집계 결과물을 만들 수 있도록 reduce() 메서드를 제공
    * 매개 타입으로 XXXOperator
   
```
int[] values = {1, 2, 3, 4, 5, 6};

Arrays.stream(values)
        .reduce((left, right) -> left * right) // 집계형
        .ifPresent(value -> System.out.println(value));

// 출력 결과: 720
```   
   
정수형 2개를 입력 받아서 연산을 해준다.   
순서대로 1 * 2 = 2. 그다음엔 2 * 2 = 4.   
그다음엔 또 4 * 3 = 12. 12 * 4 = 48 ... 이런식으로 진행된다.
   
마찬가지로 값이 없을 경우에는 ifPresent()를 사용했기 때문에 실행되지 않는 것이 확인된다.
   
***

#### Collect
* 필터링 또는 매핑(타입 변환) 후 요소들을 수집하는 최종 처리 메서드인 collect() 제공
* collect() 사용 : 필요한 요소만 새로운 컬렉션으로 리턴 받기 가능
   
```
// List 사용
List<Student> students = Arrays.asList(
    new Student("이원석", 20, "남자", 100, 100),
    new Student("하윤기", 19, "여자", 90, 80),
    new Student("이정현", 24, "남자", 80, 70)
);

List<Student> maleList = students.stream()
                                .filter(student -> student.getGender().equals("남자"))
                                .collect(Collectors.toList());

maleList.stream()
        .map(student -> student.getName())
        .forEach(name -> System.out.print(name + " "));

// 출력 결과: 이원석 이정현
```
   
남자 이름만 출력.   
collect()를 사용하여 수집하고, 수집된 maleList에서 또 새로운 stream을 받아   
이름만 출력하도록 했다.    
   
-
   
```
// Set 사용
Set<Student> femaleList = students.stream()
				.filter(student -> student.getGender().equals("여자"))
				.collect(Collectors.toSet());
		
femaleList.stream()
            .map(student -> student.getName())
            .forEach(name -> System.out.print(name + " "));

// 출력 결과: 하윤기
```
   
***








