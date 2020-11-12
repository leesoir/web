# Explain
getter와 setter를 사용하여 외부 클래스에서 private 선언된 필드에 접근 가능하도록 한다.
getter와 setter가 아닌 메소드에서 필드값을 가져올 경우 this.name과 같이 가져올 수 있지만, 되도록 getter와 setter를 사용해 가져오자.
main() 메소드는 public 선언된 클래스에 존재해야 한다. (아닐 경우 정상적으로 동작 안했음)

# SourceCode
```java
package day13.test;

import javax.swing.JOptionPane;

public class Student {
	// field
	private String name;
	private int kor;
	private int eng;
	private int math;
	private int aver;
	private char grade = 'F';

	//constructors
	Student(){
		this("", 0, 0, 0);
	}

	Student(String name){
		this(name, 0, 0, 0);
	}

	Student(int k, int e, int m){
		this("없음", k, e, m);
	}

	Student(String name, int k, int e, int m){
		this.setData(name, k, e, m);
	}

	// getters and setters
	public String getName() {
		return name;
	}

	public void setName(String name) {
		if (name.length() > 5) {
			return;
		}
		this.name = name;
	}

	public int getKor() {
		return kor;
	}

	public void setKor(int kor) {
		if (kor > 100 || kor < 0) {
			return;
		}
		this.kor = kor;
		this.setAver(); // 점수 변경 시 평균도 갱신된다.
	}

	public int getEng() {
		return eng;
	}

	public void setEng(int eng) {
		if (eng > 100 || eng < 0) {
			return;
		}
		this.eng = eng;
		this.setAver();
	}

	public int getMath() {
		return math;
	}

	public void setMath(int math) {
		if (math > 100 || math < 0) {
			return;
		}
		this.math = math;
		this.setAver();
	}

	public int getAver() {
		return aver;
	}

	public void setAver() {
		this.aver = (this.kor + this.eng + this.math) / 3;
		this.setGrade();
	}

	public char getGrade() {
		return grade;
	}

	public void setGrade() {
		switch (this.aver / 10) {
		case 10:
		case 9: {
			this.grade = 'A';
			return;
		}
		case 8: {
			this.grade = 'B';
			return;
		}
		case 7: {
			this.grade = 'C';
			return;
		}
		case 6: {
			this.grade = 'D';
			return;
		}
		}
	}

	// method
	String getData() {
		return "* 학생 정보 출력 *\n이름 : " + this.name + "\n국어 점수 : " + this.kor + "\n영어 점수 : " + this.eng + "\n수학 점수 : "
				+ this.math + "\n평균 : " + this.aver + "\n등급 : " + this.grade;
	}

	void setData(String name, int kor, int eng, int math) {
		this.setName(name);
		this.setKor(kor);
		this.setEng(eng);
		this.setMath(math);
		//		this.setAver();
		//		this.setGrade(); // 점수 설정 시 자동으로 setAver() -> setGrade() call
	}


	// method overRiding - *toString() 
	public String toString() {
		return "[" + name + "], 국어/영어/수학 : " + this.getKor() + "/" + this.getEng() + " / " + this.getMath() + 
				", 평균 : " + this.getAver() + ", 등급 : " + this.getGrade();
	}


	public static void main(String[] args) {
//		Student[] students = new Student[4];
//		String message = "";
//
//		for (int i = 0; i < students.length; i++) {
//			String name = JOptionPane.showInputDialog(null, "학생 이름을 입력하세요");
//			int kor = Integer.parseInt(JOptionPane.showInputDialog(null, "국어 점수를 입력하세요"));
//			int eng = Integer.parseInt(JOptionPane.showInputDialog(null, "영어 점수를 입력하세요"));
//			int math = Integer.parseInt(JOptionPane.showInputDialog(null, "수학 점수를 입력하세요"));
//
//			students[i] = new Student();
//			students[i].setData(name, kor, eng, math);
//
//		} // 배열 길이동안 입력받은 학생 정보를 토대로 Student 객체 생성 후 배열에 넣는다.
//
//		JOptionPane.showMessageDialog(null, "학생 정보 입력 완료!");
//		
//		for (Student s : students) {
//			message += s.getData();
//		}
//		
//		JOptionPane.showMessageDialog(null, message);
//		
		// toString override
		Student heejin;
		heejin = new Student("soir", 90, 100, 80);
		System.out.println(heejin); 
		// 객체 래퍼런스가 아닌 정보 메세지 출력 -> toString을 오버라이드하였고. sout에선s toString이 호출
	}
}


```
