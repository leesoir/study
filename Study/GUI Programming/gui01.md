# User Interface
유저와 프로그램 간 상호작용을 위한 규약을 유저 인터페이스(User Interface : UI)라고 한다.

이 때 해당 인터페이스를 그래픽으로 구현하는 것을 GUI(Graphic User Interface), 텍스트 기반으로 구현하는 것을 TUI(Text User Interface : ex-cmd)라고 한다.
GUI 관련 클래스들은 java.awt와 javax.swing 패키지에 들어있다.

* java.awt

JDK 1.0 version에 출시.
OS 환경에 맞게(의존하여) GUI 컴포넌트를 띄운다는 단점이 있다. -> OS에 따라 컴포넌트 사용이 불가하다던가, 모양이 변경되는 문제
이를 해결하기 위해 1.4에 swing 패키지를 update 하였다. 
ex) Button, TextField, ...

* javax.swing

JDK 1.4version에 출시. awt 패키지 대부분의 내용을 가지고 있다.
awt와 다르게 JVM이 자체적으로 컴포넌트를 띄운다. 따라서 모든 운영체제에서도 거의 동일한 컴포넌트가 출력된다. 
=> 트렌드가 바뀌면서 운영체제에 맞춰 나오도록 새롭게 다시 update되었다. 
ex) JButton, JTextField, ...

* javaFx
search 

## GUI
	 *root : Component
	 판 : Panel, Frame -> Container 상속
	 모형 : Button, TextField, .. -> Component의 자식 클래스들(component or widget)
	 틀 : GridLayout, BorderLayout, ... -> LayoutManager 상속
   
  ```java
  package day29.basic;

import java.awt.BorderLayout;
import java.awt.Dimension;
import java.awt.FlowLayout;
import java.awt.GridBagLayout;
import java.awt.GridLayout;
import java.awt.LayoutManager;

import javax.swing.JButton;
import javax.swing.JFrame;

public class Test03 {
	private JFrame frame;
	private JButton[] btns;

	public Test03() {
		
		
		// 판 생성(frame 설정)
		frame = new JFrame("나의 첫 GUI!"); // paramter : Stringtitle
		// default size : width 0, height 0
		
		// frame size set
		frame.setSize(100, 100); // parameter : int width, int height
		// +) Dimension d 객체를 파라미터로 받을 수 있다(가로, 세로로 구성) -> 유지보수를 위해 사용
//		frame.setSize(new Dimension(100, 100));
		
		// * GUI - x 버튼을 눌러도 프로그램이 종료되지 않는다. (기본값)
		// X클릭 시 프로그램 종료 되도록 set
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		// default : DO_NOTHING_ON_CLOSE (아무 것도 하지 않음)
		// HIDE/DESPOSE_ON_CLOSE : Background process 창에 보여준다.
		
		
		// 창이 뜨는 위치 set : Location set
		// 1) 한 가운데에 띄우기 -> frame.setLocationRelativeTo(null)
		frame.setLocationRelativeTo(null);
		// setLocationRelativeTo : 컴포넌트 기준 상대적으로 위치를 정해줌. null이 들어가면 정가운데에 위치하게 된다.
		// 2) 특정 위치(좌표)에 띄우기 -> frame.setLocation(int x, int y)
//		frame.setLocation(505, 500);
		// prameter로 Point객체도 가능 -> frame.setLocation(new Point(404, 400)); 
		// * 컴포넌트 위치의 기준이 되는 좌표는 컴포넌트의 왼쪽 최상단이다.
		
		
		
		// 판에 컴포넌트 추가하기
		// 추가 전 판의 틀 결정하기 -> 레이아웃 설정 
		LayoutManager layout = null;
		// 1) GridLayout
		layout = new GridLayout(4, 1); // parameter로 행과 열의 개수를 받는다 (int row, int col).
		frame.setLayout(layout);
		
		// 2) FlowLayout
		layout = new FlowLayout(); // 화면 크기에 따라 컴포넌트 위치가 재설정된다.
		// parameter : int align -> 정렬값. FlowLayout.LEFT/RIGHT/CENTER/LEADING/TRAILING
		// int hgap, vgap -> 버튼의 수평/수직 간격
		frame.setLayout(layout);
		
//		// 3) BorderLayout
//		layout = new BorderLayout();
//		// * 이후 컴포넌트들의 add()시 추가 옵션을 지정해야 함(동/서/남/북/중앙)
//		frame.setLayout(layout);
		
		btns = new JButton[4];
		//컴포넌트 생성
		// GridLayout, FlowLayout
		for(int i=0; i<btns.length; i++) {
			btns[i] = new JButton("희진" + i); // Automatic Casting to String
			frame.add(btns[i]);
		}
		
		// * Layout이 BorderLayout인 경우 -> 컴포넌트 위치를 지정
		// frame.add(btns[0], BorderLayout.CENTER);
		// frame.add(btns[0], BorderLayout.NORTH);
		// frame.add(btns[0], BorderLayout.SOUTH);
		
		
		// 창 띄우기(frame 띄우기)는 마지막에 실행한다.
		frame.setVisible(true);
	}

	public static void main(String[] args) {
		new Test03();
	}

}
