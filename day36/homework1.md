## hw01 : 포켓몬 관리 프로그램 만들기

### SourceCode
```java
package day36.basic;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

import javax.swing.JFrame;
import javax.swing.JOptionPane;

public class test01 extends JFrame{
	private static final String URL = 
			"jdbc:mysql://127.0.0.1/testdb?useUnicode=true&characterEncoding=utf8";
	private static final String ID = "testdba";
	private static final String PASSWORD = "test1234";

	private String sql = "SELECT * FROM pokemon";

	private static Connection connection;
	private PreparedStatement preparedStatement;
	private ResultSet resultSet;

	static {
		try {
			Class.forName("com.mysql.jdbc.Driver");
			connection = DriverManager.getConnection(URL, ID, PASSWORD);
		}catch(ClassNotFoundException | SQLException e) {
			e.printStackTrace();
		}
	}
	
	private void close() {
		// preparedStatement, connection을 닫아 주는 것을 한 번에 수행(함수화)
		try {
			if(preparedStatement != null)
				preparedStatement.close();
			if(connection != null)
				connection.close();
		}catch(SQLException e) {
			e.printStackTrace();
		}
	}

	// methods
	private void savePokemon(String name, int level, int ap, int hp) throws SQLException {
		String insertsql = "INSERT INTO pokemon(name, level, ap, hp) " + "VALUES(?, ?, ?, ?)";
		preparedStatement = connection.prepareStatement(insertsql);

		preparedStatement.setString(1, name);
		preparedStatement.setInt(2, level);
		preparedStatement.setInt(3, ap);
		preparedStatement.setInt(4, hp);
		// INJECTION 판단 쿼리(주석이 포함되어 있는지 등)
		
		preparedStatement.execute();
	}

	private void menu01() {
		// 포켓몬 추가
		String name="";
		int level=0;
		
		while(true) {
			name = JOptionPane.showInputDialog("이름을 입력하세요.");
			if(name.isEmpty()) {
				JOptionPane.showMessageDialog(null, "공백은 이름으로 지정 불가합니다.");
				continue;
			}

			level = Integer.parseInt(JOptionPane.showInputDialog("레벨을 입력하세요."));
			if(level < 0) {
				JOptionPane.showMessageDialog(null, "음수값은 레벨이 될 수 없습니다.");
				continue;
			}
			
			break;
		}

		int ap = (int)Math.round(level*.5); 
		int hp = level * 100;

		try {
			savePokemon(name, level, ap, hp);
			JOptionPane.showMessageDialog(null, "포켓몬 추가 완료!");
		}catch(SQLException e) {
			e.printStackTrace();
		}
	}

	private void menu02() {
		// 번호로 검색
		int number = Integer.parseInt(JOptionPane.showInputDialog("포켓몬 번호를 입력하세요"));
		StringBuffer sb = new StringBuffer();
		try {
			preparedStatement = connection.prepareStatement(sql);
			resultSet = preparedStatement.executeQuery();
			sb = new StringBuffer();

			while(resultSet.next()) {
				if(resultSet.getInt(1) == (number)) {
					sb.append("*포켓몬이 존재합니다*\nno.")
					.append(resultSet.getInt(1)).append(" ")
					.append(resultSet.getString(2)).append(" lv.")
					.append(resultSet.getInt(3)).append( "[")
					.append(resultSet.getString(6)).append("]" );

					JOptionPane.showMessageDialog(null, sb);
					return;
				}
			}

			JOptionPane.showMessageDialog(null, "포켓몬이 존재하지 않습니다.");

		}catch(SQLException e) {
			e.printStackTrace();
		}
	}

	private void menu03() {
		// 이름으로 검색
		String name = JOptionPane.showInputDialog("포켓몬 이름을 입력하세요.");
		StringBuffer sb = new StringBuffer();
		try {
			preparedStatement = connection.prepareStatement(sql);
			resultSet = preparedStatement.executeQuery();

			while(resultSet.next()) {
				if(resultSet.getString(2).equals(name)) {
					sb.append("*포켓몬이 존재합니다*\nno.")
					.append(resultSet.getInt(1)).append(" ")
					.append(resultSet.getString(2)).append(" lv.")
					.append(resultSet.getInt(3)).append( "[")
					.append(resultSet.getString(6)).append("]" );

					JOptionPane.showMessageDialog(null, sb);
					return;
				}
			}

			JOptionPane.showMessageDialog(null, "포켓몬이 존재하지 않습니다.");

		}catch(SQLException e) {
			e.printStackTrace();
		}
	}

	private void menu04() {
		// 포켓몬 삭제
		String name = JOptionPane.showInputDialog("삭제할 포켓몬의 이름을 입력하세요.");
		String deletesql = "DELETE FROM pokemon WHERE name='" + name + "'";

		try {
			preparedStatement = connection.prepareStatement(sql);
			resultSet = preparedStatement.executeQuery();

			while(resultSet.next()) {
				if(resultSet.getString(2).equals(name)) {
					preparedStatement = connection.prepareStatement(deletesql);
					preparedStatement.execute();
					JOptionPane.showMessageDialog(null, "삭제 완료!");
					return;
				}
			}

			JOptionPane.showMessageDialog(null, "포켓몬이 존재하지 않습니다.");

		}catch(SQLException e) {
			e.printStackTrace();
		}
	}

	private void menu05() {
		// 레벨업
		String name = JOptionPane.showInputDialog("레벨업할 포켓몬의 이름을 입력하세요.");
		String levelupsql = "UPDATE pokemon SET level = level+1 WHERE name='" + name + "'";

		try {
			preparedStatement = connection.prepareStatement(sql);
			resultSet = preparedStatement.executeQuery();

			while(resultSet.next()) {
				if(resultSet.getString(2).equals(name)) {
					preparedStatement = connection.prepareStatement(levelupsql);
					preparedStatement.execute();
					JOptionPane.showMessageDialog(null, "레벨업 완료!");
					return;
				}
			}

			JOptionPane.showMessageDialog(null, "포켓몬이 존재하지 않습니다.");

		}catch(SQLException e) {
			e.printStackTrace();
		}
	}

	private void menu06() {
		// 모두 레벨업
		String alllevelupsql = "UPDATE pokemon SET level = level+1";

		try {
			preparedStatement = connection.prepareStatement(alllevelupsql);
			preparedStatement.execute();
			JOptionPane.showMessageDialog(null, "모두 레벨업 완료!");
		}catch(SQLException e) {
			e.printStackTrace();
		}
	}

	public test01() {
		String menu = "1. 포켓몬 추가\n"
				+ "2. 번호로 검색\n"
				+ "3. 이름으로 검색\n"
				+ "4. 포켓몬 삭제\n"
				+ "5. 레벨업\n"
				+ "6. 모두 레벨업\n"
				+ "0. 종료\n";

		menu: while(true) {
			String select = JOptionPane.showInputDialog(menu);
			switch(select) {
			case "0":
				JOptionPane.showMessageDialog(null, "프로그램을 종료합니다.");
				break menu;

			case "1":
				menu01();
				break;

			case "2":
				menu02();
				break;

			case "3":
				menu03();
				break;

			case "4":
				menu04();
				break;

			case "5":
				menu05();
				break;

			case "6":
				menu06();
				break;

			default:
				JOptionPane.showMessageDialog(null, "다시 입력하세요.");
				break;
			}
		}
		
		close();
	}
	
	public static void main(String[] args) {
		new test01();
	}

}
```
