# DB와 Java Application 연결하기

## hw 1 : 입력받은 값을 바탕으로 포켓몬을 생성하여 testdb의 pokemon table에 추가하기
Scanner(Jop) 를 사용하여 새 포켓몬의 이름, 레벨을 입력 받는다.
* 공격력은 레벨의 0.5 배
* 체력은 레벨의 100 배로 세팅하여 이를 DB에 저장 (INSERT)

```java
package day35.homework;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

import javax.swing.JOptionPane;

class Pokemon{
	String name;
	int level;
	int hp;
	int ap;
	
	public Pokemon(String name, int level){
		this.name = name;
		this.level = level;
		this.hp = this.level * 100;
		this.ap = (int)(this.level*0.5);
	}
}

public class Quiz01 {
	private static final String URL = 
			"jdbc:mysql://127.0.0.1/testdb?useUnicode=true&characterEncoding=utf8";
	private static final String ID = "testdba";
	private static final String PASSWORD = "test1234";
	
	private Connection connection;
	private PreparedStatement preparedStatement;
	private ResultSet resultSet;
	
	StringBuffer sb = new StringBuffer();
	
	public Quiz01() throws SQLException{
		
		connection = DriverManager.getConnection(URL, ID, PASSWORD);
		loop : while(true) {
			Pokemon p;
			String name;
			int level;
			
			int input = JOptionPane.showConfirmDialog(null, "포켓몬을 생성하겠습니까?");
			if(input == JOptionPane.CANCEL_OPTION || input == JOptionPane.CLOSED_OPTION || input == JOptionPane.NO_OPTION) {
				JOptionPane.showMessageDialog(null, "포켓몬 생성 프로그램을 종료합니다.");
				break loop;
			}
			
			name = JOptionPane.showInputDialog("이름을 입력하세요");
			level = Integer.parseInt(JOptionPane.showInputDialog("레벨을 입력하세요"));
			
			p = new Pokemon(name, level);
			// 나머지 column값은 constructor에 의해 자동 설정
			
			preparedStatement = connection.prepareStatement
					("INSERT INTO pokemon VALUES(null, '" + p.name + "', " + p.level + ", " + p.hp + ", " + p.ap + ", DEFAULT)");
			
			preparedStatement.execute();
			JOptionPane.showMessageDialog(null, "포켓몬 생성 완료!");
			
			preparedStatement = connection.prepareStatement("SELECT * FROM pokemon");
			resultSet = preparedStatement.executeQuery();
			while(resultSet.next()) {
				sb.append("no. " + resultSet.getInt(1) + " 이름 : " + resultSet.getString(2) + " 레벨 : " + resultSet.getInt(3)
				+ " hp : " + resultSet.getInt(4) + " ap : " + resultSet.getInt(5) + " regdate : " + resultSet.getString(6) + "\n");
			}
			
			JOptionPane.showMessageDialog(null, "*현재 pokemon table*\n" + sb);
		}
	}
	
	public static void main(String[] args) {
		try {
			new Quiz01();
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}

}
```
