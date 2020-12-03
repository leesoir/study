# 절대 경로와 상대 경로
## 절대 경로(Absolute Path)
root부터 시작하는 경로
## 상대 경로(Canonical Path)
현재 위치에서 상대적인 경로
ex) MegaIT : 절대경로는 서울 마포구 신촌로 128 적암빌딩 3,4층. 
			// 상대경로는 신촌CGV 맞은편 

##
```java
package day29.basic;

import java.io.File;
import java.io.IOException;

public class Test02 {
	public static void main(String[] args) {
		File directory = new File("../../");
		
		String path = directory.getPath();
		String aPath = directory.getAbsolutePath(); // 절대 경로
		try{
			String cPath = directory.getCanonicalPath(); // 상대 경로 : error : unHandledException
			
			System.out.println(path); // nothing
			System.out.println(aPath); // D:\heejin\02. myworkspace\MyProject
			System.out.println(cPath); // D:\heejin\02. myworkspace\MyProject
			
			
			// * 경로 표기법 Location Expression
			// 처음 시작하는 구분자에 따라 의미가 달라진다.
			
			// 1. /로 시작
			// "/aa/bb.txt"
			
			// 2. ./로 시작
			// "./aa/bb.txt"
			
			// 3. ../로 시작
			// "../aa/bb.txt"
			
			// 4. 빈 문자열로 시작
			// "aa/bb.txt";
			
			File[] files = {
					new File("aa/bb.txt"),
					new File("/aa/bb.txt"),
					new File("./aa/bb.txt"),
					new File("../aa/bb.txt"),
			};
			
			for(File f: files) {
				System.out.println(f.getCanonicalPath());
			}
			
			
		} catch(IOException e) {
			e.printStackTrace();
		}
	}

}
```
