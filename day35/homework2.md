## hw 2 : 입력받은 포켓몬을 pokemon 테이블에서 조회하여 각 column값을 출력하기
없을 경우 '미등록 포켓몬'

### now(2020.12.11 16:39)
* 입력받은 포켓몬이 있다면 출력하는 것까지는 완성
* 존재하지 않는 포켓몬의 이름을 입력할 경우 catch문으로 넘어가지 않는다. 
'미등록 포켓몬' 이 출력되게 하려면 어떻게 해야 할까?

### now(2020.12.14 13:00)
* 해결 완료
* catch문으로 가지 않고 try문 내부에서 처리되도록 짜야 한다.

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
		StringBuffer sb;
		
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
				sb = new StringBuffer();
				resultSet = preparedStatement.executeQuery();
				
				if(resultSet.next()) {
				// pokemon의 name 필드는 unique 제약조건이 설정되어있으므로, 굳이 while문을 사용할 필요는 없음
					sb.append("no. ");
					sb.append(resultSet.getInt(1));
					sb.append(" ");
					sb.append(input);
					sb.append("(lv.");
					sb.append(resultSet.getInt(3));
					sb.append(") hp");
					sb.append(resultSet.getInt(4));
					sb.append("/ap ");
					sb.append(resultSet.getInt(5));
					sb.append(" 생성일자 ");
					sb.append(resultSet.getString(6));
					// +연산자를 사용하여 처리할 경우 +가 사용될 때마다 새로운 객체가 생성되었다가 gc에 의해 폐기된다. 
					// vm능력 향상을 위해 위처럼 append를 이용해 concat하는 것이 좋음.
				} else {
					JOptionPane.showMessageDialog(null, "미등록 포켓몬");
					continue;
				}
				
				JOptionPane.showMessageDialog(null, "*조회 성공*\n" + sb);
			}catch(SQLException e) {
				e.printStactTrace();
				// 해결해야 할 문제 : 미등록 포켓몬을 입력할 경우 어떻게 해당 문장이 나타나게 해야 할까?
				// -> 해결 완료
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
