```java
package day25.homework;

import java.util.HashMap;
import java.util.Map.Entry;
import java.util.Scanner;
import java.util.TreeMap;
import java.util.regex.Pattern;

import javax.swing.JOptionPane;

/*

< 학생 관리 프로그램 >

step 1. 다음 학생들의 정보를 Map 에 저장하세요. (TreeMap<Integer,HashMap<String,Object>>)
key 는 학번(Integer)입니다.

주의) Student 클래스를 사용하지 않고 학생 정보도 Map을 사용합니다. 
{
	101 : {"name":"홍길동", "average":88, "grade":"B", "contact":"010-2222-1231"},
	102 : {"name":"김길동", "average":92, "grade":"A", "contact":"010-2231-1256"},
	103 : {"name":"김장미", "average":47, "grade":"F", "contact":"010-2512-7754"},
	...
}

학번          이름      평균      등급      연락처
101         홍길동      88       B        010-2222-1231
102         김길동      92       A        010-2231-1256
103         김장미      47       F        010-2512-7754
201         장아름      85       B        010-9966-3512
202         최영수      74       C        010-1111-3864

step 2. (1)의 딕셔너리에 학생 3명의 정보를 입력 받아 추가 저장합니다.
    - 학생의 이름, 국, 영, 수, 학년, 연락처를 입력 받습니다.

    - 학년은 학번의 가장 앞자리에 해당합니다.
      예를 들어 딕셔너리에 저장된 2학년 학생이 4명이라면, 다음 2학년 학생의 학번은 205가 되어야 합니다.
  (1 <= 학년 <= 6)	
  (0 <= 학년 당 학생의 수 < 100)

    - 평균은 국,영,수 의 평균을 계산하여 저장합니다.
        *사용자에게 입력 받지 않습니다.

    - 등급은 평균에 따른 A, B, C, D, F 중 하나로 저장합니다.
        *사용자에게 입력 받지 않습니다.
        90 점 이상 : A
        80점 이상 ~ 90점 미만 : B
        70점 이상 ~ 80점 미만 : C
        60점 이상 ~ 70점 미만 : D
        60점 미만 : F

step 3. 사용자 메뉴를 출력합니다. (선택문제)
    1. 학번으로 검색
    2. 연락처 뒷번호로 검색
    3. 1등 학생 보기
    4. 모든 학생 보기
    0. 종료

    1. 학번으로 검색
        학번을 입력 받고 해당 학생의 모든 정보를 출력합니다.
        미등록 학번인 경우 '미등록 학번'을 출력합니다.

    2. 연락처 뒷번호로 검색
        연락처 뒷번호 4자리를 입력 받아 연락처가 일치하는
        '모든' 학생들의 이름, 학년, 연락처를 출력합니다.

    3. 1등 학생 보기
        평균을 가지고 1등 학생을 찾아 해당 학생의 학번, 이름, 평균 점수를 출력합니다.
        공동 1등인 경우 학년이 가장 높은 학생을,
        그 중 같은 학년에 공동 1등이 있다면 그 학생들 모두를 출력하세요.

    4. 모든 학생 보기
        현재 등록되어있는 모든 학생들의 모든 정보를 출력하세요.

*/
public class Homework01 {

	private TreeMap<Integer, HashMap<String, Object>> treeMap = new TreeMap<>();
	private int[] grades = new int[] { 100, 200, 300, 400, 500, 600 };

	// saveInfo(int 학년, String 이름, double 평균, String 연락처)
	private void saveInfo(int year, String name, int avg, String tel) {
		// 학번 생성 (key)
		Integer id = ++grades[year - 1];

		// 학생 정보 생성 (value)
		HashMap<String, Object> map = new HashMap<>();
		map.put("name", name);
		map.put("average", avg);
		map.put("grade", getGrade(avg));
		map.put("contact", tel);

		// key-value 쌍을 전체 학생 맵(TreeMap)에 저장
		treeMap.put(id, map);
	}

	private String getGrade(double avg) {
		switch ((int) avg / 10) {
		case 10:
		case 9:
			return "A";
		case 8:
			return "B";
		case 7:
			return "C";
		case 6:
			return "D";
		default:
			return "F";
		}
	}

	private int getAvg(int k, int e, int m) {
		return (k + e + m) / 3;
	}

	private void step01() {
		saveInfo(1, "홍길동", 88, "010-2222-1231");
		saveInfo(1, "김길동", 92, "010-2231-1256");
		saveInfo(1, "김장미", 47, "010-2512-7754");
		saveInfo(2, "장아름", 85, "010-9966-3512");
		saveInfo(2, "피카츄", 92, "010-1111-3864");
		saveInfo(2, "최영수", 74, "010-2222-3864");
		saveInfo(2, "푸린", 92, "010-3333-3864");
		// System.out.println("DEFAULT INFO : " + treeMap);
	}

	private void step02() {
		Scanner sc = new Scanner(System.in);
		String name;
		int kr, en, ma;
		String contact;
		int year;
		for (int i = 0; i < 3; ++i) {
			try {
				System.out.print("이름 : ");
				name = sc.next();
				System.out.print("학년 : ");
				year = sc.nextInt();
				if (year < 1 || year > 6) {
					throw new Exception("학년은 1 ~ 6학년까지만 입력 가능합니다.");
				}

				System.out.print("연락처 : ");

				contact = sc.next();
				if (!Pattern.matches("^01(?:0|1|[6-9])-(?:\\d{4})-\\d{4}$", contact)) {
					throw new Exception("XXX-XXXX-XXXX 형식으로 연락처를 기입해주세요.");
				}

				System.out.print("국/영/수 : ");
				kr = sc.nextInt();
				en = sc.nextInt();
				ma = sc.nextInt();

				saveInfo(year, name, getAvg(kr, en, ma), contact);
			} catch (Exception e) {
				System.out.println(e.getMessage());
				System.out.println("처음부터 다시 입력하세요.");
				--i;
			}
		}
	}

	private void menu01() {
		int id = Integer.parseInt(JOptionPane.showInputDialog("검색 학번"));
		if (treeMap.containsKey(id)) {
			JOptionPane.showMessageDialog(null, treeMap.get(id));
		} else {
			JOptionPane.showMessageDialog(null, "미등록 학번");
		}
	}

	private void menu02() {
		String tel = JOptionPane.showInputDialog("연락처 뒷자리 4자리 입력");
		StringBuffer sb = new StringBuffer();
		for (Entry<Integer, HashMap<String, Object>> en : treeMap.entrySet()) {
			String contact = (String) en.getValue().get("contact");
			if (contact.endsWith(tel)) {
				sb.append("학번 : " + en.getKey() + "" + en.getValue() + "\n");
			}
		}
		if (sb.toString().isEmpty()) {
			sb.append("검색 결과가 없습니다.");
		}
		JOptionPane.showMessageDialog(null, sb);
	}

	private void menu03() {
		// 최대 점수를 가진 학생 map
		Entry<Integer, HashMap<String, Object>> maxEntry = null;
		for(Entry<Integer, HashMap<String, Object>> entry : treeMap.entrySet()) {
			if(maxEntry == null) {
				maxEntry = entry;
				continue;
			}
			
			int maxAverage = (int)maxEntry.getValue().get("average");
			int average = (int)entry.getValue().get("average");
			if(maxAverage <= average) {
				maxEntry = entry;
				continue;
			}
		}
		
		// 위 for문 통해 가장 큰 평균 + 그 중 가장 높은 학년
		int year = (int)(maxEntry.getKey()) / 100; // 학년 
		int average = (int)maxEntry.getValue().get("average"); // 평균 점수
		
		
		// 최고 점수의 최고 학년이 3이다. (year:3)
		// grades[2] <== 3학년의 마지막 학번
		
		TreeMap<Integer, HashMap<String, Object>> map = new TreeMap<>();
		for(int i = (year*100)+1; i <= grades[year-1]; ++i) {
			HashMap<String, Object> iMap = treeMap.get(i);
			if(average != (int)iMap.get("average")) {
				continue;
			}
			map.put(i, iMap);
		}
		
		StringBuffer sb = new StringBuffer();
		for(Integer key : map.keySet()) {
			sb.append("학번 : " + key + map.get(key) + "\n");
		}
		JOptionPane.showMessageDialog(null, sb);
	}
	
	private void menu04() {
		StringBuffer sb = new StringBuffer();
		for (Entry<Integer, HashMap<String, Object>> en : treeMap.entrySet()) {
			sb.append("학번 : " + en.getKey() + "" + en.getValue() + "\n");
		}
		if (sb.toString().isEmpty()) {
			sb.append("등록 정보가 없습니다.");
		}
		JOptionPane.showMessageDialog(null, sb);
	}

	private void step03() {
		String menu = "1. 학번으로 검색\r\n" + "2. 연락처 뒷번호로 검색\r\n" + "3. 1등 학생 보기\r\n" + "4. 모든 학생 보기\r\n" + "0. 종료";
		String select = null;
		while (true) {
			select = JOptionPane.showInputDialog(menu);
			switch (select) {
			case "0":
				JOptionPane.showMessageDialog(null, "프로그램을 종료합니다.");
				System.exit(0);
			case "1": // 1. 학번으로 검색
				menu01();
				break;
			case "2": // 2. 연락처 뒷번호로 검색
				menu02();
				break;
			case "3":
				menu03();
				break;
			case "4":
				menu04();
				break;
			default:
				JOptionPane.showMessageDialog(null, "다시 입력하세요.");
				break;
			}

		}
	}

	public Homework01() {
		step01();
		//step02();
		step03();

	}

	public static void main(String[] args) {
		new Homework01();
	}
}
```
