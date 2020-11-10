# Question
클래스 : Student

필드 : 이름, 국, 영, 수, 평균, 등급
  메소드 : 
1) setData() : 이름, 국, 영, 수를 인자값으로 받아, 해당 필드에 모두 저장
2) setMean() : 객체가 가지고 있는 국, 영, 수를 가지고 평균을 계산하여 평균 필드에 저장
3) setGrade() : 객체가 가지고 있는 평균을 가지고 등급을 저장 
90이상 : A
80이상 ~ 90미만 : B
70이상 ~ 80미만 : C
60이상 ~ 70미만 : D
60미만 : F
4) printData() : 객체의 모든 정보(이름, 국, 영, 수, 평균, 등급)를 sysout


메인 클래스 : Quiz03
4명의 학생 객체를 배열로 선언하고 반복문을 사용하여 학생들의 이름, 국, 영, 수를 입력 받음
입력이 끝나면 모든 학생의 정보를 출력
    
# SourceCode   
```java
package com.javalec.quiz;
/*
 * 클래스 : Student
 *  필드 : 이름, 국, 영, 수, 평균, 등급
 *  메소드 : 
 *    1) setData() : 이름, 국, 영, 수를 인자값으로 받아, 해당 필드에 모두 저장
 *    2) setMean() : 객체가 가지고 있는 국, 영, 수를 가지고 평균을 계산하여 평균 필드에 저장
 *    3) setGrade() : 객체가 가지고 있는 평균을 가지고 등급을 저장 
 *       90이상 : A
 *       80이상 ~ 90미만 : B
 *       70이상 ~ 80미만 : C
 *       60이상 ~ 70미만 : D
 *       60미만 : F
 * 	  4) printData() : 객체의 모든 정보(이름, 국, 영, 수, 평균, 등급)를 sysout
 * 
 *  메인 클래스 : Quiz03
 *   4명의 학생 객체를 배열로 선언하고 
 *   반복문을 사용하여 학생들의 이름, 국, 영, 수를 입력 받음
 *   입력이 끝나면 모든 학생의 정보를 출력
 */

import javax.swing.JOptionPane;

class Student{
	String name;
	int kor;
	int eng;
	int math;
	int aver;
	char grade;
	
	void setData(String name, int kor, int eng, int math) {
		this.name = name;
		this.kor = kor;
		this.eng = eng;
		this.math = math;
		this.aver = (this.kor + this.eng + this.math)/3;
	}
	
	void setGrade() {
		if(this.aver >= 90) {
			this.grade = 'A';
		}
		if(this.aver < 90 && this.aver >= 80) {
			this.grade = 'B';
		}
		if(this.aver < 80 && this.aver >= 70) {
			this.grade = 'C';
		}
		if(this.aver < 70 && this.aver >= 60) {
			this.grade = 'D';
		}
		else if(this.aver < 60) {
			this.grade = 'F';
		} 
	}
	
	void printData() {
		JOptionPane.showMessageDialog(null,
				"* 학생 정보 출력 *\n이름 : " + this.name + "\n국어 : " + this.kor + 
				"\n영어 : " + this.eng + "\n수학 : " + this.math + "\n평균 : " + this.aver + "\n등급 : " + this.grade);
	}
	
}
public class Quiz03 {
	public static void main(String[] args) {
//		4명의 학생 객체를 배열로 선언하고 
//		 *   반복문을 사용하여 학생들의 이름, 국, 영, 수를 입력 받음
//		 *   입력이 끝나면 모든 학생의 정보를 출력
		Student[] students = new Student[4]; 
		String message = "";
		
		for(int i=0; i<students.length; i++) {
			String name = JOptionPane.showInputDialog(null, "학생 이름을 입력하세요");
			int kor = Integer.parseInt(JOptionPane.showInputDialog(null, "국어 점수를 입력하세요"));
			int eng = Integer.parseInt(JOptionPane.showInputDialog(null, "영어 점수를 입력하세요"));
			int math = Integer.parseInt(JOptionPane.showInputDialog(null, "수학 점수를 입력하세요"));
			
			students[i] = new Student();
			students[i].setData(name, kor, eng, math);
			students[i].setGrade();
			message += "학생 이름 : " + students[i].name + "\n국어 점수 : " + students[i].kor + 
					"\n영어 점수 : " + students[i].eng + "\n수학 점수 : " + students[i].math + 
					"\n평균 : " + students[i].aver + "\n등급 : " + students[i].grade + "\n---------\n";
		} // 배열 길이동안 입력받은 학생 정보를 토대로 Student 객체 생성 후 배열에 넣는다.
		
		JOptionPane.showMessageDialog(null, "학생 정보 입력 완료!");
		JOptionPane.showMessageDialog(null, "*학생 정보 출력*\n" + message);
	}
}
```
