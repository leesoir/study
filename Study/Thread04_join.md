# Thread
## 스레드 method : join()
join() 메소드는 다른 스레드의 종료까지 해당 스레드(호출 객체)를 대기 상태로 둔다.

```java
package day25.basic;

// Thread.join
// 다른 스레드가 끝날 때까지 해당 스레드를 대기 상태로 둔다.

class MetaThread extends Thread{
	@Override
	public void run() {
		for(int i=0; i<100; i++) {
			System.out.println("스레드 실행중 ! i : " + i); 
		}
	}
}

public class Test05 {
	public static void main(String[] args) {
		MetaThread th = new MetaThread();
//		System.out.println("메인 스레드 시작!");
//		
//		th.start();
//		// MetaThread 객체 start
//		
//		System.out.println("메인 스레드 종료!");
//		
		/*
		 출력 결과를 보면 
		 메인 스레드 시작!
		 메인 스레드 종료!
		 스레드 실행중 ! i : 0
		 스레드 실행중 ! i : 1
	 	 스레드 실행중 ! i : 2
		 스레드 실행중 ! i : 3
		 스레드 실행중 ! i : 4
		 스레드 실행중 ! i : 5
		 */
		
		
		// main thread의 속도가 훨씬 빨라 동시에 시작했지만 먼저 끝이 나게 된다.
		// th가 수행을 마치면 main 스레드가 실행하게 하는 것?  
		// : Thread.join();
		
		System.out.println("---------join 사용--------");
		System.out.println("메인 스레드 시작!");
		th.start();
		try {
			th.join();
		}catch (InterruptedException e) {
			e.printStackTrace();
		}
		
		System.out.println("메인 스레드 종료!");
		// 메인 스레드 시작! ~~스레드 실행중 : ~ 메인 스레드 종료!
	}
}
```
