# Explain
exit가 입력될 때까지 문자열을 JOptionPane으로 입력받고, exit를 입력하면 YYYYMMDD_HHmmss.txt로 log파일을 생성하여 문자열 저장
    
## SourceCode
```java
package day27.quiz;

import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;

import javax.swing.JOptionPane;

public class Quiz03 {
	public static void main(String[] args) {
		// exit가 입력될 때까지 문자열을 jop으로 입력받고, exit를 입력하면 YYYYMMDD_HHmmss.txt로 log파일을 생성하여 문자열 저장

		Date date;
		SimpleDateFormat sd = new SimpleDateFormat("YYYYMMDD_HHmmss");
		FileWriter writer;
		

		try {
			date = new Date();
			// String title = sd.format(date); // 현재 날짜값(date)을 가져와 규칙에 맞게 format하고(sb.format(date)) 그 값을 title에 넣는다.
			// writer = new FileWriter(title+".txt", true);
       writer = new FileWriter(sd.format(date)+".txt", true); // 줄이기 가능
			
			loop:while(true) {
				String input = JOptionPane.showInputDialog("입력하세요(exit를 누르면 종료합니다).");
				
				if(input.equals("exit")) {
					break loop;
				}
				
				writer.append(input + "\n");
			}
			
			System.out.println("일기 작성 완료!");
			writer.close(); // FileWriter객체를 닫지 않으면 메모장에 입력한 내용이 안 들어간다.
			
		}catch(IOException e) {
			e.printStackTrace();
		}
	}

}
```
