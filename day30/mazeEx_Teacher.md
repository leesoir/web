```java
package day30.homework;

import java.awt.Color;
import java.awt.GridLayout;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JOptionPane;

public class Homework01 extends JFrame implements KeyListener {


	private static final int ROAD = 0;
	private static final int WALL = 1;
	private static final int START = 2;
	private static final int END = 3;
	private static final int CURRENT = 4;

	private static final int ROW = 8;
	private static final int COL = 8;

	private int x = 0;
	private int y = 0;

	private static final Color[] COLOR = { 
			new Color(250, 237, 239),  // ROAD 의 색상
			new Color(33, 32, 32), 	   // WALL 의 색상
			new Color(235, 52, 82),    // START 의 색상
			new Color(74, 52, 237),    // END 의 색상
			new Color(207, 52, 235)    // CURRENT 의 색상
			};

	private static final int[][] MAP = { 
			{ START, ROAD, WALL, WALL, WALL, ROAD, WALL, ROAD },
			{ ROAD, ROAD, ROAD, ROAD, WALL, ROAD, WALL, ROAD }, 
			{ WALL, WALL, WALL, ROAD, ROAD, ROAD, ROAD, ROAD },
			{ WALL, ROAD, ROAD, ROAD, WALL, ROAD, WALL, ROAD }, 
			{ WALL, WALL, WALL, ROAD, WALL, WALL, WALL, ROAD },
			{ ROAD, ROAD, ROAD, ROAD, ROAD, ROAD, WALL, END }, 
			{ ROAD, WALL, WALL, WALL, WALL, WALL, WALL, ROAD },
			{ ROAD, ROAD, ROAD, ROAD, ROAD, ROAD, ROAD, ROAD }, 
			};

	private JButton[][] btnMap;

	private void initMap() {
		btnMap = new JButton[ROW][COL];
		for (int i = 0; i < ROW; ++i) {
			for (int j = 0; j < COL; ++j) {
				JButton btn = new JButton();
				btn.setBackground(COLOR[MAP[i][j]]);
				btn.setEnabled(false);
				btnMap[i][j] = btn;
			}
		}
	}

	public Homework01() {
		initMap();
		setSize(500, 500);
		setLocationRelativeTo(null);
		setLayout(new GridLayout(ROW, COL));
		setDefaultCloseOperation(EXIT_ON_CLOSE);

		for (JButton[] btns : btnMap) {
			for (JButton btn : btns) {
				add(btn);
			}
		}

		addKeyListener(this);
		setVisible(true);
	}

	@Override
	public void keyTyped(KeyEvent e) {
	}

	@Override
	public void keyPressed(KeyEvent e) {
		btnMap[y][x].setBackground(COLOR[MAP[y][x]]); // 이동 하기전, 현재 칸의 색상을 원래 색상으로 재설정
		switch (e.getKeyCode()) { // 무슨 키가 눌렸니?
		case KeyEvent.VK_UP:
		case KeyEvent.VK_W:
			if (y > 0 && MAP[y-1][x] != WALL)  // 현재 row가 0번이거나, 윗 칸이 벽이면 안된다.
				--y;
			break;
		case KeyEvent.VK_DOWN:
		case KeyEvent.VK_S:
			if (y < ROW-1 && MAP[y+1][x] != WALL)  // 현재 row가 7번이거나, 아랫칸이 벽이면 안된다.
				++y;
			break;
		case KeyEvent.VK_RIGHT:
		case KeyEvent.VK_D:
			if (x < COL-1 && MAP[y][x+1] != WALL)
				++x;
			break;
		case KeyEvent.VK_LEFT:
		case KeyEvent.VK_A:
			if (x > 0 && MAP[y][x-1] != WALL)
				--x;
			break;
		default:
			break;

		}
		btnMap[y][x].setBackground(COLOR[CURRENT]); // (변경된) 현재 좌표를 CURRENT 색으로 설정
		if (MAP[y][x] == END) { // 도착지면 
			JOptionPane.showMessageDialog(this, "도착!");
		}
	}

	@Override
	public void keyReleased(KeyEvent e) {
	}

	public static void main(String[] args) {
		new Homework01();
	}
}
```
