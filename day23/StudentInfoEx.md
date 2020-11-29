# Explain
< 학생 관리 프로그램 >

​

step 1. 다음 학생들의 정보를 Map 에 저장하세요. 
(TreeMap<Integer, HashMap<String, Object>>)

​
key 는 학번(Integer)입니다.

주의) Student 클래스를 사용하지 않고 학생 정보도 Map을 사용합니다. 

{

101 : {"name":"홍길동", "average":88, "grade":"B", "contact":"010-2222-1231"},

102 : {"name":"김길동", "average":92, "grade":"A", "contact":"010-2231-1256"},

103 : {"name":"김장미", "average":47, "grade":"F", "contact":"010-2512-7754"},
...
}

​
학번 이름 평균 등급 연락처

101 홍길동 88 B 010-2222-1231

102 김길동 92 A 010-2231-1256

103 김장미 47 F 010-2512-7754

201 장아름 85 B 010-9966-3512

202 최영수 74 C 010-1111-3864

​

step 2. (1)의 딕셔너리에 학생 3명의 정보를 입력 받아 추가 저장합니다.

- 학생의 이름, 국, 영, 수, 학년, 연락처를 입력 받습니다.

​

- 학년은 학번의 가장 앞자리에 해당합니다.
예를 들어 딕셔너리에 저장된 2학년 학생이 4명이라면, 다음 2학년 학생의 학번은 205가 되어야 합니다.

(1 <= 학년 <= 6) 

(0 <= 학년 당 학생의 수 < 100)

​

- 평균은 국,영,수 의 평균을 계산하여 저장합니다.
*사용자에게 입력 받지 않습니다.

​

- 등급은 평균에 따른 A, B, C, D, F 중 하나로 저장합니다.

*사용자에게 입력 받지 않습니다.

90 점 이상 : A

80점 이상 ~ 90점 미만 : B

70점 이상 ~ 80점 미만 : C

60점 이상 ~ 70점 미만 : D

60점 미만 : F

​

step 3. 사용자 메뉴를 출력합니다. (선택문제)

1. 학번으로 검색

2. 연락처 뒷번호로 검색

3. 1등 학생 보기

4. 모든 학생 보기

0. 종료

​

1. 학번으로 검색

학번을 입력 받고 해당 학생의 모든 정보를 출력합니다.
미등록 학번인 경우 '미등록 학번'을 출력합니다.

​

2. 연락처 뒷번호로 검색

연락처 뒷번호 4자리를 입력 받아 연락처가 일치하는

'모든' 학생들의 이름, 학년, 연락처를 출력합니다.

​

3. 1등 학생 보기

평균을 가지고 1등 학생을 찾아 해당 학생의 학번, 이름, 평균 점수를 출력합니다.

공동 1등인 경우 학년이 가장 높은 학생을,

그 중 같은 학년에 공동 1등이 있다면 그 학생들 모두를 출력하세요.

​

4. 모든 학생 보기

현재 등록되어있는 모든 학생들의 모든 정보를 출력하세요.

​

# Check
## 11.29
check 1 : 반복문을 통해 넣은 마지막 객체의 정보로 모든 학생 객체들이 reset된다.
check 2 : 연락처 뒷자리로 찾기 시, 존재하는 번호의 뒷자리를 입력해도 아무 것도 출력하지 않고 해당 메소드가 끝난다(menu02).

