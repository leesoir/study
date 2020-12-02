# Thread
## lambda Expression(람다 식)
anonymous class를 람다 식으로 줄여서 표현하는 것이 가능하다.
```java
package day26.basic;

public class Test01 {
	public static void main(String[] args) {
		// anonymous class -> lambda expression(람다식)으로 줄여서 표현 가능하다.
		
		
		//normal anonymous class
		Thread t = new Thread(new Runnable() {
			
			@Override
			public void run() {
				// 스레드가 할 일 .. 
				System.out.println("1");
				System.out.println("2");
				System.out.println("3");
			}
		});
		
		
		// lambda expression
		Thread t2 = new Thread(()->{
			// 실제로 run의 내용만 쓰기
			// JavaScript 화살표 함수랑 비슷한듯 : 소괄호에는 매개변수, {} 안에는 함수 내용
			// override할 method가 하나라면 해당 표현처럼 사용할 수 있다.
			// lambda expreesion JDK 1.8부터 사용 가능하다.
			System.out.println("1");
			System.out.println("2");
			System.out.println("3");
		});
		// new Runnable(){ 의 내용을 간단하게 바꿔준다 }
	}

}
```
