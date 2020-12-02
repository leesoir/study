# ioStream
## byteStream
```java
package day28.basic;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

import javax.swing.JOptionPane;

public class Test01 {
	public static void main(String[] args) {
	
		// 바이트 기반 스트림
		// 비문자 형식의 파일(binary file : png, jpg, avi, mp4, ...)을 읽어들일 수 있다.
		
		// aa.jpg의 복사본 bb.jpg 파일 생성하기
		FileInputStream in = null;
		FileOutputStream out = null;
		
		try {
			// 스트림 생성하기
			// 파일을 복사하려면 두 개의 Stream이 필요하다. 
			// 1) 원본 파일의 이진 데이터를 가져올 입력 스트림
			// 2) 가져온 이진 데이터를 내보낼 출력 스트림
			
			// 원본
			in = new FileInputStream("aa.jpg");
			
			// 복사본
			out = new FileOutputStream("bb.jpg");
			
			int data; // 이진 데이터를 저장할 int형 변수
			
			// byteStream method : read()
			// 입력 스트림의 queue에 1byte(=8bit)를 읽어 이를 int type return
			// EOF(EndOfFile)에 도달하면 -1 return
			
			while((data = in.read()) != -1) {
				// data에 입력 스트림이 읽어온 데이터를 할당하고, 해당 값이 -1이 아닐(파일의 끝이 아니면) 동안 loop 실행
				out.write(data);
				// 1byte data를 outPutStream에 출력
			} // 해당 while문에서 IOException 발생 가능
			
			// 위 while문은 다음과 같음
//			while(true) {
//				data = in.read();
//				if(data == -1) break;
//				out.write(data);
//			}
			
			JOptionPane.showMessageDialog(null, "복사 완료!");
			
		}catch (IOException e) {
			e.printStackTrace();
		}finally {
			try {
				if(null !=out)
					out.close();
				if(null != in)
					in.close();
			}catch (IOException e) {
				e.printStackTrace();
			}
		}
		
	}
	
}
```

+) 파일 크기만큼 데이터를 받아와 byte[] 배열에 저장하고 해당 배열을 write()하기
```java
package day28.basic;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class Test02 {
	public static void main(String[] args) {
		// byte[] 를 미리 만들어 데이터를 한꺼번에 받아 전송(Buffer)
		// Test01에서는 읽고-출력하는 것을 3만번 반복했다(그림 파일이 30,000 byte).
		// date size가 커지면 작업 수행에 시간이 오래 걸리게 됨

		FileInputStream in = null;
		FileOutputStream out = null;
		File f = null; // 특정 디렉토리의 정보 등을 얻어올 때 사용
		byte[] arr;

		try {
			in = new FileInputStream("aa.jpg");
			out = new FileOutputStream("bb.jpg");

			// 파일 크기와 동일한 크기의 byte[] 만들기
			f = new File("aa.jpg"); // 원본 파일을 File형 객체로 포장
			long size = f.length(); // File.length() : 파일의 크기를 알려줌
			arr = new byte[(int)size];

			in.read(arr); // 배열 크기만큼 읽어들임
			out.write(arr); // 배열에 들어온 binary data를 outStream을 통해 출력

		}catch(IOException e) {
			e.printStackTrace();
		}finally {
			try {
				if(null != out)
					out.close();
				if(null != in)
					in.close();
			}catch (IOException e) {
			}
		}
	}

}
```
