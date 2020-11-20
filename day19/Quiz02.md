```java
package day19.homework;

import javax.swing.JOptionPane;

public class Quia02 {
	/*
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
	 */
	public static void main(String[] args) {
		String email="";
		String password="";
		String id="";
		String protectedPass = "";
		boolean flag = true;
		
		while(flag) {
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
			
			String[] emailArr = email.split("@");
			id += emailArr[0];
			
			// 패스워드를 입력받는 while문
			while(true) {
				password = JOptionPane.showInputDialog("비밀번호를 입력하세요");
				if(password.length() <4 || password.length()>20) {
					JOptionPane.showMessageDialog(null, "비밀번호는 4자 이상 20자 이하여야 합니다.");
					continue;
				}
				
				String passwordCheck = JOptionPane.showInputDialog("다시 한 번 입력하세요");
				if(password.equals(passwordCheck)) {
					flag = false;
					break;
				}
				JOptionPane.showMessageDialog(null, "비밀번호가 동일하지 않습니다!");
				continue;
			}
			
			String[] pass = password.split("");
			for(int i=0; i<pass.length; i++) {
				if(i>1) {
					protectedPass += "*";
					continue;
				}
				protectedPass += pass[i];
			}
		}
		// while문 종료
		JOptionPane.showMessageDialog(null, "회원 가입 완료!");
		JOptionPane.showMessageDialog(null, "* 회원 정보 출력 *\n아이디 : " + id + "\n패스워드 : " + protectedPass + "\n이메일 : " + email);
	}

}
```
