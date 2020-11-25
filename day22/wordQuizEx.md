# Explain		
String menu = "1. 단어 추가\n" 
				+ "2. 단어 검색\n" 
				+ "3. 모든 단어 보기\n"
				+ "4. 퀴즈 풀기 \n"
				+ "0. 종료\n입력 : ";


1 : 영단어, 그의 뜻(한글) 을 입력 받고 단어장(Map)에 저장

2 : 영단어 입력 받고 그의 뜻을 출력. 없으면 "미등록 단어" 출력  (containsKey("apple")) 

3 : for문 사용 

4 : (선택문제) 

문제 : 뜻   / 답 : 영단어  

예) 사과(은)는 영어로? ==> 'home' 입력 ==> 땡!

문제는 랜덤하게 나와야 함. Map --> List 나 array 로 변경해야 함



# Sourcede
from soir
```java
package day22.homework;

import java.util.Map;
import java.util.Random;
import java.util.Map.Entry;
import java.util.Set;
import java.util.TreeMap;

import javax.swing.JOptionPane;

public class Quiz01 {
	private Map<String, String> map;
	Random r = new Random();

	@Override
	public String toString() {
		return super.toString() + "\n";
	}

	private void menu01() { // 단어 추가
  
		if(null == map) {
			return;
		}

		String word = null;
		String meaning = null;

		while(true) {
			word = JOptionPane.showInputDialog("단어를 입력하세요(한글)");
			if(word.equals("")) {
				JOptionPane.showMessageDialog(null, "단어가 비었습니다. 다시 입력하세요");
				continue;
			}
			while(true) {
				meaning = JOptionPane.showInputDialog("영단어를 입력하세요");
				if(meaning.equals("")) {
					JOptionPane.showMessageDialog(null, "단어가 비었습니다. 다시 입력하세요");
					continue;
				}
				break;
			}
			break;
		}

		map.put(word, meaning);
		JOptionPane.showMessageDialog(null, "추가 완료!");
	}


	private void menu02() { // 단어 검색
		if(map == null || map.isEmpty()) {
			JOptionPane.showMessageDialog(null, "단어장이 비었습니다.");
			return;
		}

		String key = JOptionPane.showInputDialog("찾는 단어를 입력하세요:");
		Set<String> keys = map.keySet();
		if(keys.contains(key)) {
			JOptionPane.showMessageDialog(null, key+"는 영어로 " + map.get(key) + "입니다.");
		} else {
			JOptionPane.showMessageDialog(null, "찾는 단어가 존재하지 않습니다.");
		}
	}


	private void menu03() { // 모든 단어 보기
		Set<Entry<String, String>> allWords = map.entrySet();
		JOptionPane.showMessageDialog(null, "*단어장*\n" + allWords);
	}


	private void menu04() { // 퀴즈 풀기
		Object[] keys = map.keySet().toArray(); // 키값을 모아 배열으로 변환
		int ran = r.nextInt(map.size());
		String answer = JOptionPane.showInputDialog(keys[ran] + "는(은) 영어로? ");
		if(answer.equalsIgnoreCase(map.get(keys[ran]))) { // 대소문자 무시
			JOptionPane.showMessageDialog(null, "정답입니다!");
		} else {
			JOptionPane.showMessageDialog(null, "틀렸습니다! 정답은 " + map.get(keys[ran]) + "입니다.");
		}
	}


	public Quiz01() {

		map = new TreeMap<>();

		String menu;
		String select;

		menu = "1. 단어 추가\n2. 단어 검색\n3. 모든 단어 보기\n4. 퀴즈 풀기\n0. 종료\n입력 :";
		loop:while(true) {
			select=JOptionPane.showInputDialog(menu);

			switch(select) {
			case "0":{ // 종료
				break loop;
			}

			case "1":{ // 단어 추가
				menu01();
				break;
			}

			case "2":{ // 단어 검색
				menu02();
				break;
			}

			case "3":{ // 모든 단어 보기
				menu03();
				break;
			}

			case "4":{ //퀴즈 풀기
				menu04();
				break;
			}

			default:{
				JOptionPane.showMessageDialog(null, "잘못된 입력입니다.");
			}
			}
		}

		JOptionPane.showMessageDialog(null, "프로그램을 종료합니다.");
	}

	public static void main(String[] args) {
		new Quiz01();
	}

}
```
