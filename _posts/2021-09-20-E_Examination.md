---
layout: single
title: "평가"
---
   
#### 평가
오늘은 시험을 봤다.   
범위는 여태까지 배운 내용까지였고,   

1교시, 2교시 나누어 보았는데   
채점도 바로 해주셔서 결과를.. 빠르게 보았다.   

클래스다이어그램 문제 아작난듯.ㅠㅠ   
      
***
1교시에는   
오류가 있는 코드를 보고, 오류의 원인과 해결 방안을 제시하는 문제였다.   
여기서 클래스다이어그램이 나왔는데, 일단 객체를 보자마자 멘붕....!!   

2교시에는 여태까지 내용을 서술형으로 작성해서 내면 되는 문제였다.   
예를 들어 삼항연산자가 무엇인지, 주어진 코드를 보고 결과값을 예측하는 정도였다.   

오늘은 객체를 조지겠다..., 어제 블로그에 정리하면서 복습하긴 했는데   
왠 초면인 애들이 주르륵... 봐도 봐도 새로운 문자들 파티.ㅠㅠ   

오늘 객체 조진다.   
   
***
문제 1) 사용자에게 문자열을 입력 받아 그 문자열의 길이를 출력하고, 입력한 문자열이 "exit"면   
본 프로그램을 종료하도록 만들고 싶다. 하지만 코드의 일부분 때문에 본 의도대로 프로그램이 제대로 돌지 않는다.   
아래의 코드를 보고 문제점이 있는 부분을 찾아 파악된 문제점을 원인(15점)에 기술하고, 각 문제점에 대한 해결 방안을 조치내용(15점)에 작성하시오.   
``` java
public class Count {
	public void count() {
		Scanner sc = new Scanner(System.in);
		
		while( false ) {
			System.out.print("문자열을 입력해주세요 : " );
			String str = sc.nextLine();
			
			if(str == "exit") {
				System.out.println("프로그램을 종료합니다.");
				break;
			} else {
				System.out.println(str.length() + "글자 입니다.");
			}
		}

        System.out.println("프로그램을 종료합니다.");
	}
}
```   
``` java
public class Count {
	public void count() {
		Scanner sc = new Scanner(System.in);
		
		while( true ) { // false -> true로 변경 : 조건식이 true일 때만 실행
			System.out.print("문자열을 입력해주세요 : " );
			String str = sc.nextLine();
			
			if(str.equals("exit")) { // equals 추가: 문자열 비교 시 equals 메서드 사용
				System.out.println("프로그램을 종료합니다.");
				break;
			} else {
				System.out.println(str.length() + "글자 입니다.");
			}
		}
	}
}
```   


