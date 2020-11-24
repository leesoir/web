# Explain
< 국가 관리 프로그램 >
0. Nation 클래스 
필드 : 국가명(nation) 수도명(capital) 인구수(population) ==> 모두 private 
메서드 : 
Nation() 
Nation(국가, 수도)
Nation(국가, 수도, 인구수)
getter, setter 
toString() 오버라이드 

​
1. ArrayList 객체 생성 (Nation 객체들을 저장할 창고 객체) 
​

2. 메뉴 띄우기
1) 국가 추가 ==> 국가명, 수도명, 인구수 입력 받아 Nation 객체 생성 후 ArrayList에 add()
2) 모든 국가 보기 ==> 현재 등록된 국가들을 모두 출력 (for문과 Nation.toString() 활용)
3) 국가 검색 ==> 국가명을 입력 받고, 해당 국가가 있으면 수도, 인구수 출력
없으면 "미등록 국가"
인구수는 ',' 추가 ( 예) 100,000,000 명 ) 
0) 종료 

# SourceCode
```java
package day21.homework;

import java.util.ArrayList;

import javax.swing.JOptionPane;

class Nation{
	//field
	private String nation;
	private String capital;
	private int population;
	private static final DecimalFormat DECIMAL_FORMAT = new DecimalFormat("#,###");


	// construcotrs
	// only default Constructor

	//  getters and steers
	public String getNation() {
		return nation;
	}

	public void setNation(String nation) {
		this.nation = nation;
	}
	
	public String getCapital() {
		return capital;
	}
	
	public void setCapital(String capital) {
		this.capital = capital;
	}
	
	public int getPopulation() {
		return population;
	}
	
	public void setPopulation(int population) {
		this.population = population;
	}


	//methods
	@Override
	public String toString() {
		return "국가명 : " + this.getNation() + "\n수도명 : " + this.getCapital() + 
				"\n인구수 : " + DECIMAL_FORMAT.format(getPopulation()) + "\n";
	}
}

public class Quiz01 {
	public static void main(String[] args) {
		boolean flag = true;
		ArrayList<Nation> arr = new ArrayList<>();

		while(flag) {
			String input = JOptionPane.showInputDialog("1. 국가 추가\n2. 모든 국가 보기\n3. 국가 검색\n0. 종료");

			switch(input) {
			case "1":{ // 국가 추가
				String nation = JOptionPane.showInputDialog("국가명을 입력하세요");
				String capital = JOptionPane.showInputDialog("수도명을 입력하세요");
				int population = Integer.parseInt(JOptionPane.showInputDialog("인구수를 입력하세요"));

				Nation people = new Nation();
				Nation people = new Nation(nation, capital, population);
				arr.add(people);
				break;
			}

			case "2":{ // 모든 국가 보기
				if(arr.isEmpty()) {
					JOptionPane.showMessageDialog(null, "데이터가 존재하지 않습니다.");
					break;
				}
				JOptionPane.showMessageDialog(null, "*모든 국가 보기*\n" + arr); // arr.toString()
				break;
			}

			case "3":{ // 국가 검색
				if(arr.isEmpty()) { // NullPointerException 
					JOptionPane.showMessageDialog(null, "데이터가 존재하지 않습니다.");
					break;
				}
				
				String inputNation = JOptionPane.showInputDialog("*국가명 찾기* \n국가명을 입력하세요");
				
				boolean isthere = false;
				for(Nation n:arr) {
					if(n.getNation().equals(inputNation)) {
						JOptionPane.showMessageDialog(null, inputNation + "\n수도명 : " + n.getCapital() + "\n인구수 : " + n.getPopulation());
						isthere = true;
						break;
					}
				}
				if(isthere == false) {
					JOptionPane.showMessageDialog(null, "찾는 국가명이 존재하지 않습니다.");
				}
				break;
			}

			case "0":{ // 종료
				JOptionPane.showMessageDialog(null, "종료합니다.");
				flag = false;
				break;
			}
			
			default:{
				JOptionPane.showConfirmDialog(null, "잘못된 입력입니다!");
				break;
			}
			}
		}
	}

}
```

# Review
