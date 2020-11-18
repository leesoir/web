# Explain
```java
/*
 * 부모 클래스 : Student 
 *  1) 필드 : 학생이름, 나이, 학교명
 *  2) 메소드 :
 *   	ㄱ. 생성자 
 *   		- 디폴트 생성자(기본생성자)
 *   		- 학생이름, 나이, 학교명 3개 넣고 생성되도록 
 *   	ㄴ. getters
 *   	ㄷ. setters
 * 자식 클래스1 : ElementaryStudent
 *  1) 추가할 필드 : 국어점수, 영어점수, 학부모 연락처
 *  2) 메소드 : 
 *   	ㄱ. 생성자 
 *   		- 학생이름, 나이, 학교명
 *   		- 학생이름, 나이, 학교명, 학부모 연락처
 *   		- 학생이름, 나이, 학교명, 국어점수, 영어점수
 *		ㄴ. getters
 *		ㄷ. setters
 * 자식 클래스2 : MiddleSchoolStudent
 *  1) 추가할 필드 : 국어점수, 영어점수, 수학점수, 평균점수		
 *  2) 메소드 : 
 *  	ㄱ. 생성자 
 *  		- 학생이름, 나이, 학교명, 국어점수, 영어점수, 수학점수
 *  		  (평균 자동 계산)
 *  	ㄴ. getters
 *  	ㄷ. setters
 * 자식 클래스3 : HighSchoolStudent
 *  1) 추가할 필드 : 국어점수, 영어점수, 수학점수, 평균점수, 내신등급	
 *  2) 메소드 : 
 *  	ㄱ. 생성자 
 *  		- 학생이름, 나이, 학교명, 국어점수, 영어점수, 수학점수
 *  		  (평균 자동 계산)
 *  	ㄴ. getters
 *  	ㄷ. setters
 * 
 * 메인 클래스 : Quiz02
 *  - 이름과 나이를 입력 받음
 *  - 나이에 따른 객체 생성 (예. 13 -> new ElementaryStudent())
 *  - 각 객체의 필드를 입력 받아서 저장 
 *    예. 중학생이면
 *    	  학교명, 국어점수, 영어점수, 수학점수 입력 받음
 *  - 결과 출력
 */
 ```
 # SourceCode
 ```java
package com.javalec.quiz;

class Student{
	// student : 이름, 나이, 학교
	private String name;
	private int age;
	private String school;
	
	// constructors
	Student(){
		this("", 0, "");
	}

	Student(String name, int age, String school){
		this.name = name;
		this.age = age;
		this.school = school;
	}
	
	// getters and setters
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public String getSchool() {
		return school;
	}

	public void setSchool(String school) {
		this.school = school;
	}
	
	
	// toString override
	@Override
	public String toString() {
		return "이름 : " + this.name + "\n나이 : " + this.age + "\n학교 : " + this.school;
	}

}

class ElementaryStudent extends Student{
	// 초등학생 : 이름, 나이, 학교, 국어, 영어, 부모님 연락처
	private int kor;
	private int eng;
	private String parents;

	//constructors
	public ElementaryStudent(String name, int age, String school, int kor, int eng){
		super(name, age, school);
		this.setKor(kor);
		this.setEng(eng);
	}

	public ElementaryStudent(String name, int age, String school) {
		super(name, age, school);
	}

	public ElementaryStudent(String name, int age, String school, int parents) {
		super(name, age, school);
		this.setParents(parents);
	}

	//getters and setters
	public int getKor() {
		return kor;
	}

	public void setKor(int kor) {
		this.kor = kor;
	}

	public int getEng() {
		return eng;
	}

	public void setEng(int eng) {
		this.eng = eng;
	}

	public String getParents() {
		return parents;
	}

	public void setParents(int parents) {
		this.parents = parents;
	}
	
	
	// toString override
	@Override
	public String toString() {
		return super.toString() + "\n국어점수 : " + this.getKor()
		+ "\n영어점수 : " + this.getEng() + "\n부모님 연락처 : " + this.getParents();
	}

}


class MiddleSchoolStudent extends Student{
	// 중학생 : 이름, 나이, 학교, 국어, 영어, 수학, 평균
	private int kor;
	private int eng;
	private int math;
	private int aver;

	
	// constructors
	public MiddleSchoolStudent(String name, int age, String school, int kor, int eng, int math) {
		super(name, age, school);
		setKor(kor);
		setEng(eng);
		setMath(math);
		setAver((getKor() + getEng() + getMath())/3);
	}
	
	
	// getters and setters
	public int getKor() {
		return kor;
	}

	public void setKor(int kor) {
		this.kor = kor;
	}

	public int getEng() {
		return eng;
	}

	public void setEng(int eng) {
		this.eng = eng;
	}

	public int getMath() {
		return math;
	}

	public void setMath(int math) {
		this.math = math;
	}

	public int getAver() {
		return aver;
	}

	public void setAver(int aver) {
		this.aver = aver;
	}


	// toString() override
	@Override
	public String toString() {
		return super.toString() + "\n국어점수 : " + this.getKor() 
		+ "\n영어점수 : " + this.getEng() + "\n수학점수 : " + 
		this.getMath() + "\n평균 : " + this.getAver();
	}
}

class HighSchoolStudent extends MiddleSchoolStudent{
	// 고등학생 : 이름, 나이, 학교, 국어, 영어, 수학, 평균, 내신
	private char gpa;
	
	// constructors
	public HighSchoolStudent(String name, int age, String school, int kor, int eng, int math) {
		super(name, age, school, kor, eng, math);
		this.setGpa();
	}
	
	// getters and setters
	public char getGpa() {
		return gpa;
	}

	public void setGpa() {
		if(this.getAver() >= 90 && this.getAver() <= 100) {
			this.gpa = 'A';
		} else if(this.getAver() < 90 && this.getAver() >= 80) {
			this.gpa = 'B';
		} else if(this.getAver() < 80 && this.getAver() >= 70) {
			this.gpa = 'C';
		} else if(this.getAver() < 70 && this.getAver() >= 60) {
			this.gpa = 'D';
		} else this.gpa = 'F';
	}
	
	// toString override
	@Override
	public String toString() {
		return super.toString() + "\n내신등급 : " + this.getGpa();
	}

}

public class Quiz02 {
	public static void main(String[] args) {
		String inputName = JOptionPane.showInputDialog("이름을 입력하세요");
		int inputAge = Integer.parseInt(JOptionPane.showInputDialog("나이를 입력하세요"));

		if(inputAge < 14) {
			ElementaryStudent es = new ElementaryStudent(inputName, inputAge, null);
			// 초등학생 : 이름, 나이, 학교, 국어, 영어, 부모연락처
			String school = JOptionPane.showInputDialog("학교명을 입력하세요");
			int kor = Integer.parseInt(JOptionPane.showInputDialog("국어 점수를 입력하세요"));
			int eng = Integer.parseInt(JOptionPane.showInputDialog("영어 점수를 입력하세요"));
			String parents = JOptionPane.showInputDialog("부모님 연락처를 입력하세요");

			es.setSchool(school+"초등학교");
			es.setKor(kor);
			es.setEng(eng);
			es.setParents(parents);

			JOptionPane.showMessageDialog(null, es);
		}

		if(inputAge >= 14 && inputAge < 17) {
			// 중학생 : 이름, 나이, 학교, 국어, 영어, 수학, 평균
			MiddleSchoolStudent ms;

			String school = JOptionPane.showInputDialog("학교명을 입력하세요");
			int kor = Integer.parseInt(JOptionPane.showInputDialog("국어 점수를 입력하세요"));
			int eng = Integer.parseInt(JOptionPane.showInputDialog("영어 점수를 입력하세요"));
			int math = Integer.parseInt(JOptionPane.showInputDialog("수학 점수를 입력하세요"));

			ms = new MiddleSchoolStudent(inputName, inputAge, school+"중학교", kor, eng, math);
			JOptionPane.showMessageDialog(null, ms);
		}

		if(inputAge >=17 && inputAge < 20) {
			// 고등학생 : 이름, 나이, 학교, 국어, 영어, 수학, 평균, 내신
			HighSchoolStudent hs;

			String school = JOptionPane.showInputDialog("학교명을 입력하세요");
			int kor = Integer.parseInt(JOptionPane.showInputDialog("국어 점수를 입력하세요"));
			int eng = Integer.parseInt(JOptionPane.showInputDialog("영어 점수를 입력하세요"));
			int math = Integer.parseInt(JOptionPane.showInputDialog("수학 점수를 입력하세요"));

			hs = new HighSchoolStudent(inputName, inputAge, school+"고등학교", kor, eng, math);
			JOptionPane.showMessageDialog(null, hs);

			// check : 내신등급이 숫자로 나옴 -> 해결
		}

		if(inputAge < 8) {
			JOptionPane.showMessageDialog(null, "학생이 아닙니다!");
		}

		if(inputAge >= 20) {
			JOptionPane.showMessageDialog(null, "대학생입니다(관리 영역을 벗어났습니다.)");
		}
	}
}
```
