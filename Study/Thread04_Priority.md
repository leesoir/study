# Thread
## 스레드와 스레드 우선순위(priority)
```java
package day25.basic;

// Thread Priority
class TestThread extends Thread{
	@Override
	public void run() {
		System.out.println(getName() + "실행중");
		int i = 1;
		try {
			while(true) {
				System.out.println(i + "초..");
				i++;
				Thread.sleep(1000);
			}
		}catch (InterruptedException e) {
			System.out.println(getName() + "종료!");
		}
	}
}

public class Test04 {
	// Thread priority
	public static void main(String[] args) {
		TestThread t1, t2, t3, t4;
		t1 = new TestThread();
		t2 = new TestThread();
		t3 = new TestThread();
		t4 = new TestThread();
		
		t1.setName("스레드 1");
		t2.setName("스레드 2");
		t3.setName("스레드 3");
		t4.setName("스레드 4");
		
		t1.start();
		t2.start();
		t3.start();
		t4.start();
		
		
		// Thread priority
		t1.setPriority(Thread.MAX_PRIORITY);
		t2.setPriority(Thread.NORM_PRIORITY);
		t3.setPriority(Thread.MIN_PRIORITY);
	}

}
```
