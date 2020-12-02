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
