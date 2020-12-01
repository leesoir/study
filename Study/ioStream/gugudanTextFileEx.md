# Explain
1. 2~9단까지의 구구단 텍스트 파일을 생성하고 각 파일에 단에 맞는 구구단을 write()한다. (파일 쓰기)
2. 사용자에게 단을 입력받아 해당 구구단 파일을 열고, 그 내용을 JOptionPane으로 출력한다. (파일 읽기)

## 파일 쓰기
```java
package day27.quiz;

import java.io.FileWriter;
import java.io.IOException;

public class Quiz01 {
	public static void main(String[] args) {
		// 2단~9단.txt 생성
		
		FileWriter writer = null;
		try {
			for(int i=2; i<10; i++) {
				writer = new FileWriter(i+".txt", true);
				for(int j=1; j<10; j++){
					writer.write(i + " x " + j + " = " + (i*j) + "\n");
				}
			}
			
			
			System.out.println("구구단 텍스트 파일 생성 완료!");
		}catch (IOException e) {
			e.printStackTrace();
		}finally {
			try {
				if(null != writer)
					writer.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}

}
```

## 파일 읽기
```java
package day27.quiz;

import java.io.FileReader;
import java.io.IOException;
import java.util.Scanner;

import javax.swing.JOptionPane;

public class Quiz02 {
	public static void main(String[] args) {
		// 사용자에게 단을 입력받아 해당 구구단 txt 파일을 열고, 그 내용을 JOptionPane으로 출력한다.
		FileReader reader = null;
		Scanner sc = null;
		
		try{
			int dan = Integer.parseInt(JOptionPane.showInputDialog("단을 입력하세요."));
			reader = new FileReader(dan+".txt"); // 문자열과 병합(+)하는 부분에서 자동 문자열 casting이 일어난다.
			StringBuffer sb = new StringBuffer();
			sc = new Scanner(reader);
			
			while(sc.hasNext()) {
				sb.append(sc.nextLine() + "\n");
			}
			
			JOptionPane.showMessageDialog(null, sb);

			reader.close();
			sc.close();
		}
		catch (IOException e) {
			e.printStackTrace();
		}finally {
			try {
				if(null != sc)
					sc.close();

				if(null != reader)
					reader.close();
				
			}catch(IOException e) {
				e.printStackTrace();
			}
		}
	}
}
```
