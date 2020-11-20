# Question
회원가입과정은 다음과 같습니다.
	1) 이메일을 입력 받는다.
	2) 비밀번호를 2번 입력받는다.
	
    이때 다음 조건에 충족하면 저장, 그렇지 않으면 해당 항목을 재입력 받으세요
 	1) 이메일 조건
		- @ 를 포함하여야 한다.
		- com, co.kr, net 중 하나로 끝나야 한다
		- 메일서버(naver, gmail, hanmail 등) 이름을 포함해야 한다.
		- 아이디가 있어야 한다.
		- 공백이 있다면 제거한다.
		
	2) 비밀번호 조건
		- 4자 이상 20자 이하여야 한다.
		- (선택사항) 특수기호, 숫자, 대소문자가 최소 1개씩 모두 있어야 한다. (String 클래스의 matches()사용)
		- 두 비밀번호가 동일해야 한다.

   모두 정상적인 입력을 받았다면 사용자의 id, 패스워드, 이메일을 출력하세요.
	1) id 는 이메일의 @ 앞 부분을 추출합니다.
	2) 비밀번호는 앞 두 글자만 출력하고 나머지는 '*'로 대체합니다.
		예) pika1234 ==> pi******
	3) 이메일은 모두 출력합니다.

# Review
나는 while문 ) 아이디입력 내부while) 패스워드입력 및 체크 이렇게 짰는데 이러면 depth가 깊어지니까 좋지 않고, 아이디를 확인하는 while문과 패스워드를 확인하는 while문(이 while문 내부에 중복 확인하는 while문)을 따로 두는 게 좋다.
그리고 반복할 필요가 없는 단순 동작은 while문 밖에 빼는 것이 좋다.

```java
package day19.homework;

import javax.swing.JOptionPane;

public class Quia02 {
	public static void main(String[] args) {
		String email="";
		String password="";
		String id= null;
		String protectedPass = "";
		boolean flag = true;

		while(true) {
			// 이메일 입력받기
			email = JOptionPane.showInputDialog("이메일을 입력하세요");
			
			if(!email.contains("@")) {
				JOptionPane.showMessageDialog(null, "@을 반드시 포함하여야 합니다.");
				continue;	
			}
			
			if(!email.endsWith("com") || email.endsWith("co.kr") || email.endsWith("hanmail")) {
				JOptionPane.showMessageDialog(null, "잘못된 이메일 형식입니다(com, co.kr, hanmail로 끝나야 합니다.");
				continue;
			}

			if(email.indexOf("@") != 0) {
				email.trim(); // 공백 제거
			} else {
				JOptionPane.showMessageDialog(null, "아이디가 없습니다.");
				continue;
			}
			break;
		}
		
		id = email.split("@")[0];

		
		// 패스워드를 입력받는 while문
		while(flag) {
			password = JOptionPane.showInputDialog("비밀번호를 입력하세요");
			
			if(password.length() <4 || password.length()>20) {
				JOptionPane.showMessageDialog(null, "비밀번호는 4자 이상 20자 이하여야 합니다.");
				continue;
			}
			
			while(true) {
				String passwordCheck = JOptionPane.showInputDialog("다시 한 번 입력하세요");
				
				if(password.equals(passwordCheck)) {
					JOptionPane.showMessageDialog(null, "비밀번호 확인에 성공했습니다.");
					flag = false;
					break;
				}
				
				JOptionPane.showMessageDialog(null, "비밀번호가 동일하지 않습니다!");
				continue;
			}
		}

		String[] pass = password.split("");
		
		for(int i=0; i<pass.length; i++) {
			if(i>1) {
				protectedPass += "*";
				continue;
			}
			protectedPass += pass[i];
		}
		
		// while문 종료
		JOptionPane.showMessageDialog(null, "회원 가입 완료!");
		JOptionPane.showMessageDialog(null, "* 회원 정보 출력 *\n아이디 : " + id + "\n패스워드 : " + protectedPass + "\n이메일 : " + email);
	}


}
```
