# Assist Stream
## Object Stream
```java
package day28.homework;

import java.util.ArrayList;
import java.util.List;
import java.util.Map.Entry;
import java.util.Set;
import java.util.TreeMap;

import javax.swing.JOptionPane;

public class Homework01 {

	private TreeMap<String, String> map;

	private void save() {
		// 현재 map을 word.w 에 덮어씀 (저장)
		// 1.FileOutputStream 생성
		// 2.ObjectOuputStream 생성
		try(FileOutputStream out = new FileOutputStream("words.w", true); 
				ObjectOutputStream oout = new ObjectOutputStream(out);){
				
		// 3.oOut.writeObject(map);
		oout.writeObject(map);
		
		// 4.ObjectOuputStream 닫기
		// 5.FileOutputStream 닫기 
			}catch (Exception e) {
		}
	}
	private void load() {
		// word.w 에 readObject하여 그 객체를 map에 저장
		// FileNotFound 익셉션이 발생했다면 new TreeMap()하여 map에 저장
		
		// 1. FileInputStream 생성
		// 2. ObjectInputStream 생성
		// 3. map = (TreeMap<String, String>)oIn.readObject()
		// 4. ObjectInputStream 닫기
		// 5. FileInputStream 닫기
		
		try(FileInputStream in = new FileInputStream("words.w"); // 최초 실행 시 여기에서 Exception(FileNotFound)
				ObjectInputStream oin = new ObjectInputStream(in);){
			
			map = (TreeMap<String, String>)oin.readObject();
			// think : 최초 실행에는 words.w가 없어 FileNotFoundException
			
		}catch(FileNotFoundException e) {
			// 최초 실행일 경우(파일이 없을 경우)
			map = new TreeMap<>();
		}
		catch (Exception e) {
			e.printStackTrace();
		}
		
	}
	
	private void menu1() { // 단어 추가
		String w, m;
		w = JOptionPane.showInputDialog("새 단어");
		m = JOptionPane.showInputDialog("[" + w + "]의 뜻");
		if (w == null || m == null) {
			JOptionPane.showMessageDialog(null, "메뉴로 돌아갑니다.");
		}
		w = w.trim();
		m = m.trim();

		map.put(w, m);
		JOptionPane.showMessageDialog(null, "저장 완료!");
	}

	private void menu2() { // 단어 검색
		String w, m;
		w = JOptionPane.showInputDialog("검색할 단어");
		if (w == null) {
			JOptionPane.showMessageDialog(null, "메뉴로 돌아갑니다.");
		}
		JOptionPane.showMessageDialog(null, map.containsKey(w) ? map.get(w) : "미등록 단어");
	}

	private void menu3() { // 모든 단어 보기
		StringBuffer message = new StringBuffer("===== 단어 현황 =====");
		for (Entry<String, String> en : map.entrySet()) {
			message.append("[" + en.getKey() + "] : " + en.getValue() + "\n");
		}
		JOptionPane.showMessageDialog(null, message);
	}

	private void menu4() { // 퀴즈
		// 1. '단어'들을 리스트에 담는다.
		Set<String> wordSet = map.keySet(); // 단어들 => Set에 담음
		List<String> wordList = new ArrayList<>(wordSet);

		// 2. 리스트에서 랜덤하게 1개의 '단어'를 뽑는다.
		int rand = (int) (Math.random() * wordList.size());
		String quizWord = wordList.get(rand);

		// 3. 사용자에게는 뽑힌 단어의 '뜻'을 문제로 낸다.
		String ansWord = JOptionPane.showInputDialog("[" + map.get(quizWord) + "](은)는 영어로?");

		// 4. 사용자가 입력한 '답'과 위에서 뽑은 '단어'가 같은 지 확인한다.
		JOptionPane.showMessageDialog(null, quizWord.equals(ansWord) ? "정답!" : "땡..");
	}

	private void menu4_2() {
		// 1. '뜻'들을 배열에 담는다. (map : {apple:사과, book:책, computer:컴퓨터}
		String[] meanings = new String[map.size()]; 
		map.values().toArray(meanings); // meanings : [사과, 책, 컴퓨터] 
		
		// 2. 리스트에서 랜덤하게 1개의 '뜻'을 뽑는다.
		int rand = (int) (Math.random() * meanings.length); // 2
		String quizMeaning = meanings[rand]; // quizMeaning : 컴퓨터

		// 3. 사용자에게는 뽑힌 단어의 '뜻'을 문제로 낸다.
		String ansWord = JOptionPane.showInputDialog("[" + quizMeaning + "](은)는 영어로?");

		// 4. 사용자가 입력한 '답'와  문제(단어)에 매핑된 '단어'가 같은 지 확인한다. 
		JOptionPane.showMessageDialog(null, quizMeaning.equals(map.get(ansWord)) ? "정답!" : "땡..");
		
	}

	public Homework01() {
		String select;
		load();
		menu: while (true) {
			select = JOptionPane
					.showInputDialog("1. 단어 추가 \n" + "2. 단어 검색 \n" + "3. 모든 단어 보기 \n" + "4. 퀴즈 \n" + "0. 종료");
			switch (select) {
			case "0":
				JOptionPane.showMessageDialog(null, "프로그램을 종료합니다.");
				
				break menu;
			case "1":
				menu1();
				break;
			case "2":
				menu2();
				break;
			case "3":
				menu3();
				break;
			case "4":
				menu4();
				break;

			default:
				JOptionPane.showMessageDialog(null, "다시 입력하세요.");
				break;
			}
		}
		save();
	}

	public static void main(String[] args) {
		new Homework01();
	}
}
```
