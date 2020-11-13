# Explain
main에 들어간 코드들을 전부 메소드로 빼 주고, 클래스의 생성자를 만들어 생성자 실행 시 while문이 동작하게 하였다.
main() 메소드에서는 클래스 생성자를 통해 while문이 동작하고, while문의 siwtch문에는 케이스마다 코드 대신 빼준 메소드만 호출하여 결과적으로는 이전과 동일하게 프로그램이 동작하게 된다.
그러나 1보다는 더 구조적이게 된 클래스

# SourceCode
```java
package day14.quiz;

import java.text.DecimalFormat;

import javax.swing.JOptionPane;

public class Quiz02 {
	private Tourist[] tourists = new Tourist[5];
	private int count=0;
	private static boolean flag = true;
	private int vipNum = 0;

	public Quiz02() {
		while(flag) {
			int input = Integer.parseInt(JOptionPane.showInputDialog
					("1. 목적지 설정\n2. 여행객 추가\n3. 모든 여행객 정보 보기\n4. 전체 예산 보기\n5. VIP 조회\n0. 종료"));

			switch(input) {
			case 1:{ // 목적지 설정
				menu1();
				break;
			}

			case 2:{ // 여행객 추가하기
				menu2();
				break;
			}

			case 3:{ // 모든 여행객 정보 보기
				menu3();
				break;
			}

			case 4:{ // 예산 총합 보기
				menu4();
				break;
			}

			case 5:{ // vip 조회
				menu5();
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

	private void menu1() {
		String destination = JOptionPane.showInputDialog("*목적지 설정*\n목적지를 입력하세요.");
		Tourist.setDestination(destination);
	}

	private void menu2() {
		if(count == tourists.length) {
			JOptionPane.showMessageDialog(null, "여행 인원을 초과하였습니다.");
			return;
		}

		tourists[count] = new Tourist(JOptionPane.showInputDialog("*여행객 추가*\n이름"), 
				Integer.parseInt(JOptionPane.showInputDialog("*여행객 추가*\n예산")));
		count++;
		JOptionPane.showMessageDialog(null, "저장 완료!");
	}

	private void menu3() {
		String message = "*모든 여행객 정보 보기*\n목적지 : " + Tourist.getDestination() + "\n";
		for(Tourist t:tourists) {
			if(null == t) {
				return;
			} 
			message += t; 
		}
		JOptionPane.showMessageDialog(null, message);
	}

	private void menu4() {
		int budSum=0;
		for(Tourist t:tourists) {
			if(null == t) 
				break;
			budSum += t.getBudget();
		}
		DecimalFormat df = new DecimalFormat("###,###");
		JOptionPane.showMessageDialog(null, "*전체 예산 보기*\n전체 예산 : "+ df.format(budSum));
	}

	private void menu5() {
		if(count == 0) {
			JOptionPane.showMessageDialog(null, "여행객이 없습니다.");
			return;
		}
		int max=tourists[0].getBudget();

		for(int i=1; i<tourists.length; i++) {
			if(null == tourists[i]) 
				break; // check : 이 처리 안하고 i<count-1까지만 해도 괜찮음. count-1는 현재 객체가 생성된 인덱스값을 의미한다.

			if(tourists[i].getBudget() > max) {
				vipNum = i;
			}
		}

		JOptionPane.showMessageDialog(null, "*VIP 조회*\n" + 
				tourists[vipNum]);
	}


	public static void main(String[] args) {
		new Quiz02();
	}

}
```
