# Explain

## SourceCode
```java
package day29.homework;

import java.awt.BorderLayout;
import java.awt.FlowLayout;
import java.awt.GridLayout;
import java.awt.LayoutManager;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.SimpleDateFormat;
import java.util.Date;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JTextArea;

class MyButton extends JButton{
	private String menuName;
	private int price;

	MyButton(String menuName, int price){
		this.menuName = menuName;
		this.price = price;
	}
}

class TimeThread extends Thread{
	SimpleDateFormat df = new SimpleDateFormat("yyyy년 MM월 dd일\nHH시mm분ss초");
	Date date = new Date();
	JLabel timela;

	@Override
	public void run() {
		while(true)
		{		
			timela = new JLabel(df.format(date));
		}
	}
}

public class Homework01 extends JFrame{

	// components
	int totalPrice = 0;

	JPanel northP = new JPanel();
	JPanel rightP = new JPanel();
	JPanel leftP = new JPanel();
	JPanel southP = new JPanel();

	JLabel total;
	JTextArea orderList = new JTextArea();
	//	
	//	MyButton btn1 = new MyButton("아메리카노", 3000);
	//	MyButton btn2 = new MyButton("돌체라떼", 4000);
	//	MyButton btn3 = new MyButton("다크초콜릿", 3000);
	//	MyButton btn4 = new MyButton("녹차", 1000);
	//	MyButton btn5 = new MyButton("둥글레차", 2000);
	//	
	JButton[] btns = {
			new JButton("아메리카노"),
			new JButton("돌체라떼"),
			new JButton("다크초콜릿"),
			new JButton("녹차"),
			new JButton("둥글레차"),
	};

	JButton saveBtn = new JButton("저장하기");
	JButton loadBtn = new JButton("불러오기");
	JButton payBtn = new JButton("결제하기");

	ActionListener listener = new ActionListener() {

		@Override
		public void actionPerformed(ActionEvent e) {
			String name = e.getActionCommand();
			int price = 0;

			switch(name) {
			case "아메리카노":{
				price = 3000;
				break;
			}
			case "돌체라떼":{
				price = 4000;
				break;
			}
			case "다크초콜릿":{
				price = 3000;
				break;
			}
			case "녹차":{
				price = 2000;
				break;
			}
			case "둥글레차":{
				price = 1000;
				break;
			}

			}

			totalPrice += price;
			total.setText("총 결제액 : " + totalPrice + "원");
			String temp = orderList.getText();
			orderList.setText(temp + name + " : " + price + "원\n");
		}
	};


	private void initNorthPanel() {
		northP.setLayout(new GridLayout(1, 3, 10, 10));
		northP.add(saveBtn);
		northP.add(loadBtn);
		northP.add(payBtn);
	}

	private void initSouthPanel() {
		southP.setLayout(new BorderLayout());
		JPanel priceP = new JPanel();
		JPanel timeP = new JPanel();
		TimeThread tt = new TimeThread();

		priceP.add(total = new JLabel("총 결제액 : " + totalPrice));
		tt.start();

		southP.add(priceP, BorderLayout.WEST);
		southP.add(timeP, BorderLayout.EAST);
	}

	private void initRightPanel() {
		rightP.setLayout(new GridLayout());
		JLabel orderTitle = new JLabel("* 주문 내역 *\n");
		rightP.add(orderTitle);
	}

	private void initLeftPanel() {
		leftP.setLayout(new GridLayout(5, 1, 40, 40));

		for(JButton b:btns) {
			b.addActionListener(listener);
			leftP.add(b);
		}
	}

	public Homework01() {
		super("음료 주문하기");
		orderList.setEditable(false);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setSize(1200, 800);
		setLocationRelativeTo(null);
		setLayout(new BorderLayout());

		initNorthPanel();
		initLeftPanel();
		initRightPanel();
		initSouthPanel();

		add(southP, BorderLayout.SOUTH);
		add(northP, BorderLayout.NORTH);
		add(rightP, BorderLayout.CENTER);
		add(leftP, BorderLayout.WEST);

		setVisible(true);
	}

	public static void main(String[] args) {
		new Homework01();
	}
}

```
