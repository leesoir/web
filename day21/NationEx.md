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
		return "국가명 : " + this.getNation() + "\n수도명 : " + this.getCapital() + "\n인구수 : " + this.getPopulation() + "\n";
	}
	
	public void makePeople(String nation, String capital, int population) {
		this.setNation(nation);
		this.setCapital(capital);
		this.setPopulation(population);
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
				people.makePeople(nation, capital, population);

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
				String inputNation = JOptionPane.showInputDialog("*국가명 찾기* \n국가명을 입력하세요");
				
				for(Nation n:arr) {
					if(n.getNation().equals(inputNation)) {
						JOptionPane.showMessageDialog(null, inputNation + "\n수도명 : " + n.getCapital() + "\n인구수 : " + n.getPopulation());
						break;
					}
					
//					if( == arr.size()-1) {
//						JOptionPane.showMessageDialog(null, "찾는 국가명이 존재하지 않습니다.");
//					}
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
