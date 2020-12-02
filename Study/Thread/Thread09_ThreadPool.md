# Thread 
## ThreadPool

```java
package day27.homework;

import java.io.FileWriter;
import java.util.ArrayList;
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
/*
 * 쓰레드 1000개 생성 (X)
 * 쓰레드 10개만 생성 --> 작업 1000개를 10개의 스레드로만 처리하도록 ==> ThreadPool
 * 
 *  Callable 과 Runnable 
 *              
 *  Runnable 의 작업 메서드 
 *  	public void run() 
 *  Callable 의 작업메서드 
 *  	public V call()	
 * 
 * 
 */

class GugudanCallable implements Callable<Void>{
	private int dan;
	public GugudanCallable(int dan) {
		this.dan = dan;
	}
	
	@Override
	public Void call() throws Exception {
		FileWriter writer = null;
		String filename = null;
		StringBuffer sb = null;
		
		filename = dan + "단.txt";
		sb = new StringBuffer();
		for(int i = 1; i <= 9; ++i) {
			sb.append(dan + " X " + i + " = " + dan*i + "\n");
		}
		
		try {
			writer = new FileWriter(filename);
			writer.write(sb.toString());
		} catch(Exception e) {
			e.printStackTrace();
		} finally {
			try {
				if (null != writer) {
					writer.close();
				}
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
		return null;
	}
}
public class Homework05 {
	public static void main(String[] args) {
		
		// 쓰레드 풀 생성 
		ExecutorService service = Executors.newFixedThreadPool(10); 
		
		ArrayList<Callable<Void>> tasks = new ArrayList<>();
		for(int i = 2; i <= 1000; ++i) {
			tasks.add(new GugudanCallable(i)); // 1000개의 작업 객체 (Callable) 를 list에 미리 담기  
		}
		try {
			service.invokeAll(tasks);// list 전달하여 쓰레드 10개가 처리해야할 작업들을 전달 + 모두 실행! 
		} catch (InterruptedException e) {
			e.printStackTrace();
		} 
		
	}
}


```
