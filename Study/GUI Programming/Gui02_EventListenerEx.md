# Event
사용자가 어떤 액션을 취하는 것
## ActionListner 예제
```java
package day29.basic;

import java.awt.BorderLayout;
import java.awt.FlowLayout;
import java.awt.GridLayout;
import java.awt.LayoutManager;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JTextField;

public class Test04 extends JFrame{
	
	// 화면에 들어갈 컴포넌트들 미리 선언
	JLabel la1 = new JLabel("이름");
	JLabel la2 = new JLabel("나이");
	JTextField txt1 = new JTextField();
	JTextField txt2 = new JTextField();
	JButton btn = new JButton("확인");
	JPanel centerP = new JPanel();
	JPanel southP = new JPanel();
	
	ActionListener listener = new ActionListener() {
		
		@Override
		public void actionPerformed(ActionEvent e) {
			String name = txt1.getText();
			int age = Integer.parseInt(txt2.getText());
			
			String message = age>=20 ? name+"님은 성인입니다." : name+"님은 미성년자입니다.";
			JOptionPane.showMessageDialog(Test04.this, message);
			// this로 하면 ActionListener 객체(listener)를 의미한다. 
		}
	};
	
	private void initCenterPanel() {
		// centerP의 레이아웃은 Grid이다 (2행 2열)
		centerP.setLayout(new GridLayout(2, 2, 10, 10));
		
		// 위젯 붙이기
		centerP.add(la1);
		centerP.add(txt1);
		centerP.add(la2);
		centerP.add(txt2);
	}
	
	private void initSouthPanel() {
		southP.setLayout(new FlowLayout());
		southP.add(btn);
		btn.addActionListener(listener);
	}
	
	public Test04() {


		// 판 생성(frame 설정)
		super("My Second GUI!"); // extends JFrame이므로 자기 자신(this)이 Frame이 됨

		// frame size set
		setSize(500, 500); 
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setLocationRelativeTo(null);



		LayoutManager layout = null;
		layout = new BorderLayout(20, 20); 
		setLayout(layout);

		initCenterPanel();
		initSouthPanel();
		add(centerP, BorderLayout.CENTER);
		add(southP, BorderLayout.SOUTH);
		
		pack();
		// pack() : 컴포넌트들이 가진 최소 너비/높이에 맞게 frame이 잡힌다. 조절 불가능.

		setVisible(true);
	}

	public static void main(String[] args) {
		new Test04();
	}
}
```
