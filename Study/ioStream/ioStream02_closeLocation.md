# java.io
## close() 메소드의 위치
```java
package day27.basic;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.Scanner;

public class Test02 {
	public static void main(String[] args) {
		// aa.txt의 내용 읽기
		FileReader reader = null;
		Scanner sc = null; 
		try {
			reader = new FileReader("aa.txt");	
			// * 출력 스트림은 없는 파일을 목적지로 한 경우 새 파일을 생성한다.
			// 그러나 입력 스트림은 예외를 발생시킨다(FileNotFoundException).

			//			reader.read();
			// read() 자료형은 정수형을 return한다. 
			// 1) read()는 한 문자씩(chracter) 읽어들이고, 더이상 읽어들일 문자열이 없을 경우 -1을 return
			// 2) read(char[]||CharBuffuer cbuf) : 배열에 스트림의 내용을 담아준다(바구니 역할).
			// 파일에 존재하는 문자의 size가 필요하다.
			// -> File class를 이용하여 알아낼 수 있다.

			sc = new Scanner(reader);
			System.out.println(sc.next()); // sc.next(): space 이전까지만 읽어온다.
			// nextLine() : 한 줄(line)을 읽어온다(\n 전까지).

			// 파일 모두 읽어들이기
			while(sc.hasNext()) {
				System.out.println(sc.nextLine());
			} // 다음 내용이 있을 때까지만 해당 내용을 출력한다. 없을 경우 종료.


		}catch(IOException e) {
			e.printStackTrace();
		}finally {
			// 역순으로 닫기  :normal close mechanism

			try {
				if(null != sc)
					sc.close(); 
				// 1) error : sc cannot be resolved (try문 안에 scanner 객체 선언 시)
				// 이를 해결하기 위해서는 sc를 전역변수로 선언해야 한다.
				// 해결해도 2) error : be not initialized -> 초기화되지 않고 finally block으로 내려올 수 있다.
				// sc에 null로 initializing

				if(null != reader)
					reader.close();
			} catch (IOException e) {
				e.printStackTrace();
			} 
			// Exception 발생 가능성 때문에 전역변수 선언 및 초기화에도 error가 발생한다. 따라서 해당 문장을 try-catch로 감싼다.
			// 즉, finally{ try{ reader.close()}catch(IOException e){}}

			// 3) : NullPointerException 발생할 수 있다 -> inner catch block에 처리
			// 이는 if문으로 처리한다.
		}
	}

}
```