# SourceCode
```java
package day23.homework;

import java.util.HashMap;
import java.util.Map;
import java.util.Set;
import java.util.TreeMap;

import javax.swing.JOptionPane;

public class Quiz01 {
	private static Map<Integer, HashMap<String, Object>> map = new TreeMap<>();
	Set<Integer> keyset = map.keySet();
	static int level1 = 103; // 1학년의 마지막 학번
	static int level2 = 202; // 2학년의 마지막 학번
	// map의 구조는 학번, 학생정보(HashMap)

	//methods
	private static String setGrade(int average) {
		String grade;

		if(average > 90 && average <= 100) {
			grade = "A";
		}else if(average > 80) {
			grade = "B";
		}else if(average > 70) {
			grade = "C";
		}else if(average > 60) {
			grade = "D";
		}else grade = "F";

		return grade;
	}

	private void menu01() { // 1. 학번으로 검색
		int id = Integer.parseInt(JOptionPane.showInputDialog("학번을 입력하세요."));
		
		if(id == 0) {
			return;
		}
		
		if(map.containsKey(id)) {
			JOptionPane.showMessageDialog(null, "*학생 정보 확인*\n" + map.get(id));
			return;
		}
		JOptionPane.showMessageDialog(null, "학번에 해당하는 학생이 없습니다.");
		return;
	}

	private void menu02() { // 2. 연락처 뒷번호로 검색
		String num = JOptionPane.showInputDialog("연락처 뒷번호를 입력하세요.");
		if(num == null) {
			return;
		}
		// 1="101" 이런 식으로 있을거

		// 연락처 substring() 값이 num과 같은 hashMap 객체를 가진 map의 key값을 가져오기.
		for(int s:keyset) {
			if(((String) map.get(s).get("contact")).substring(9).equals(num)) {
				System.out.println("*학생정보 출력*\n" + map.get(s));
			}
		}
	}

	private void menu03() { // 3. 1등 학생 보기
		int max = 0;
		HashMap<String, Object> top = null;
		// map을 보면서 가장 aver가 높은 학생을 찾아야 함.

		JOptionPane.showMessageDialog(null, "*1등 학생 보기*\n");
		Set<Integer> keyset = map.keySet();

		for(int s:keyset) {
			// map을 돌기
			if((int)(map.get(s).get("average")) > max) {
				max = (int)(map.get(s).get("average"));
				top = map.get(s);
			}
		}

		JOptionPane.showMessageDialog(null, top);
	}

	private void menu04() { // 4. 모든 학생 보기
		JOptionPane.showMessageDialog(null, "*모든 학생 보기*\n");
		String message="";

		for(int s:keyset) {
			message += map.get(s);
		}
		// check : 마지막으로 추가한 학생의 이름으로 모든 key의 name값이 변경된다.

		JOptionPane.showMessageDialog(null, message);
	}

	public Quiz01() {
		String select;

		map.put(101, null);
		map.put(102, null);
		map.put(103, null);
		map.put(201, null);
		map.put(202, null);

		HashMap<String, Object> hash = new HashMap<>();

		hash.put("name", "홍길동");
		hash.put("average", 88);
		hash.put("grade", 'B');
		hash.put("contact", "010-2222-1231");
		map.put(101, hash);

		hash.put("name", "김길동");
		hash.put("average", 92);
		hash.put("grade", 'A');
		hash.put("contact", "010-2231-1256");
		map.put(102, hash);

		hash.put("name", "김장미");
		hash.put("average", 47);
		hash.put("grade", 'F');
		hash.put("contact", "010-2512-7754");
		map.put(103, hash);

		hash.put("name", "장아름");
		hash.put("average", 85);
		hash.put("grade", 'B');
		hash.put("contact", "010-9966-3512");
		map.put(201, hash);

		hash.put("name", "최영수");
		hash.put("average", 74);
		hash.put("grade", 'C');
		hash.put("contact", "010-1111-3864");
		map.put(202, hash);


		JOptionPane.showMessageDialog(null, "학생 정보 사전등록 완료! \n3명의 학생정보를 추가로 입력합니다.");
		// 1. 학생 3명의 정보를 입력 받아 추가 저장하기
		for(int i=0; i<3; i++){
			String name = JOptionPane.showInputDialog("이름을 입력하세요.");
			int kor = Integer.parseInt(JOptionPane.showInputDialog("국어 점수를 입력하세요."));
			int eng = Integer.parseInt(JOptionPane.showInputDialog("영어 점수를 입력하세요."));
			int math = Integer.parseInt(JOptionPane.showInputDialog("수학 점수를 입력하세요."));
			int level = Integer.parseInt(JOptionPane.showInputDialog("학년을 입력하세요."));
			String contact = JOptionPane.showInputDialog("연락처를 입력하세요.");

			int aver = (kor+eng+math)/3;
			String grade = setGrade(aver);

			// 학번, 이름, 평균, 등급, 연락처

			hash.put("name", name);
			hash.put("average", aver);
			hash.put("grade", grade);
			hash.put("contact", contact);

			if(level == 1) {
				map.put(++level1, hash);
			} // 학년이 1이면 104가 됨

			if(level == 2) {
				map.put(++level2, hash);
			} // 학년이 2이면 203이 됨
		}


		// 메뉴 출력하기
		menu : while(true) {
			select = JOptionPane.showInputDialog("1. 학번으로 검색\n2. 연락처 뒷번호로 검색\n3. "
					+ "1등 학생 보기\n4. 모든 학생 보기\n0. 종료");

			switch(select) {
			// check 2 : 어떤 search를 해도 마지막에 map에 put한 학생 객체가 나온다.

			case "0":{
				JOptionPane.showMessageDialog(null, "프로그램을 종료합니다.");
				break menu;
			}
			case "1":{
				menu01();
				break;
			}

			case "2":{
				menu02();
				break;
			}

			case "3":{ //1등 학생 보기
				menu03();
				break;
			}

			case "4":{ // 모든 학생 보기
				menu04(); 
				break;
			}
			}

		}

	}


	public static void main(String[] args) {
		new Quiz01();
	}
}
```
