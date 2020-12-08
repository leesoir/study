# extends를 통한 코드 중복 줄이기
```java
package day32.basic;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.net.Socket;

import javax.swing.JOptionPane;

public abstract class Common implements Runnable{
	protected String name;
	protected BufferedWriter bw;
	protected BufferedReader br;
	protected Socket socket;
	
	public Common(String name) {
		this.name = name;
		execute();
	}


	@Override
	public void run() {
		String input;
		try {
			while((input = br.readLine()) != null) {
				System.out.println(name + " : " + input);
			}
		}catch(IOException e) {
			e.printStackTrace();
		}
		
	}
	
	private void execute() {
		try {
			init();
			br = new BufferedReader(new InputStreamReader(socket.getInputStream()));
			bw = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));
			
			new Thread(this).start();
			
			String input;
			while(true) {
				input = JOptionPane.showInputDialog("상대방에게");
				if(input == null) {
					break;
				}
				bw.write(input + "\n");
				bw.flush();
				System.out.println("나 : " + input);
			}
		}catch(IOException e) {
			e.printStackTrace();
		}finally {
			try {
				if(bw != null)
					bw.close();
				if(br != null)
					br.close();
				if(socket != null)
					socket.close();
			}catch(IOException e) {
				e.printStackTrace();
			}
		}
	}
	
	protected abstract void init() throws IOException;

}
```
