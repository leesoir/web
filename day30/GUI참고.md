```java
package day30.basic;

import java.awt.BorderLayout;
import java.awt.Dimension;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.JTextArea;
import javax.swing.JTextField;

public class Test01 extends JFrame{
	private JTextArea ta;
	private JTextField tf;
	private JButton btn;
	
	public Test01() {
		super("메모장");
		setLayout(new BorderLayout());
		setSize(new Dimension(500, 700));
		setDefaultCloseOperation(EXIT_ON_CLOSE);
		setLocation(1200, 120);
		
		// frame center에는 JTextArea, south에는 JPanel - JTextField
		// 
		
		ta = new JTextArea();
		ta.setEditable(false); // 사용자가 편집 불가능하도록 함
		
		tf = new JTextField();
		
		
		// JTextField의 이벤트 추가
		// tf에 문자열을 입력하고 엔터를 치면 해당 내용은 ta에 붙여주도록 한다.
		
		// mechanism
		// 1. KeyListener 객체 생성
		// 2. KeyListener 객체를 tf에 붙여준다.
		tf.addKeyListener(new KeyListener() {
			// anonymous class로 EventListener add
			
			@Override
			public void keyTyped(KeyEvent e) {
				// keyTyped : 
				
			}
			
			@Override
			public void keyReleased(KeyEvent e) {
				// keyReleased : 
				
			}
			
			@Override
			public void keyPressed(KeyEvent e) {
				// keyPressed
				if(e.getKeyCode() == KeyEvent.VK_ENTER) { // e.getKeyCode() == '\n'
					
					// 1. TextField에 입력한 text 값 얻어오기
					String input = tf.getText() + "\n";

					// 2. 얻어온 text를 TextArea에 append
					String memo = ta.getText();
					ta.setText(memo + input);
					
					// 3. tf의 내용 지우기
					tf.setText(null);
					System.out.println("입력 완료!");
				}
			}
		});
	
		
		
		// JButton의 이벤트 추가
		btn = new JButton("삭제");
		btn.addActionListener(new ActionListener() {
			
			@Override
			public void actionPerformed(ActionEvent e) {
				// JTextArea, TextField에 적힌 모든 텍스트를 삭제
				ta.setText(null);
				tf.setText(null);
				System.out.println("삭제 완료!");
			}
		});
		
		
		JPanel southP = new JPanel();
		southP.setLayout(new BorderLayout());
		southP.add(tf, BorderLayout.CENTER);
		southP.add(btn, BorderLayout.EAST);
		
		this.add(ta, BorderLayout.CENTER);
		this.add(southP, BorderLayout.SOUTH);
		setVisible(true);
		tf.requestFocus(); // tf에 focus 요청
		// * requestDefaultFocus : deprecated
	}
	
	public static void main(String[] args) {
		new Test01();
	}
}
```
