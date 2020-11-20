```java
package day19.homework;

import javax.swing.JOptionPane;

public class Quiz01 {
	public static void main(String[] args) {
		String total = "";
		boolean flag = true;
		int numOfA = 0;
		
		/*
		 1. 사용자가 -1을 입력할 때까지 문자열을 입력 받고
    	1) 입력된 문자열 중 소문자 'a'의 개수를 출력하세요.
    	2) 비출력문자(공백,엔터 등)을 제외한 문자의 총 개수를 출력하세요.
    	3) 단어의 개수를 출력하세요.
		 */
		
		while(flag) {
			String input = JOptionPane.showInputDialog(null, "문자열을 입력하세요(-1을 입력하면 종료합니다.)");
			if(input.equals("-1")) { // "-1".equals(input)이 좋음(JOptionPane인 경우 nullpointerException).
				flag = false;
				continue;
			}
			total += input;
		}
		
		// toCharArry()를 생각하지 못하고 split으로 잘라서 넣었다...
		String[] inputs = total.split("");
		for(int i=0; i<inputs.length; i++) {
			if(inputs[i].equals("a"))
				numOfA += 1;
			if(inputs[i].equals("\n")||inputs[i].equals("\t")||inputs[i].equals(" ")) { // \\s+는 1개 이상의 공백문자를 의미한다.
				inputs[i] = ""; // 공백 문자 제거하기
			}
		}
		
		total = "";
		for(String s:inputs) {
			total += s;
		}
		
		JOptionPane.showMessageDialog(null, "문자열 입력 완료!");
		JOptionPane.showMessageDialog(null, "*입력한 문자열*\n" + total + "\na의 개수 : " + numOfA);
		
		
		// 
	}

}
```
