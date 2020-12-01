```java
package day25.homework.thread;

public class Main {
	private final int NUMBER_OF_PEOPLE = 10;
	private final int NUMBER_OF_MACHINES = 2;
	private final ThreadGroup group;
	private final Thread[] threads = new Thread[NUMBER_OF_PEOPLE];
	private final VendingMachine[] machines = new VendingMachine[NUMBER_OF_MACHINES];
	
	public Main() {
		// ThreadGroup 생성
		group = new ThreadGroup("People");

		// VendingMachine 생성
		for(int i = 0; i < NUMBER_OF_MACHINES; ++i) {
			machines[i] = new VendingMachine("[" + i + "]번 자판기");
		}
		
		// Person Thread NUMBER_OF_MACHINES개 생성
		for (int i = 0; i < NUMBER_OF_PEOPLE; ++i) {
			threads[i] = new PersonThread(machines, group, "\'" + i + "번 사람\'");
		}
		
		for(Thread t : threads) {
			try {
				Thread.sleep(500); // 헷갈려서 각 쓰레드마다 0.5 마다 실행시킴
			} catch (InterruptedException e) {
				e.printStackTrace();
			} 
			t.start();
		}
	}

	public static void main(String[] args) {
		new Main();
	}
}
```
