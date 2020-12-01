# Thread 스레드
하나의 프로세스가 처리하는 작업 단위를 의미한다.
1) Single Thread : 스레드가 하나인 프로그램
2) Multi Thread : 여러 개의 스레드(2개 이상)로 구성된 프로그램

* 스레드 추가하기
1. class에 extends Thread 또는 implements Runnable(Anonymous class로 작성해도 ok)
2. run() 메소드의 override
3. Thread 실행 시점에 생성한 객체로 start() 메소드를 호출한다. 이 때는 extends Thread한 클래스와 implements Runnable한 클래스는 다르게 처리한다.
이는 start() 메소드가 Thread class에는 존재하지만 Runnable interface에는 존재하지 않기 때문이다.

* Runnable의 존재 이유

implements Runnalbe할 경우 결국 Thread 객체를 생성하여 인자로 Runnable 객체를 가져와야 한다. 
Runnable은 병렬 스레드를 만들 수 있는 root이기 때문에 존재하며, 이미 부모 class가 있을 경우 Runnable의 implements로 스레드의 추가가 가능하게 한다.


```java
import javax.swing.JOptionPane;

class TimerThread extends Thread{
	@Override
	public void run() {
		// 10초 카운트다운
		try {
			for(int i=10; i>0; i--) {
				System.out.println(i + "초");
				Thread.sleep(1000);
			}
		}catch(Throwable e) {
			e.printStackTrace();
		}
	}
}

class TimerRunnable implements Runnable{
	@Override
	public void run() {
		try {
			for(int i=10; i>0; i--) {
				System.out.println(i + "초");
				Thread.sleep(1000);
			}
		}catch(Throwable e) {
			e.printStackTrace();
		}
	}
}

public class Test04 {
	public static void main(String[] args) {
		// JOptionPane으로 입력을 받은 뒤 해당 값을 다시 JOptionPane으로 출력한다.
		// 이와 동시에 sout으로 10초를 카운트다운 한다.
		// 이는 단일 스레드로 구현이 불가능하다. 
		
		// extends Thread
		Thread th = new TimerThread(); // 동시에 수행된다.
		th.start();
		
		// implements Runnable : Thread 클래스의 도움을 받는다.
		Runnable runnable = new TimerRunnable();
//		runnable.start(); // error
		Thread thread = new Thread(runnable);
		thread.start();
		
		// 1) 입/출력
		String input = JOptionPane.showInputDialog("입력하세요");
		JOptionPane.showMessageDialog(null, input);

		// 2) 10초의 카운트다운 : sleep() 메소드로 인한 try-catch 처리
//		try {
//			for(int i=10; i>0; i--) {
//				System.out.println(i + "초");
//				Thread.sleep(1000);
//			}
//		}catch(Throwable e) {
//			e.printStackTrace();
//		}
		
	
		
		// 스레드 추가로 작업의 동시 수행 구현
		// 작업 1 : 입력받은 값 출력
		// 작업 2 : 10초 카운트다운
		// 추가해야 할 스레드 : 1개
		// 메인 스레드가 한 작업을, 추가한 스레드가 다른 작업을 수행하게 한다.
		
		
		// 1) extends Thread로 구현하기
		// 1. Thread를 extends하는 class TimeThread를 생성하고, 내부에 run()의 오버라이드 --> 10초 카운트다운 내용을 넣는다.
		// 2. TimerThread를 main 내부에서 실행(Thread th = new TimeThread(); \n th.start();)
		
		
		// 2) implements Runnable로 구현하기
		// 1. Runnable implements하는 class를 생성하고 run 오버라이드
		// 2. runnable ru = new 클래스(); \b ru.start(); 하면 error: Runnable interface에는 run() 메소드밖에 없다(Abstrat method).
		
		// 해결 --> Thread 빌리기
		// Runnable runnable = new TimerRunnable();
		// Thread thread = new Thread(runnable);
		// thread.start();
	}

}
