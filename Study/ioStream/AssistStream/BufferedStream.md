# Assist Stream
## Buffered Stream
보조 스트림.

Buffer에 데이터를 모두 보내고, 전송자는 connection을 끊는다. 수신자는 Buffer에서 데이터를 가져간다. 

Buffer에 데이터 전송을 완료하면 연결을 끊고 다른 작업을 수행할 수 있어 시간이 절약된다는 장점이 있다.

없어도 작업 수행에는 문제가 없으나, 사용할 경우 성능이 좋아지고 사용이 편리하다.

단독으로 사용이 불가능하며 주 스트림에 연결하여 사용한다.

PC 간 통신, 파일(동영상처럼 크기가 큰 것)을 대상으로 사용한다.

```java
package day28.basic;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class Test03 {
	public static void main(String[] args) {

		// 보조 스트림 
		// 없어도 가능하지만, 있으면 성능이 좋아지고 사용이 편리하다.
		// * 단독으로 사용할 수 없고, 주 스트림에 붙여야 한다.
		// OjbectIn/OutStream, BufferedReader/Writer, BufferedIn/OutStream

		FileReader reader = null;
		BufferedReader breader = null;
		String str;

		try {
			reader = new FileReader("aa.txt");
			breader = new BufferedReader(reader); // 주 스트림인 reader에 연결

			while((str = breader.readLine()) != null) {
				System.out.println(str);
			}
			
		}catch(IOException e) {
			e.printStackTrace();
		}finally {
			try {
				if(null != breader)
					breader.close();
				if(null != reader)
					reader.close();
			}catch(IOException e) {
			}
		}
	}
}
```
