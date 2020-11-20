# Explain
메인 클래스와 User 클래스를 구분하여 작성하였다.

# User Class
```java
package loginHomework;

public class User {
	//fields
	private String id; // set, get
	private String email; // set, get
	private String password; // set, get 대신 hiddenPassword

	// teacher : 유효한 서버 이름, 도메인을 상수 선언할 경우 유지보수가 편리하다.
	// interfece 위치는 외부가 좋을까, 내부(class User 안에서만 사용할 인터페이스가 된다)가 좋을까?
	interface Whitelist{ // 내장 인터페이스 Whitelist
		String[] VALID_MAIL_SERVER_NAMES = {
				"naver", "daum", "hanmail", "nate"
		};
		String[] VALID_MAIL_SUFFIXES = {
				"com", "co.kr", "net", "org"
		};
	}


	// getters and setters
	public String getId() {
		return this.id;
	}
	
	private void setId() {
		if(null == email)
			return;

		// 이메일에서 아이디만 추출하기
		// 방법 1 : split("@")
		this.id = email.split("@")[0];

		// 방법 2 : email.subString(0, indexOf("@"));


	}

	public String getEmail() {
		return this.email;
	}

	public boolean setEmail(String email) {
		// 이메일 조건 확인
		if(null == email) 
			return false;
		
		// 이메일 공백 제거
		email = email.trim();
		
		// @를 포함하여야 한다.
		if(!email.contains("@")) {
			System.out.println("@을 포함해야 합니다.");
			return false;
		}
		
		// 공백 제거 후 @가 있는 것이 확인된 이메일은 아이디가 없을 경우 앞글자가 @
		if(email.indexOf("@") == 0) {
			System.out.println("아이디가 없습니다.");
			return false;
		}

		// SUFFIXES로 끝나야 한다.
		String suffix = null;
		for(String s : Whitelist.VALID_MAIL_SUFFIXES) {
			if(email.endsWith(s)) {
				suffix = s;
				break;
			}
		}

		if(null == suffix) { // 체크 후에도 suffix가 null이면 올바른 이메일 형식으로 끝나지 않았다는 뜻이다.
			System.out.println("이메일 형식이 옳지 않습니다(com, co.kr, hanmail로 끝나야 합니다).");
			return false;
		}

		
		// 메일 서버의 이름을 포함해야 한다.
		boolean check = false;
		for(String server : Whitelist.VALID_MAIL_SERVER_NAMES) {
			if(email.endsWith("@" + server + "." + suffix)) {
				check = true;
				break;
			}
		}

		if(!check)
			return false;
		
		// 해당 자리까지 오면 입력값은 email 조건을 모두 충족하였다.
		this.email = email;
		this.setId();
		return true;
	}

	
	public String getPassword() {
		//null값 처리
		if(null == password) {
			return null;
		}
		
		// 패스워드가 앞 2글자만 두고 *로 표시되도록 한다.
		String hiddenPass = password.substring(0,2);
		for(int i=0; i<password.length()-2; i++) {
			hiddenPass += "*";
		}
		return hiddenPass;
	}

	
	public boolean setPassword(String password) {
		if(password.length() < 4 || password.length() > 20) {
			System.out.println("패스워드 길이는 4자 이상, 20자 이하여야 합니다.");
			return false;
		}
		this.password = password;
		return true;
	}


	// method
	public boolean confirmPassword(String password) {
		
		// 등록된 패스워드의 존재 확인
		if(null == this.password)
			return false; 
		
		return this.password.equals(password);
	}
	
	@Override
	public String toString() {
		return "User id : " + this.getId() 
+ " password : " + this.getPassword() + " email : " + this.getEmail();
	}
}
```


# Main Class
```java
package loginHomework;
import java.util.Scanner;


public class Test {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		User user = new User();

		// 이메일 입력 루프
		while(true) {
			System.out.print("이메일 > ");
			String email = sc.next();
			if(!user.setEmail(email)) 
				continue;
			
			break;
		}

		// 패스워드 입력 루프
		while(true) {
			System.out.print("비밀번호 > ");
			String password = sc.next();
			if(!user.setPassword(password)) 
				continue;
			

			while(true) {
				System.out.print("한 번 더 입력하세요 > ");
				String check = sc.next();
				if(!user.confirmPassword(check)) {
					System.out.println("비밀번호가 일치하지 않습니다.");
					continue;
				}
				break;
			}
			break;
		}
		
		System.out.println(user);

		sc.close();
	}

}
```
