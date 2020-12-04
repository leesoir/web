# Explain
![Day30_1 숙제](https://user-images.githubusercontent.com/69781566/101131284-61b92180-3648-11eb-873f-5f328fea75c3.png)
## plus
GUI 컴포넌트 스타일링 참고  :https://www.crocus.co.kr/548

## SourceCode
```java
package day30.homework;

import java.awt.Color;
import java.awt.GridLayout;
import java.awt.Point;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JOptionPane;

public class Quiz01 extends JFrame{
	
	private static final int WALL = 0;
	private static final int ROAD = 1;
	private static final int START = 2;
	private static final int END = 3;
	private static final int NOW = 4;
	private JButton[] btns = new JButton[64];
	
	
	private static final int[][] maze = {
			{START, ROAD, WALL, WALL, WALL, ROAD, WALL, ROAD},
			{ROAD, ROAD, ROAD, ROAD, WALL, ROAD, WALL, ROAD},
			{WALL, WALL, WALL, ROAD, ROAD, ROAD, ROAD, ROAD},
			{WALL, ROAD, ROAD, ROAD, WALL, ROAD, WALL, ROAD},
			{WALL, WALL, WALL, ROAD, WALL, WALL, WALL, ROAD},
			{ROAD, ROAD, ROAD, ROAD, ROAD, ROAD, WALL, END},
			{ROAD, WALL, WALL, WALL, WALL, WALL, WALL, ROAD},
			{ROAD, ROAD, ROAD, ROAD, ROAD, ROAD, ROAD, ROAD},
	};
	
	
	public Quiz01() {
		super("maze");
		setSize(500, 500);
		setLayout(new GridLayout(8,8));
		setDefaultCloseOperation(EXIT_ON_CLOSE);
		int count = 0;
		
		for(int[] i : maze) {
			for(int j:i) {
				btns[count] = new JButton();
				btns[count].setEnabled(false);
				
				switch(j) {
				case START:{
					btns[count].setBackground(Color.red);
					break;
				}
				case ROAD:{
					btns[count].setBackground(Color.white);
					break;
				}
				case WALL:{
					btns[count].setBackground(Color.black);
					break;
				}
				case END:{
					btns[count].setBackground(Color.blue);
					break;
				}
				}
				count++;
			}
		}
		
		for(JButton j:btns) {
			add(j);
		}
		
		Point player = new Point(0,0);
		
		// KeyEvent 작성
		KeyListener listener = new KeyListener() {
			
			@Override
			public void keyTyped(KeyEvent e) {
			}
			
			@Override
			public void keyReleased(KeyEvent e) {
			}
			
			@Override
			public void keyPressed(KeyEvent e) {
				switch(e.getKeyCode()) {
				case KeyEvent.VK_UP:{
					if(player.x == 0) {
						JOptionPane.showMessageDialog(null, "미로의 꼭대기 층입니다.");
						break;
					}
					if(maze[player.x][player.x] == WALL) {
						JOptionPane.showMessageDialog(null, "벽이라서 이동할 수 없습니다.");
						break;
					}
					player.x -= 1;
					JOptionPane.showMessageDialog(null, "이동 완료!");
					btns[(int)player.getX()*8 + (int)player.getY()].setBackground(Color.gray);
					// check
					break;
				}
				case KeyEvent.VK_DOWN:{
					player.x += 1;
					break;
				}
				case KeyEvent.VK_LEFT:{
					if(player.y == 0) {
						JOptionPane.showMessageDialog(null, "미로의 가장 왼쪽입니다.");
					}
					break;
				}
				case KeyEvent.VK_RIGHT:{
					if(player.y == 7) {
						JOptionPane.showMessageDialog(null, "미로의 가장 오른쪽입니다.");
					}
					break;
				}
				}
				
			}
		};
		
		setVisible(true);
		
	}
	
	public static void main(String[] args) {
		new Quiz01();
	}

}

```
