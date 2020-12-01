# Thread
## 스레드와 동기화(Synchronize)
```java
package day25.basic;

class Resource{
	private static int RES = 1;
	
	synchronized static void increase(String name) {
		System.out.println(name + "이 increase() 실행 : 현재 res " + Resource.RES++);
		try {
			Thread.sleep(1000);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		System.out.println(name + "의 increase() 실행 종료");
	}
}

class MyIncreaseThread extends Thread{
	@Override
	public void run() {
		Resource.increase(getName()); // Thread의 getName() : Thread의 별명 return
	}
}

public class Test03 {
	public static void main(String[] args) {
		// Synchronized
		
		MyIncreaseThread t1 = new MyIncreaseThread();
		t1.setName("스레드 1");
		MyIncreaseThread t2 = new MyIncreaseThread();
		t2.setName("스레드 2");
		MyIncreaseThread t3 = new MyIncreaseThread();
		t3.setName("스레드 3");
		MyIncreaseThread t4 = new MyIncreaseThread();
		t4.setName("스레드 4");
		
		t1.start();
		t2.start();
		t3.start();
		t4.start();
	}

}

```
