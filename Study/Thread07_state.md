# Thread
## 스레드 상태(State)와 상태 제어
```java
package day26.basic;

class CheckStateThread extends Thread{
	private Thread target; // target thread
	
	public CheckStateThread(Thread target) {
		this.target = target;
	}
	
	@Override
	public void run() {
		while(true) {
			// target thread의 상태를 계속해서 받아온다.
			Thread.State state = target.getState();
			System.out.println("타겟 스레드 상태  :" + state);
			if(state == Thread.State.NEW) {
				target.start(); // 상태가 new이면 start()
			}
			
			if(state == Thread.State.TERMINATED) {
				break; // target thread의 상태가 종료된(terminated) 경우 상태 받아오기를 종료(break)한다.
			}
			
			try {
				Thread.sleep(1000);
			}catch(Exception e) {
				e.printStackTrace();
			}
			
		} // while
		
	} // run()
	
} // ChectStateThread class


public class Test02 {
	public static void main(String[] args) {
		// Thread의 상태(status : stat)
		/*
		 * 스레드 상태
		 * [메인 스레드]						[작업 스레드 상태]	
		 * |
		 * new 작업스레드() ----------------   NEW
		 * |								|
		 * 작업스레드.start() ---------------  실행 대기(RUNNABLE)<----
		 * |								|					 |
		 * |								|					 |
		 * ...								run() (RUNNING) ---- 일시 정지 (WAITING / TIMED_WAITING / BLOCKED)
		 * ...								|
		 * 									|
		 * 									종료 (TERMINATE)
		 * 
		 *  Thread.State.NEW  			객체 생성. start()가 호출되지 않은 상태
		 *  Thread.State.RUNNABLE		실행 대기. start()는 호출되었으나 run()이 아직 호출되지 않은 상태
		 *  Thread.State.WAITING		일시 정지.	다른 쓰레드가 통지할 때까지 기다리는 상태
		 *  Thread.State.TIMED_WAITING  일시 정지. 주어진 시간동안 기다리는 상태
		 *  Thread.State.BLOCKED		일시 정지. 사용하고자 하는 객체의 LOCK이 풀릴 때까지 기다리는 상태
		 *  Thread.State.TERMINATED		종료.		실행을 완료한 상태
		 */
		
		// 스레드의 상태 제어
		
		Thread target = new Thread(()->{
			// lambda expression으로 run() overriding
			
			for(long i=0; i<10000000000L; i++); // body가 없는 반복문 : delay를 위해
			// Runnable 상태를 육안으로 확인하기 위해 작성하였다.
			// 해당 for문은 thread 객체의 run()이 실행되야 실행되는 코드인데, 왜 Runnable로 표시될까?
			// JVM은 run()이라고 간주하나 OS는 not run()이라고 생각할 수 있다.
			// running이라는 sTate가 따로 없어서 runnable로 퉁쳐서 간주되는듯? (2)
			
			try {
				Thread.sleep(1500); // TIMED_WAITING 상태를 확인하기 위해(1.5)
			}catch(Exception e) {
				e.printStackTrace();
			}
			
			for(long i=0; i<10000000000L; i++); 
		});
		
		CheckStateThread thread = new CheckStateThread(target);
		thread.start();
	}

}

```
