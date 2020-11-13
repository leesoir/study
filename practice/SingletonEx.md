# Singleton Pattern 
singleton은 '단독 개체', '독신자'라는 뜻 말고도 '정확히 하나의 요소만 갖는 집합' 등의 의미가 있다. 
singleton 패턴은 객체의 생성과 관련된 패턴으로서 특정 클래스의 객체가 오직 한 개만 존재하도록 보장한다. 
즉 클래스의 객체를 하나로 제한한다.
[네이버 지식백과] singleton 패턴 (쉽게 배우는 소프트웨어 공학, 2015. 11. 30., 김치수)

# Singleton Pattern의 특징
1. instance라는 이름의 private static 멤버변수를 선언한다. data type은 반드시 해당 클래스여야 한다.
2. 클래스의 default constructor를 private 선언한다. 즉, 본인의 클래스 내부에서만 객체 생성이 가능하며, 외부 클래스에서는 객체화가 불가능하다.
3. 멤버변수 instance의 getter를 선언한다. 해당 getter를 통해서만 외부 클래스에서 class type 객체의 사용이 가능해진다.
== > 즉, getInstance()를 통해서만 해당 class type object의 사용이 가능한데 이 getter는 static 변수 instance를 리턴한다. 결국 실제로 사용하는 객체는 하나가 되는 것이다.

# 예제 : Class Singleton
```java
package day15.basic;

import javax.swing.JOptionPane;

class Singleton{
	// 1. instance 이름의 private static field declare. data type은 반드시 자기 자신이어야 한다.
	private static Singleton instance; // static field

	// 2. 기본 생성자를 private로 declare
	// 클래스 자기 자신 빼고는(Singleton) 객체를 생성할 수 없음.
	private Singleton() {

	}

	// 3. getter getInstance를 public declare
	public static Singleton getInstance() {
		if(instance == null) {
			instance = new Singleton();
		}
		return instance;
	}

	private int year;
	private int month;
	private int date;
	private String weekday; // instance field


	public int getYear() {
		return year;
	}

	public void setYear(int year) {
		this.year = year;
	}

	public int getMonth() {
		return month;
	}

	public void setMonth(int month) {
		this.month = month;
	}

	public int getDate() {
		return date;
	}

	public void setDate(int date) {
		this.date = date;
	}

	public String getWeekday() {
		return weekday;
	}

	public void setWeekday(String weekday) {
		this.weekday = weekday;
	}

	@Override
	public String toString() {
		return this.getYear() + "년 " + this.getMonth() + "월 " + this.getDate() + "일 " + this.getWeekday() + "\n";
	}

}

public class Test01 {
	public static void main(String[] args) {
		Singleton s = Singleton.getInstance(); // 객체는 한 번만 설정됨. 생성자가 private이므로 사용 가능한 객체는 instance 뿐이고 이 객체는 static 선언되었으므로.
		s.setYear(2020);
		s.setMonth(11);
		s.setDate(13);
		s.setWeekday("금요일");

		JOptionPane.showMessageDialog(null, s);

		Singleton s2 = Singleton.getInstance();
		s2.setYear(2022);
		s2.setMonth(12);
		s2.setDate(25);
		s2.setWeekday("크리스마스");

		JOptionPane.showMessageDialog(null, s); // 2022년 12월 25일 크리스마스
		JOptionPane.showMessageDialog(null, s2); // 2022년 12월 25일 크리스마스
		// 같은 값인 이유. 하나뿐인 객체 instance는 static 선언되었다. 따라서 main()에서 새롭게 객체를 생성 값을 할당해도, 
		// 결국에는 같은 주소를 가리키고 있기 때문에(값을 공유하기 때문에) 동일해진다.
	}

}
```
