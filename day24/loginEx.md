# Explain
 email, password 문제 리팩토링 
 
==> 조건에 맞는 않는 입력이면 throw 로 예외객체를 생성하여 던질 것 

==> 예외클래스 MySignupPolicy를 정의하여 사용할 것 

==> setEmail(), setPassword(), confirmPassword() 에 throws 선언을 할 것!

==> main()에서 try-catch를 할 것

# SourceCode
```java
package day24.homework;

import java.util.Arrays;
import java.util.Scanner;


@SuppressWarnings("serial")
/*
 email, password 문제 리팩토링 
==> 조건에 맞는 않는 입력이면 throw 로 예외객체를 생성하여 던질 것 
==> 예외클래스 MySignupPolicy를 정의하여 사용할 것 
==> setEmail(), setPassword(), confirmPassword() 에 throws 선언을 할 것!
==> main()에서 try-catch를 할 것
 */

class MySignupPolicyException extends Throwable{
	// user defined exception
	public MySignupPolicyException() {
		super("이메일 규정을 위반하였습니다.");
	}

	public MySignupPolicyException(String message) {
		super(message);
	}
}

class User {

	interface Whitelist{
		String[] VALID_MAIL_SERVER_NAMES = 
			{ "naver", "gmail", "hanmail", "nate"};

		String[] VALID_MAIL_SUFFIXES = 
			{"com", "co.kr", "net", "org" };
		String PASSWORD_REGEX = "^(?=.*[0-9])(?=.*[a-z])(?=.*[A-Z])(?=.*[@#$%^&+=])(?=\\S+$).{4,20}$";

	}


	private String id; // get
	private String email; // set, get
	private String password; // set, (get 대신 hiddenPassword) 


	public boolean setEmail(String email) throws Throwable{

		if(null == email) {
			throw new MySignupPolicyException("이메일이 누락되었습니다.");
		}


		// email 양 공백 제거
		email = email.trim();


		// @ 를 포함하여야 한다.
		if(!email.contains("@")) {
			throw new MySignupPolicyException("@를 포함해야 합니다.");
		}

		// trim이 되었고 @가 있는 이메일은  
		//  아이디가 없을 경우 무조건 맨 앞글자가 "@"일 것이다.
		if(email.indexOf("@") == 0) {
			throw new MySignupPolicyException("이메일은 아이디를 포함해야 합니다.");
		}

		// com, co.kr, net 중 하나로 끝나야 한다
		String suffix = null;
		for(String s : Whitelist.VALID_MAIL_SUFFIXES) {
			if(email.endsWith(s)) {
				suffix = s;
				break;
			}
		}
		if(null == suffix) {
			throw new MySignupPolicyException(Arrays.toString(Whitelist.VALID_MAIL_SUFFIXES) + "중 하나로 끝나야 합니다.");

		}

		// 메일서버(naver, gmail, hanmail 등) 이름을 포함해야 한다.
		boolean check = false;
		for(String server : Whitelist.VALID_MAIL_SERVER_NAMES) {
			if(email.endsWith("@" + server + "." + suffix)) {
				check = true;
				break;
			}
		}
		if(!check) {
			throw new MySignupPolicyException("이메일은 메일 서버 이름을 포함해야 합니다.(" + Whitelist.VALID_MAIL_SERVER_NAMES + ")");
		}
		this.email = email;
		setId();
		return true;
	}


	public boolean setPassword(String password) throws MySignupPolicyException{
		if (!password.matches(Whitelist.PASSWORD_REGEX)) {
			throw new MySignupPolicyException("특수기호, 숫자, 대소문자를 최소 1개씩 포함해야 합니다.");
		}
		//		if(password.length() < 4 || password.length() > 20) {
		//			throw new MySignupPolicyException("비밀번호 길이는 4자 이상 20자 이하여야 합니다.");
		//		} // REGEX때문에 필요 없음
		this.password = password;
		return true;
	}


	public boolean confirmPassword(String password) throws MySignupPolicyException{
		if(null == this.password) {
			throw new MySignupPolicyException("second password가 누락되었습니다.");
		}
		return this.password.equals(password);
	}


	private void setId(){
		if(null == email) 
			return;
		id = email.substring(0, email.indexOf("@"));
	}

	public String hiddenPassword() { // 예외 발생 x
		if(null == password) {  // pika1234 
			return null;
		}
		String temp = password.substring(0,2); // pi
		for(int i = 0; i < password.length()-2; ++i) { // "*" 를 총 6번 붙임
			temp += "*";
		}
		return temp; // pi******
	}

	@Override
	public String toString() {
		return "User [id=" + id + 
				", email=" + email + 
				", password=" + hiddenPassword() + "]";
	}
}


public class Quiz01 {
	public static void main(String[] args) throws Throwable {
		User user = new User();
		Scanner sc = new Scanner(System.in);

		// try-catch가 while문을 감쌀 때 : exception이 발생하면 밑의 코드가 실행 x
		// while문이 try-catch를 감쌀 때 : exception이 발생해도 다시 처음부터 실행되게 됨

		// heejin : 2로 수행

		// email
		while(true) {
			try {
				System.out.print("이메일 > ");
				String email = sc.next();
				user.setEmail(email); // email 약관을 벗어난 경우 catch문 실행 후 while문으로 돌아옴
				break;
			}
			catch (MySignupPolicyException e) {
				System.out.println(e.getMessage()); // setEmail이 조건마다 가지는 Exception 객체의 메세지를 가져온다.
			}
		}
		
		// password
		while(true) {
			try {
				System.out.print("비밀번호 > ");
				String password = sc.next();
				user.setPassword(password); // exception point
				
				System.out.print("한 번 더 입력하세요 > ");
				String twice = sc.next();
				if(!user.confirmPassword(twice)) {
					System.out.println("비밀번호가 일치하지 않습니다.");
					continue;
				}
				break; // 정상적으로 비밀번호를 같게 입력한 경우 while문 종료. 
			}catch(MySignupPolicyException e) {
				System.out.println(e.getMessage()); // 비밀번호가 약관에 맞지 않는 경우 exception 후 다시 while문으로 돌아감
			}
		}
		
		sc.close();
	}
}
```
