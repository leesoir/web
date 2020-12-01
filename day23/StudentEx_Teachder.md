# SourceCode
```java
package day23.homework_teacher;

import java.util.HashMap;
import java.util.Map.Entry;
import java.util.Scanner;
import java.util.TreeMap;
import java.util.regex.Pattern;

import javax.swing.JOptionPane;


public class Quiz01 {
	
	private TreeMap<Integer, HashMap<String, Object>> treeMap = new TreeMap<>();
	// 학생 정보를 저장할 TreeMap 객체 treeMap
	
	private int[] years = new int[] {100, 200, 300, 400, 500, 600};
	// 학번 정보를 저장한 학번배열
	

	//methods
	// int 학년, String 이름, double 평균, String 연락처 -> 를 treeMap에 저장해주는 메소드 
	private void saveInfo(int year, String name, int aver, String tel) {
		
		// 학번 생성(key)
		Integer id = ++years[year-1]; // 학년에 위치한 값 -1
		
		// 학생 정보 생성(value)
		HashMap<String, Object> map = new HashMap<>();
		map.put("name", name);
		map.put("average", aver);
		map.put("grade", getGrade(aver));
		map.put("contact", tel);
		
		// key-value 쌍을 전체 학생 맵(treeMap)에 put
		treeMap.put(id, map);
	}
	
	private String getGrade(double aver) {
		switch((int)(aver/10)){
			case 10: 
			case 9:
				return "A";
			case 8:
				return "B";
			case 7:
				return "B";
			case 6:
				return "B";
			default:
				return "F";
		}
	}
	
	private int getAver(int k, int e, int m) {
		int average = (k+e+m) / 3;
		return average;
	}
	
	private void step01() { // setDefaultInfo
		saveInfo(1, "홍길동", 88, "010-2222-1231");
		saveInfo(1, "김길동", 92, "010-2231-1256");
		saveInfo(1, "김장미", 47, "010-2512-1231");
		saveInfo(2, "장아름", 85, "010-2222-1231");
		saveInfo(2, "최영수", 74, "010-2222-1231");
		
		System.out.println("Default Info: " + treeMap);

	}
	
	private void step02() { // inputStudent
		Scanner sc = new Scanner(System.in);
		String name;
		int kor, eng, math;
		String contact;
		int year;
		
		// 3명의 학생 객체를 입력받음
		for(int i=0; i<3; i++) {
			try{
			
			System.out.print("이름 > ");
			name = sc.next();
			
			System.out.print("학년 > ");
			year = sc.nextInt();
			if(year < 1 || year > 6) {
				// final 변수를 사용해 조건문을 다는 것이 좋음
				throw new Exception("학년은 1~6학년까지 입력 가능합니다.");
			}
			
			System.out.print("연락처 > ");
			contact = sc.next();
			if(!Pattern.matches("^01(?:0|1|[6-9])-(?:\\d{4})-\\d{4}$", contact)) {
				throw new Exception("XXX-XXXX-XXXX 형식으로 연락처를 기입해주세요.");
			}
			
			System.out.println("국 / 영 / 수 점수 >");
			kor = sc.nextInt();
			eng = sc.nextInt();
			math = sc.nextInt();
			
			saveInfo(year, name, getAver(kor, eng, math), contact);
			} catch(Exception e) {
				System.out.println(e.getMessage());
				System.out.println("처음부터 다시 입력하세요.");
				--i; // 다시 입력하게 함
			}
		}
	}
	
	
	// menu() methods
	private void menu01() { // 1. 학번으로 검색
		int id = Integer.parseInt(JOptionPane.showInputDialog("검색할 학번을 입력하세요."));
		if(treeMap.containsKey(id)) {
			JOptionPane.showMessageDialog(null, treeMap.get(id));
			return;
		}
		JOptionPane.showMessageDialog(null, "미등록 학번입니다.");
	}
	

	private void menu02() { // 2. 연락처 뒷번호로 검색
		String tel = JOptionPane.showInputDialog("연락처 뒤 4자리를 입력하세요.");
		StringBuffer sb = new StringBuffer();
		
		for(Entry<Integer, HashMap<String, Object>> e: treeMap.entrySet()) {
			String contact = (String)e.getValue().get("contact");
			if(contact.endsWith(tel)) {
				sb.append("학번 : " + e.getKey() + "\n" + e.getValue() + "\n");
			}
		}
		
		if(sb.toString().isEmpty()) {
			// sb가 비었을 경우 : 일치하는 뒷자리가 없음
			sb.append("검색 결과가 없습니다.");
		}
		
		JOptionPane.showMessageDialog(null, sb);
	}
	

	private void menu03() { // 3. 1등 학생 보기
		// 최댓값 잡기?  : int max로 잡으면 코드가 복잡해짐.
		// 점수 말고 HashMap 객체를 통째로 받아온다.
		Entry<Integer, HashMap<String, Object>> topEntry = null;
		
		// 가장 큰 평균과 가장 큰 평균을 가진 가장 고학년인 학생객체를 찾아내는 for문
		for(Entry<Integer, HashMap<String, Object>> e : treeMap.entrySet()) {
			if(topEntry == null) {
				topEntry = e;
				continue;
			}
			
			int topAver = (int)topEntry.getValue().get("average");
			// 최고 학생의 평균점수
			int average = (int)e.getValue().get("average");
			
			if(topAver <= average) {
				topEntry = e;
				continue;
			}
		}
		
		// 최고 점수가 여러 명일 경우 가장 고학년이 topEntry가 된다. (treeMap이므로 오름차순 정렬)
		int year = (int)(topEntry.getKey())/100; // 학년
		int average = (int)topEntry.getValue().get("average"); // 평균 점수
		
		TreeMap<Integer, HashMap<String, Object>> map = new TreeMap<>();
		// 최고 점수의 최고학년이 3학년일 경우 year : 3
		// years는 각 학년의 마지막 학번값들을 담고 있다 { 104, 205, 305, 400, 501, ...}
		for(int i=(year*100)+1; i<=years[year-1]; i++) {
			HashMap<String, Object> iMap = treeMap.get(i);
			if(average != (int)iMap.get("average")) { // average에는 최고점이 들어가 있음.
				continue;
			} // 같지 않으면 continue;
			map.put(i, iMap); // 같은 점수가 있으면 ArrayList에 add
		}
		StringBuffer sb = new StringBuffer();
		for(Integer key:map.keySet()) {
			sb.append("학번 : " + key + map.get(key) + "\n");
		}
		
		JOptionPane.showMessageDialog(null, sb);
		
	}


	private void menu04() { // 4. 모든 학생 보기
		StringBuffer sb = new StringBuffer();
		for(Entry<Integer, HashMap<String, Object>> e : treeMap.entrySet()) {
			sb.append("학번 : " + e.getKey() + "" + e.getValue() + "\n");
		}
		
		if(sb.toString().isEmpty()) {
			sb.append("등록 정보가 없습니다.");
		}
		JOptionPane.showMessageDialog(null, sb);
	}


	public Quiz01() {
		String select;
		
		// 기본 학생 정보 정하기
		step01();

		// 학생 정보 입력하기
		step02();


		// 메뉴 출력하기
		menu : while(true) {
			select = JOptionPane.showInputDialog("1. 학번으로 검색\n2. 연락처 뒷번호로 검색\n3. "
					+ "1등 학생 보기\n4. 모든 학생 보기\n0. 종료");

			switch(select) {

			case "0":{
				JOptionPane.showMessageDialog(null, "프로그램을 종료합니다.");
				break menu;
				// System.exit(0)을 써도 ok
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
			
			default:
				JOptionPane.showMessageDialog(null, "잘못된 입력입니다. 다시 입력하세요.");
			}

		}

	}


	public static void main(String[] args) {
		new Quiz01();
	}
}
```
