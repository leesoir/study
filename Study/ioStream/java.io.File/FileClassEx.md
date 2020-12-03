# java.io.File
파일이나 디렉토리를 다룰 때 사용하는 클래스. 
파일 크기 얻어오기, 빈 파일 생성, 권한 얻어오기, 디렉토리 생성, 디렉토리 파일 목록 얻어오기 등에 사용

## 
```java
import java.io.File;

public class Test01 {
	public static void main(String[] args) {
		
		File directory = new File("/"); // 현재 프로젝트가 위치하는 드라이브인듯? C: 혹은 D:
		System.out.println(directory.toString());
		
		// boolean isDirectory(), isFile()
		System.out.println(directory.isDirectory()); // 디렉토리 여부를 묻는다 -> true
		System.out.println(directory.isFile()); // 파일 여부를 묻는다 -> false
		
		// boolean canExecute(), canRead(), canWrite() : 실행, 읽기, 쓰기 권한 여부 
		// createNewFile() : 새 파일을 생성해준다.
		
		// boolean exist() : 파일의 존재 여부를 묻는다.
		// delete(), deleteOnExit() : 삭제 (종료 시 삭제)
		// getTotalSpace() : 총 사용 공간 return
		
		// File[] listFiles() : parameter로 (), FileFilter, FilenameFilter를 받는다.(오버로딩)
		File[] files = directory.listFiles();
		for(File f:files) {
			System.out.println(f.getName() + (f.isFile() ? "파일" : "디렉토리"));
		}
		
	}

}
```
