# Explain

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
 
```java
package com.javalec.quiz;

class Student{
	private String name;
	private int age;
	private String school;

	Student(){
		this("", 0, "");
	}

	Student(String name, int age, String school){
		this.name = name;
		this.age = age;
		this.school = school;
	}

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


}

class ElementaryStudent extends Student{
	private int kor;
	private int eng;
	private int parents;

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

	public int getParents() {
		return parents;
	}

	public void setParents(int parents) {
		this.parents = parents;
	}


}


class MiddleSchoolStudent extends Student{
	
}

class HighSchoolStudent extends MiddleSchoolStudent{
	
}

public class Quiz02 {
	public static void main(String[] args) {

	}
}
```
