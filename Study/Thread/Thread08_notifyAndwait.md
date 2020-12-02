# Thread
## Thread method : notify()와 wait()
notify()는 일시정지 상태에 있는 다른 스레드를 RUNNABLE State로 변경해준다.

wait()는 현재 진행 중이던 스레드 객체(즉, 메소드 호출 객체)를 WAIT State로 변경해준다.
```java
package day26.basic;

class WorkObject{
	
	//methods
	public synchronized void methodA(Thread th) {
		System.out.println(th.getName() + "이 method()를 점유함!");
		notify();
		// 일시정지 상태에 있는 ThreadB를 RUNNABLE로 변경
		try {
			wait(); // try-catch문으로 묶어주어야 한다.
			// 현재 진행 중이던 ThreadA를 WAIT 상태로 변경
		}catch(Exception e) {
			e.printStackTrace();
		}
	}
	
	

	public synchronized void methodB(Thread th) {
		System.out.println(th.getName() + "이 method()를 점유함!");
		notify();
		// 일시정지 상태인 ThreadA를 RUNNABLE로 변경
		try {
			wait(); // 현재 진행중인 ThreadB를 WAIT 상태로 변경
		}catch(Exception e) {
			e.printStackTrace();
		}
	}
}



class ThreadA extends Thread{
	private WorkObject workObject;
	
	// constructor
	public ThreadA(WorkObject workObject) {
		this.workObject = workObject;
		this.setName("ThreadA");
	}
	
	// methods
	@Override
	public void run() {
		for(int i=0; i<10; i++) {
			workObject.methodA(this);
		}
	}
}



class ThreadB extends Thread{
	private WorkObject workObject;
	
	// constructor
	public ThreadB(WorkObject workObject) {
		this.workObject = workObject;
		this.setName("ThreadB");
	}
	
	// methods
	@Override
	public void run() {
		for(int i=0; i<10; i++) {
			workObject.methodB(this);
		}
	}
}



public class Test03 {
	public static void main(String[] args) {
		// 동기화를 위한 Object class의 method : wait(), notify() 
		// Object는 해당 method를 왜 가지고 있을까?
		// ==> 동기화가 될 공유 객체(즉, Lock이 걸릴 객체)는 여러 스레드가 함께 사용할 공유 자원이다.

		WorkObject workObject = new WorkObject();
		ThreadA a = new ThreadA(workObject);
		ThreadB b = new ThreadB(workObject);
		
		a.start();
		b.start();
	}

}
```
