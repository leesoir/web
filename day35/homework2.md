## hw 2 : 입력받은 포켓몬을 pokemon 테이블에서 조회하여 각 column값을 출력하기
없을 경우 '미등록 포켓몬'

### now(2020.12.11 16:39)
* 입력받은 포켓몬이 있다면 출력하는 것까지는 완성
* 존재하지 않는 포켓몬의 이름을 입력할 경우 catch문으로 넘어가지 않는다. 
'미등록 포켓몬' 이 출력되게 하려면 어떻게 해야 할까?

```java
package day35.homework;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

import javax.swing.JOptionPane;

public class Quiz02 {
//	사용자에게 조회할 포켓몬의 이름을 입력 받고 해당 포켓몬의 정보를 DB에 조회한 뒤 출력
//    없으면 '미등록 포켓몬'
	private static final String URL = 
			"jdbc:mysql://127.0.0.1/testdb?useUnicode=true&characterEncoding=utf8";
	private static final String ID = "testdba";
	private static final String PASSWORD = "test1234";
	
	private Connection connection;
	private PreparedStatement preparedStatement;
	private ResultSet resultSet;
	
	public Quiz02(){
		StringBuffer sb = new StringBuffer();
		
		try {
			connection = DriverManager.getConnection(URL, ID, PASSWORD);
		}catch(SQLException e) {
			e.printStackTrace();
		}
		
		while(true) {
			String input = JOptionPane.showInputDialog("조회할 포켓몬의 이름을 입력하세요(exit를 누르면 종료합니다).");
			if(input.equals("exit")) {
				break;
			}
			
			try {
				preparedStatement = connection.prepareStatement("SELECT * FROM pokemon WHERE name='" + input + "'");
				
				resultSet = preparedStatement.executeQuery();
				while(resultSet.next()) {
					sb.append("no." + resultSet.getInt(1) + " " + input + "(lv." + resultSet.getInt(3) + 
				") hp " + resultSet.getInt(4) + "/ap " + resultSet.getInt(5) + " 생성일자 " + resultSet.getString(6));
				}
				
				JOptionPane.showMessageDialog(null, "*조회 성공*\n" + sb);
			}catch(SQLException e) {
				JOptionPane.showMessageDialog(null, "미등록 포켓몬");
				// 해결해야 할 문제 : 미등록 포켓몬을 입력할 경우 어떻게 해당 문장이 나타나게 해야 할까?
			}
		}
	}
	
	public static void main(String[] args) {
		try {
			new Quiz02();
		}catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```
