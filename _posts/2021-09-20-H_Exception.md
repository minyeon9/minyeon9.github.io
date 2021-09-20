---
layout: single
title: "예외 처리(Exception)"
categories: ['Programming', 'Java']
---
   
#### 예외 처리(Exception)
* 프로그램 수행 시 비정상 종료 상황 발생하는 프로그램 에러 해결   
    * 컴파일 에러
    * 런타임 에러
    * 시스템 에러
* Object 클래스의 자손
* 예외의 최상위 조상은 Exception
    * Checked Exception
        * 반드시 예외 처리 필요
    * Unchecked Exception
    
   
***
#### Runtime Exception
* 주로 프로그래머의 부주의로 인한 오류 발생   
* 예외 처리 보다는 코드를 수정해야하는 경우가 다수   
   
* ArithmeticException
    * 0으로 나누는 경우 발생
    * if문으로 나누는 수가 0인지 검사
* NullPointerException
    * Null인 참조 변수로 객체 멤버 참조 시도 시 발생
    * 객체 사용 전에 참조 변수가 null인지 확인
* NegativeArraySizeException
    * 배열 크기를 음수로 지정한 경우 발생
    * 배열 크기는 0보다 크게 지정
* ArrayIndexOutOfBoundsException
    * 배열의 index범위를 넘어서 참조하는 경우
    * 배열명.length를 사용하여 배열의 범위 확인
* ClassCastException
    * Cast 연산자 사용 시 타입 오류
    * instanceof연산자로 객체타입 확인 후 cast 연산
    
***
#### 예외 처리 방법
* try ~ catch문을 이용한 예외 처리
    * close() 선언 필수
* try ~ with ~ resource
    * close() 자동 처리
* 호출한 메서드에게 예외 처리를 위임(throws)
    * 계속 위임하면 main() 메서드에게 까지 위임하게 되고, 여기서는 Object가 처리
    
``` java
try {
    // exception 발생 가능성 코드 작성
} catch() {
    // try 구문에서 exception 발생 시 해당하는 exceptio에 대한 처리 작성. 여러 개의 exception처리가 가능하나 exception간의 상속 관계 고려
} finally {
    // exception 발생 여부와 관계 없이 꼭 처리해야 하는 코드 작성
    // 중간에 return문을 만나도 finally구문은 실행되지만 System.exit();를 만나면 무조건 프로그램 종료
}
```   
   
***
#### 예외 던지기
* Exception 처리를 호출한 메소드에게 위임
    * 메소드 선언 시 throws ExceptionName문을 추가하여 호출한 상위 메소드에게 예외 처리를 위임
    * 계속 위임하면 main()메소드까지 위임하게 되고 거기서도 처리되지 않는 경우 비정상 종료   
    
``` java
public void method1() throws Exception { // method1()을 호출한 곳에서 예외 처리 하도록 예외 던지기
    // ...
}
```   
   
***
