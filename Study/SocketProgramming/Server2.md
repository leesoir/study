```java
package day32.basic;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.net.ServerSocket;
import java.net.Socket;

import javax.swing.JOptionPane;
public class Server implements Runnable {
	
	private BufferedReader br;
	
	@Override
	public void run() {
		String input;
		try {
			while((input=br.readLine()) != null) {
				System.out.println("Client : " + input);
			}
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	
	public Server() {
		ServerSocket sSocket = null;
//		BufferedReader br = null;
		BufferedWriter bw = null;
		
		try {
			sSocket = new ServerSocket(50000); // 포트 번호 :50000
			System.out.println("서버 소켓 생성!");
			
			Socket clientSocket = sSocket.accept();
			System.out.println("클라이언트와 연결되었다. 클라이언트 IP : " + clientSocket.getInetAddress());
			br = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
			bw = new BufferedWriter(new OutputStreamWriter(clientSocket.getOutputStream()));
			
			new Thread(this).start();
			
			
//			String input;
			while(true) {
				String toClient = JOptionPane.showInputDialog("To Client");
				if(toClient == null) {
					break;
				}
				bw.write(toClient + "\n");
				bw.flush();
				System.out.println("나 : " + toClient);
			}
		} catch(IOException e) {
			e.printStackTrace();
		} finally {
			try {
				if(bw != null)
					bw.close();
				if(br != null) 
					br.close();
				if(sSocket != null)
					sSocket.close();
			} catch(IOException e) {
				e.printStackTrace();
			}
		}
	}
	public static void main(String[] args) {
		new Server();
	}
}

```
