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

public class Client implements Runnable{
	private BufferedReader br;
	
	@Override
	public void run() {
		String input;
		try {
			while((input=br.readLine()) != null) {
				System.out.println("Server : " + input);
			}
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	
	public Client() {
		Socket socket = null;
		BufferedWriter bw = null;
		
		try {
			socket = new Socket("127.0.0.1", 50000);
			System.out.println("서버와 연결되었다!");
			
			br = new BufferedReader(new InputStreamReader(socket.getInputStream()));
			bw = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
			
			new Thread(this).start();
			
			String input;
			while(true) {
				
				input = JOptionPane.showInputDialog("To Server.");
				if(input == null) {
					break;
				}
				bw.write(input + "\n");
				bw.flush();
				
				System.out.println("나 : " + input);
				
			}
		} catch(IOException e) {
			e.printStackTrace();
		} finally {
			try {
				if(bw != null)
					bw.close();
				if(br != null) 
					br.close();
				if(socket != null)
					socket.close();
			} catch(IOException e) {
				e.printStackTrace();
			}
		}
	
	}
	
	
	public static void main(String[] args) {
		new Client();
	}
}
```
