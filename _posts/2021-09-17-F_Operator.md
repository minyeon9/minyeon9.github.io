---
layout: single
title: "연산자(Operator)"
categories: ['Programing', 'Java']
---

#### 1. 논리 부정 연산자
* !
* 논리값(boolean)을 부정   
* true / false로 반환   
   
``` java
boolean b1 = true;
boolean b2 = false;
System.out.println(b1); // true
System.out.println(!b1); // false
System.out.println(b1); // true, 논리 연산자 사용 후에도 리터럴 누적 되지 않음.
System.out.println(b2); // false
System.out.println(!b2); // true
```
   
***
#### 2. 증감 연산자
* -- / ++
* 피 연산자 값에 1을 더하거나 빼기   
* 사용 위치에 따라 출력 값 상이   
    * 전위 연산 : 값이 참조되기 전에 연산   
    * 후위 연산 : 값이 참조된 후에 연산   
   
``` java
int a = 10;
int b = 20;
System.out.println(++a); // 11
System.out.println(b++); // 20
```   
   
위 처럼 증감 연산자의 위치에 따라 값이 달라진다.   

a = 10; 여기에 ++ 연산자를 앞에 붙여줬을 때를 '전위 연산'이라 하고,   
값이 참조되기 전에 연산되기 때문에 1을 더해 11이 출력 된다.   
   
b = 20; 이라는 변수를 선언하고 ++를 뒤에 붙일 경우 21일 출력될 것처럼 보이지만   
이처럼 값 뒤에 연산자를 붙인 '후위 연산'은 값이 참조된 후에 연산을 실행한다.   
따라서 20으로 출력이 된다.   
   
★ 짱나는 건 출력만 20이고 이제 b = 21이다.   
출력만 안 되었을 뿐 참조 후 연산이 실행되었기 때문.   

   
``` java
int a = 10;
int b = 20;
System.out.println(++a); // 11
System.out.println(b++); // 20
System.out.println(b); // 21
```   
   
***
#### 3. 산술 연산자
* (+) (-) (*) (/) (%)   
* 사칙 연산, 나누기의 나머지 값   
* 연산 방법과 우선 순위는 수학과 동일   
* (+) 더하기   
* (-) 빼기   
* (*) 곱하기   
* (/) 나누기   
* (%) 나누기의 나머지   
   
``` java
int num1 = 20;
int num2 = 10;
System.out.println(num1 + num2); // 30
System.out.println(num1 - num2); // 10
System.out.println(num1 * num2); // 200
System.out.println(num1 / num2); // 2
System.out.println(num1 % num2); // 0
```   
   
***
#### 4. 비교 연산자(관계 연산자)
* (==) (!=) (>) (>=) (<=) (<)    
* 비교 결과 값으로 논리 값 출력   
* 피 연산자로 모든 자료형 사용 가능   
* 논리 값은 비교 불가능   
* (==) 같다   
* (!=) 같지 않다   
* (>)  왼쪽 항이 오른쪽 항보다 크다   
* (>=) 왼쪽 항이 오른쪽 항보다 크거나 같다   
* (<=) 왼쪽 항이 오른쪽 항보다 작거나 같다   
* (<) 왼쪽 항이 오른쪽 항보다 작다   
   
``` java
int a = 5;
int b = 100;
System.out.println(a == b); // false
System.out.println(a != b); // true
System.out.println(a > b); // false
System.out.println(a >= b); // false
System.out.println(a <= b); // true
System.out.println(a < b); // true
```   
   
***
#### 5. 논리 연산자
* && / ll
* 논리 값을 비교   
* &&(AND) : 피 연산자 모두 true일 때 true 반환 / ll(OR) : 피 연산자 중 하나만 true여도 true 반환   
   
``` java
// &&
int a = 10;
int b = 20;
System.out.println( (a == 10) && (b == 20) ); // true && true : true
System.out.println( (a == 10) && (b == 70) ); // true && false : false
System.out.println( (a == 70) && (b == 20) ); // false && true : false
System.out.println( (a == 70) && (b == 70) ); // false && false : false
```   
   
``` java
// ||
int c = 30;
int d = 40;
System.out.println( (c == 30) || (d == 40) ); // true || true : true
System.out.println( (c == 30) || (d == 70) ); // true || false : true
System.out.println( (c == 70) || (d == 40) ); // false || true : true
System.out.println( (c == 70) || (d == 70) ); // false || false : false
```   
      
   
**번외 Short Circuit**   
* 앞 조건만 수행해도 출력값이 정해질 때 뒤의 조건은 실행하지 않는 것   
    
![Alt text](/assets/images/Operator01.png)   
&&(AND) 연산자는 피 연산자의 조건이 모두 true일 때만 true를 반환한다.   
앞에서 false가 나오는 순간 이 연산은 뒤를 볼 것도 없이 false가 출력된다.   
이때, 뒤 연산을 생략하는 것. = Short Circuit   
    
     
   
![Alt text](/assets/images/Operator02.png)   
||(OR) 연산자는 하나만 true가 되어도 만족 하기 때문에   
true 하나가 나오면 바로 연산을 만족하게 된다. 이때도 뒤 연산은 생략한다. 이게 Short Circuit !   
   
      
   
이 연산을 원하지 않을 경우는 연산자를 하나씩만 써주면 된다고 한다..!   
   
``` java
int a = 10;
int b = 20;
int c = 30;
int d = 40;
System.out.println( (a == 20) & (b == 20) ); // false & true : false
System.out.println( (c == 30) | (d == 40) ); // true | true : true
```   
   
이미 출력값은 앞에서 다 결정 되었지만, 그래도 뒤 연산을 수행한다.   
   
***
#### 6. 복합 대입 연산자
* (+=) (-=) (*=) (+=) (%=)    
* 타 연산자와 대입 연잔자의 결합   
* 자기 자신과 연산 후 연산 결과를 자기 자신에게 누적 대입   
* 메모리에서 직접 연산을 수행하기 때문에 처리 속도 증가   
   
``` java
int a = 10;
int b = 20;
int c = 30;
int d = 40;
int e = 50;
a += 5; // a = a + 5;
b -= 5; // b = b - 5;
c *= 5; // c = c * 5;
d /= 5; // d = b / 5;
e %= 5; // e = b % 5;
System.out.println(a); // 10 + 5 = 15
System.out.println(b); // 20 - 5 = 15
System.out.println(c); // 30 * 5 = 150
System.out.println(d); // 40 / 5 = 8
System.out.println(e); // 50 % 5 = 0
```
   
***
#### 7. 삼항 연산자
* 조건의 결과 값에 따라 연산 처리   
* true, false 반환   
* 중첩 가능   
   
``` java
(조건식) ? true : false ;
```   
   
조건식이 참일 때 true 영역을 실행하고, 거짓일 때 false 영역을 실행한다.   
   
      
``` java
int num = 10;
int testNum = (num == 10) ? 1 : 2;
System.out.println(testNum);
// 출력 결과 : 1
```   
   
num이 10과 같으면 1을 출력하고, 아닐 경우 2를 출력한다.   
   
   
***