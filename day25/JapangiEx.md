# Explain
동기 (synchronized) 사용하여 자판기 구현하기 

1) 자판기는 2개가 있다.

2) 사람쓰레드는 10개가 있다.

3) 자판기에서 음료를 뽑는 시간은 3초다.

4) 사람쓰레드는 1번 자판기를 우선적으로 선택하되 자판기가 사용중이라면 2번 자판기를 사용한다.

2번 자판기도 사용중이라면 1번 자판기로 가서 기다린다.

1, 2 번 자판기 중 먼저 사용가능한 자판기를 선택하여 사용한다.
## 11.29
자판기 객체를 2개 만들어서 어떻게 해야 할 지 감이 안잡힌다. 문제 이해를 못한 것 같다.. 

# SourceCode
```java
package day25.homework;

class Japangi{
	private static int DRINK = 5;
	String name;
	
	synchronized static void putDrink(String name) {
		if(DRINK == 0) {
			System.out.println("남은 음료수가 없음!");
			return;
		}
		
		System.out.println(name + "이 음료를 뽑음 : 남은 음료는 " + --DRINK + "개");
		try {
			Thread.sleep(3000);
		}catch(InterruptedException e) {
			e.printStackTrace();
		}
		System.out.println(name + "의 음료수 뽑기 끝");
	}
}

class PersonThread extends Thread{
	@Override
	public void run() {
		putDrink(getName());
	}
}

public class Quiz01 {
	public static void main(String[] args) {
		
		// 자판기 2개
		Japangi j1 = new Japangi();
		Japangi j2 = new Japangi();
		
		// 사람 스레드 10개
		PersonThread p1 = new PersonThread();
		PersonThread p2 = new PersonThread();
		PersonThread p3 = new PersonThread();
		PersonThread p4 = new PersonThread();
		PersonThread p5 = new PersonThread();
		PersonThread p6 = new PersonThread();
		PersonThread p7 = new PersonThread();
		PersonThread p8 = new PersonThread();
		PersonThread p9 = new PersonThread();
		PersonThread p10 = new PersonThread();
		
		// 이름 임의 지정
		p1.setName("사람 1");
		p2.setName("사람 2");
		p3.setName("사람 3");
		p4.setName("사람 4");
		p5.setName("사람 5");
		p6.setName("사람 6");
		p7.setName("사람 7");
		p8.setName("사람 8");
		p9.setName("사람 9");
		p10.setName("사람 10");
		
		
		p1.start();
		p2.start();
		p3.start();
		p4.start();
		p5.start();
		p6.start();
		p7.start();
		p8.start();
		p9.start();
		p10.start();
		
		
		
	}

}
```
