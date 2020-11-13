# Explain
Tourist 클래스와 main 클래스를 만든다.

Tourist   
(1) 필드 : name, budget(예산), destination(목적지)   
(2) 메소드 : constructor, getter, setter, 여행자 정보를 출력하는 printInfo()

main() : 메뉴 -> 1. 목적지 설정 2. 여행객 추가 3. 모든 여행객 정보 보기 4. 전체 예산 보기 5. VIP 조회 0. 종료

조건 : 여행객은 최대 5명까지 받는다. 모든 여행객의 목적지는 동일하며, 예산이 가장 많은 여행객을 VIP로 한다.

# Tourist.java
```java
package day14.quiz;

import javax.swing.JOptionPane;

public class Tourist {
	private String name; // 여행객 이름
	private int budget; // 여행객의 예산
	public static String destination; // 목적지
	
//	static {
//		destination = JOptionPane.showInputDialog("목적지를 입력하세요.");
//	} // static block을 만들어 initializing할 경우 
	
	// constructors
	Tourist(String name, int budget, String destination){
		setName(name);
		setBudget(budget);
		Tourist.destination = destination;
	}
	
	Tourist(String name, int budget){
		this(name, budget, Tourist.destination);
	}
	
	Tourist(String name){
		this(name, 0, Tourist.destination);
	}
	
	
	// getters and setters
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getBudget() {
		return budget;
	}
	public void setBudget(int budget) {
		this.budget = budget;
	}
	
	
	//methods
	public String printInfo() {
		String message = "";
		message += "이름 : " + this.getName() + "\n예산 : " + 
				this.getBudget() + "\n";

		//		JOptionPane.showMessageDialog(null, message); 
		// JOptionPane과의 결합도가 높다. toString() 활용하기
		// check: 결합도는 낮췄는데 toString을 어떻게 활용해야 할지 모르겠다
		return message;
	}
	
}
```

# main.java
```java
package day14.quiz;
import javax.swing.JOptionPane;

public class Quiz01 {
	public static void main(String[] args) {
		Tourist[] tourists = new Tourist[5];
		int count=0;
		boolean flag = true;
		int vipNum = 0;

		while(flag) {
			int input = Integer.parseInt(JOptionPane.showInputDialog
					("1. 목적지 설정\n2. 여행객 추가\n3. 모든 여행객 정보 보기\n4. 전체 예산 보기\n5. VIP 조회\n0. 종료"));

			switch(input) {
			case 1:{
				String destination = JOptionPane.showInputDialog("*목적지 설정*\n목적지를 입력하세요.");
				Tourist.destination = destination;
				break;
        
        //Tourist.destination;
        //break;
				// Think : static block을 이용해서 위의 case문에는 Tourist.destination만 작성하고 싶었는데 이러면 오류난다. 
				// teacher: 메소드를 호출하지 않고, 그냥 변수 자체만 나열하기 때문에 의미가 없다(참조가 안 되는것 같다). 이러한 문장은 bad code다.
			}

			case 2:{
				String name = JOptionPane.showInputDialog("*여행객 추가*\n이름");
				int budget = Integer.parseInt(JOptionPane.showInputDialog("*여행객 추가*\n예산"));

				if(count == tourists.length) {
					JOptionPane.showMessageDialog(null, "여행 인원을 초과하였습니다.");
					break;
				}

				tourists[count] = new Tourist(name, budget, Tourist.destination);
				count++;
				break;
			}

			case 3:{
				String message = "*모든 여행객 정보 보기*\n목적지 : " + Tourist.destination + "\n";
				for(Tourist t:tourists) {
					if(null == t) {
						break;
					}
					message += t.printInfo();
				}
				JOptionPane.showMessageDialog(null, message);
				break;
			}

			case 4:{
				int budSum=0;
				for(Tourist t:tourists) {
					if(null == t) // exception 처리
						break;
					budSum += t.getBudget();
				}
				JOptionPane.showMessageDialog(null, "*전체 예산 보기*\n전체 예산 : "+ budSum);
				break;
			}

			case 5:{
				int max=tourists[0].getBudget();

				for(int i=1; i<tourists.length; i++) {
					if(null == tourists[i]) 
						break; 
					
					if(tourists[i].getBudget() > max) {
						max = tourists[i].getBudget();
						vipNum = i;
					}
				}

				JOptionPane.showMessageDialog(null, "*VIP 조회*\n이름 : " + 
						tourists[vipNum].getName() + "\n예산 : " + max);
				break;
			}

			case 0:{
				JOptionPane.showMessageDialog(null, "종료합니다.");
				flag = false;
				break;
			}

			default:{
				JOptionPane.showConfirmDialog(null, "잘못된 입력입니다.");
				break;
			}
			}
		}
	}

}
```


# Think
NullPointerException 처리에 주의하자.
이 예외처리를 안해줘서 실행하면 자꾸 오류가 났다. 
tourists는 이미 길이가 정해진 배열이기 때문에, 3, 4, 5의 for문에서 객체가 할당되지 않은 인덱스 값을 참조하면(즉 null값 참조) nullPointerException이 발생하게 된다. 
저번에도 했던 실수인데 이번에도 체크 못 했다. 다음에 하면 꼭 신경쓰기.
