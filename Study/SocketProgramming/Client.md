```java
package day31.basic;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.net.ServerSocket;
import java.net.Socket;

import javax.swing.JOptionPane;

public class Client {
	// 클라이언트 프로그램
	
	public Client() {
		Socket socket = null;
		BufferedReader br = null;
		InputStreamReader is = null;
		InputStream in = null;
		BufferedWriter bw = null;

		try {
			socket = new Socket("127.0.0.1", 50000); 
			// key : alt:shift:r
			// port number : 50000
			// IP(127.0.0.1) : 내 컴퓨터(localhost)
			// 클라이언트 측의 socket에 연결되면 binding이 이루어진다.
			System.out.println("서버와 연결 완료");
			
			br = new BufferedReader(new InputStreamReader(socket.getInputStream()));
			bw = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
			
			String input;
			while(true) {
				input = JOptionPane.showInputDialog("To Server : ");
				if(input == null)
					// x를 눌러도 null이 반환된다.
					break;
				
				bw.write(input + "\n");
				bw.flush();
				
				System.out.println("From Server : " + br.readLine());
			}
		

		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				// normal close
				if(bw != null) 
					bw.close();

				if(br != null)
					br.close();

				if(null != socket)
					socket.close();

			} catch (IOException e) {
				e.printStackTrace();
			}
		}

	}
	
	public static void main(String[] args) {
		new Client();
	}

}
```
