# Explain
User 객체는 id, pw값을 private로 가진다. 이 때 id값은 20글자 이하, pw값은 10글자 이하이며 checkInfo를 통해 정보를 확인할 경우 pw값은 *으로 표시된다. 
login을 통해 id, pw값을 설정하고 환영 메세지를 띄운다. 

# SourceCode
```java
package day13.basic;
import javax.swing.JOptionPane;

class User{
	private String id;
	private String pw;

	// 조건 : id는 20글자 이하, pw는 10글자 이하이며, 확인 시 *으로 나타낸다.
	public void setId(String id) {
		if(id.length() > 20) {
			this.id = null;
			return;
		}
		this.id = id;
	}
	
	public void setPw(String pw) {
		if(pw.length() > 10) {
		this.pw = null;
		return;
		}
		this.pw = pw;
	}
	
	public String getId() {
		return this.id;
	}
	
	public String getPw() {
		String starPw="";
		if(this.pw == null) {
			return null;
		}
		for(int i=0; i<this.pw.length(); i++) {
			starPw += "*";
		}
		return starPw;
	}
	
	public void login() {
		String id = JOptionPane.showInputDialog("id");
		String pw = JOptionPane.showInputDialog("pw");
		
		this.setId(id);
		this.setPw(pw); 
		// 사용자에게 id, pw값을 입력받고 해당 값을 현재 user객체 필드에 설정한다. 만약 조건을 어긋난 값을 입력한 경우 설정되지 않는다.
		
		if(this.getId()==null || this.getPw()==null) {
			JOptionPane.showMessageDialog(null, "유저 정보가 없습니다.");
			return; // user객체에 아이디/패스워드 값이 설정되있지 않으면(잘못된 값을 설정하였을 경우) 로그인 실패
		}
		JOptionPane.showConfirmDialog(null, "환영합니다, " + this.getId() + "!");
	}
	
	public void checkInfo() {
		if(this.getId()==null || this.getPw()==null) {
			JOptionPane.showMessageDialog(null, "유저 정보를 불러오는데 실패했습니다.");
			return;
		}
		JOptionPane.showMessageDialog(null, "* user 정보 *\nid:" + this.getId() + "\npw:" + this.getPw());
	}
}

public class heejinTest {
	public static void main(String[] args) {
		
		User u1 = new User();
		u1.login();
		u1.checkInfo();
	}

}
```
