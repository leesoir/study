# java.io
## java.io package
﻿java.io는 입출력 스트림 관련 패키지로, io는 input/output을 의미한다. 파일을 전송하거나 파일의 쓰기/읽기, 통신(메일, 채팅 등) 등에 이용된다.
 
## Stream 사용 매커니즘
1. Stream type(byte 기반/문자 기반)과 방향 결정
2. Stream 객체 생성
3. Stream 객체를 통해 데이터 입/출력(read()/write())
4. Stream 닫기(close())
 * stream close는 안정적인 파일 사용 및 메모리 누수(Resource leak)를 방지하기 위해 꼭 필요하다.
 
## 파일 쓰기
```java
public class Test01 {
	public static void main(String[] args) {
		// 예제 : aa.txt 파일에 "피카츄", "라이츄", "파이리"를 저장하기
		
		// write()
		try{ 
		// mechanism
		// 1. Stream type과 방향 결정하기
		// 문자 기반이므로 Reader/Writer
			FileWriter writer;
		
		// 2. Stream 생성
		writer = new FileWriter("aa.txt"); // default 경로에 aa.txt 파일이 만들어진다.
		// default directory : project 폴더에 존재한다.(src 상위 폴더)
		// directory 구분 : / 혹은 \\(\하나는 이스케이프 문자로 간주된다)
		// unhandleException : 반드시 예외 처리가 필요하다.
		
		// * write()와 append()
		// write()는 덮어씌어진다. 즉, 기존의 내용을 모두 지우고 write()한 내용을 작성한다.
		// append()는 기존에 있던 내용 밑에 파라미터를 덧붙여 작성한다.
		// append()를 사용할 경우 FileWriter의 생성자에 append 여부를 파라미터로 넣어주어야 한다.
		// writer = new FileWriter("aa.txt", true);
		// append 여부가 true이면 write()를 써도 내용이 덧붙여 작성된다.
		
		// 3. Stream에 데이터 쓰기/읽기
		
		// 데이터 쓰기
		writer.write("피카츄\n"); // write() : char형 배열, String, int도 parameter로 받음. 자동 줄바꿈을 지원하지 않는다.
		writer.write("라이츄\n");
		writer.write("파이리\n");
//		writer.append("붙여쓰기");
		
		// 4. Stream close 
		writer.close();
		System.out.println("파일 저장 완료!");
		
		}catch(IOException e) { 
			// IOException : 디렉터리 경로가 잘못되었거나 스트림이 열리지 않았을 경우, 파일이 생성되지 않았을 때 발생한다. 스트림 관련 예외. 
			e.printStackTrace();
		}
	}

}

```

## 파일 읽기
```java
public class Test02 {
	public static void main(String[] args) {
		// aa.txt의 내용 읽기
		try {
			FileReader reader = new FileReader("aa.txt");	
			// * 출력 스트림은 없는 파일을 목적지로 한 경우 새 파일을 생성한다.
			// 그러나 입력 스트림은 예외를 발생시킨다(FileNotFoundException).
			
//			reader.read();
			// read() 자료형은 정수형을 return한다. 
			// 1) read()는 한 문자씩(chracter) 읽어들이고, 더이상 읽어들일 문자열이 없을 경우 -1을 return
			// 2) read(char[]||CharBuffuer cbuf) : 배열에 스트림의 내용을 담아준다(바구니 역할).
			// 파일에 존재하는 문자의 size가 필요하다.
			// -> File class를 이용하여 알아낼 수 있다.
			
			 Scanner sc = new Scanner(reader);
			 System.out.println(sc.next()); // sc.next(): space 이전까지만 읽어온다.
			 // nextLine() : 한 줄(line)을 읽어온다(\n 전까지).
			 
			 // 파일 모두 읽어들이기
			 while(sc.hasNext()) {
				 System.out.println(sc.nextLine());
			 } // 다음 내용이 있을 때까지만 해당 내용을 출력한다. 없을 경우 종료.
			
		}catch(FileNotFoundException e) {
			e.printStackTrace();
		}
	}

}
```
