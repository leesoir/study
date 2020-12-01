# Thread

##  Runnable 객체를 익명 클래스(Anonymous Class)로 작성하기
```java
package day25.basic;

import javax.swing.JOptionPane;

class test implements Runnable{
	@Override
	public void run() {
		try {
			for(int i=10; i>0; i--) {
				System.out.println(i);
				Thread.sleep(1000);
			}
		}catch(Exception e){
			e.printStackTrace();
		}
	}
} // 이렇게 클래스를 만들 경우 Thread 객체에 Runnable 객체를 넣어야 한다. 굳이 클래스를 만들 필요가 없음.
// 이를 간단히 하기 위해 익명 클래스를 사용한다. 

// Anonymous class로 thread 추가하기
public class Test01 {
	public static void main(String[] args) {
		
		// 동작 1 : 카운트다운(10sec)

		test t = new test();
		Thread th = new Thread(t);
		th.start(); // 클래스를 생성해서 사용하기
		
		
		// 익명 클래스 사용하기
		Thread th2 = new Thread(new Runnable() {
			
			@Override
			public void run() {
				try {
					for(int i=10; i>0; i--) {
						System.out.println(i);
						Thread.sleep(1000);
					}
				}catch(Exception e){
					e.printStackTrace();
				}
			}
		});

		
		// 동작 2 : 입력받아 출력
		String str = JOptionPane.showInputDialog("아무거나");
		JOptionPane.showMessageDialog(null, "입력 결과 : " + str);



	}
}


```

## interrupt()로 스레드 객체 강제 종료하기
```java
package day25.basic;

import javax.swing.JOptionPane;

class MyThread extends Thread{
	@Override
	public void run() {
		while(!isInterrupted()) {
			// 종료되지 않을 동안 수행되는 코드
			System.out.println("MyThread 실행 중!");
		}
	}
}
public class Test02 {
	public static void main(String[] args) {
		MyThread my = new MyThread();
		my.start();
		
		JOptionPane.showMessageDialog(null, "종료하려면 확인을 누르세요.");
		my.interrupt();
	}

}
```
