```java
package com.javalec.quiz;

import javax.swing.JOptionPane;

/*
 * 클래스 : MyMath
 *  - 필드 : 없음
 *  - 메소드 
 *    1) getTotal()	: 정수 1개를 인자값으로 받고, 1 부터 그 수까지의 모든 합을 return
 *      e.g. 인자값 : 5 -> 리턴값 : 10
 *           인자값 : 3 -> 리턴값 : 6
 *    2) getGugudan() : 정수 1개를 인자값으로 받고, 해당 단을 String형태로 return 
 *  
 * 메인 클래스 : Quiz02
 * 	메뉴 : 
 *    1. 총합 구하기
 *    2. 구구단 보기
 *    3. 종료하기
 *  - 1번 선택 시 : 정수 1개를 입력 받아 1 ~ 정수까지의 합 출력
 *  - 2번 선택 시 : 정수 1개를 입력 받아 해당 단 출력
 *  - 3번 선택 시 : 프로그램 종료 
 *    (3번을 선택해야 메뉴창 띄우기를 반복 종료함.)
 */
class MyMath {
	int getTotal(int num){
		int sum = 0;
		for(int i=1; i<=num; i++) {
			sum += i;
		}
		return sum;
	}
	
	String getGugudan(int dan) {
		String gugudan="";
		for(int i=1;i<=9; i++) {
			gugudan += Integer.toString(dan) + " X " + Integer.toString(i) + " = " + Integer.toString(dan*i) + "\n";
		}
		return gugudan;
	}
}


public class Quiz02 {
	public static void main(String[] args) {
		boolean flag = true;
		MyMath ma = new MyMath();
		
		while(flag) {
			String input = JOptionPane.showInputDialog(null, "1. 총합 구하기\n2. 구구단 보기\n3. 종료하기");
			switch(input) {
			case "1":{ // 총합 구하기
				int num = Integer.parseInt(JOptionPane.showInputDialog(null, "수를 입력하세요"));
				JOptionPane.showMessageDialog(null, ma.getTotal(num));
				break;
			}
			
			case "2":{ // 구구단 보기
				int dan = Integer.parseInt(JOptionPane.showInputDialog(null, "단을 입력하세요"));
				JOptionPane.showMessageDialog(null, ma.getGugudan(dan));
				break;
			}
			
			case "3":{ // 프로그램 종료
				JOptionPane.showMessageDialog(null, "프로그램을 종료합니다.");
				flag = false;
				break;
			}
			
			default:{
				JOptionPane.showMessageDialog(null, "잘못된 값을 입력하셨습니다.");
				break;
			}
			}
		}
	}
}
```
