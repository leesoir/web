```java
package com.javalec.quiz;

import javax.swing.JOptionPane;

/*
 * 클래스 : Rectangle
 *  - 필드(멤버변수) : base, height
 *  - 메소드 
 *    1) setData() : 두 정수를 인자값으로 받아, 객체의 base, height에 각각 저장
 *    2) getArea() : 넓이를 리턴
 *    3) getCircum() : 둘레를 리턴
 * 
 * 메인 클래스 : Quiz01
 *  - Rectangle 객체 1개 생성 
 *  - JOptionPane을 사용하여 밑변, 높이를 입력 받고, 
 *    Rectangle 객체에 저장 (setData() 사용)
 *  - 이 사각형 객체의 넓이와 둘레를 메소드를 사용하여 출력 (getArea(), getCircum())
 */	
class Rectangle {
	int base;
	int height;

	void setData(int base, int height) {
		this.base = base;
		this.height = height;
	}

	int getArea() {
		return this.base*this.height;
	}

	int getCircum() {
		return 2*(this.base+this.height);
	}
}
public class Quiz01 {
	public static void main(String[] args) {
		Rectangle r = new Rectangle(); // default constructor
		r.setData(Integer.parseInt(JOptionPane.showInputDialog(null, "밑변")), 
				Integer.parseInt(JOptionPane.showInputDialog(null, "높이")));

		System.out.println(r.getArea());
		System.out.println(r.getCircum());
	}
}
```
