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

// socket programming
// 통신 -> 다른 PC와 소통하는 것(TCP) 
// server-client 간 통신을 수행하는 프로그램을 작성한다. 

// * TCP와 UDP
// 1) TCP : Transmission Control Protocol(전송 프로토콜)
// --> 신뢰성, 연결지향적, 양방향성
// UDP에 비해 전송 속도가 느리다.

// * 연결 ? 
// 상대와 연결되었음을 확인한 후(Check Connection) 데이터 전송

// 2) UDP : 
// --> 비신뢰성, 비연결성
// TCP에 비해 전송 속도가 빠르다.


public class Server {
	// 서버 프로그램

	public Server() {
		ServerSocket sSocket = null;
		Socket cSocket = null;
		BufferedReader br = null;
		InputStreamReader is = null;
		InputStream in = null;
		BufferedWriter bw = null;

		try {
			sSocket = new ServerSocket(50000); // try-catch 처리 안할 시 unhandled error 
			cSocket = sSocket.accept();
			// accept() 동작 순서
			// 1. 서버 소켓을 열어두고 클라이언트를 기다린다.
			// 2. 하나의 클라이언트와 binding이 성립되면 상대 클라이언트의 Socket 객체를 반환한다.

			System.out.println("클라이언트와 연결 성공! Client IP : " + cSocket.getInetAddress());
			// getInetAddress() : 클라이언트 소켓의 IP 주소를 얻어옴

			in = cSocket.getInputStream(); // return type : InputStream(Not Reader)
			//			BufferedReader br = new BufferedReader(in); // reader 계열만 들어갈 수 있다.
			// 따라서 InputStream을 Reader 계열로 만들어야 함. 이 때 InputStreamReader를 이용한다.
			is = new InputStreamReader(in);
			br = new BufferedReader(is);
			bw = new BufferedWriter(new OutputStreamWriter(cSocket.getOutputStream()));

			// 줄이기 : BufferedReader br = new BufferedReader(new InputStreamReader(cSocket.getInputStream())));
			
			String input;
			while((input = br.readLine()) != null) {
				System.out.println("From Client : " + input);
				
				bw.write(input + "\n");
				System.out.println("Echo!!!!");
				bw.flush(); 
				// *flush : 스트림이 다 차지 않으면 전송이 되지 않는 경우가 있다. 이를 대비하여 스트림이 모두 차지 않아도 바로 전송하는 작업을 수행하는 메소드.
				
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

				if(null != sSocket)
					sSocket.close();

			} catch (IOException e) {
				e.printStackTrace();
			}
		}

	}
	
	public static void main(String[] args) {
		new Server();
	}
}
```
