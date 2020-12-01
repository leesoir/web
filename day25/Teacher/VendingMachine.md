```java
package day25.homework.thread;

import java.util.Queue;
import java.util.concurrent.LinkedBlockingQueue;

public class VendingMachine {
	private final int DURATION_TIME_SECOND = 3;
	private boolean isOccupied;
	private int second;
	private String name;
	
	// 현재 대기중인 사람 목록 (없어도 됨.)
	private Queue<PersonThread> queue = new LinkedBlockingQueue<>();
	
	
	public VendingMachine(String name) {
		this.name = name;
	}
	public String getName() {
		return name;
	}
	
	
	private void reset() {
		isOccupied = false;
	}

	public void enqueue(PersonThread occupant) {
		isOccupied = true;
		second += DURATION_TIME_SECOND;
		queue.add(occupant);
		System.out.println("\t" + occupant.getName() + "(이)가 " + name + "사용을 대기합니다. (대기중 인원 : " + queue);
		
		synchronized (this) {
			try {
				System.out.println("\t" + occupant.getName() + "(이)가 " + name + "을 사용합니다.");
				for (int i = DURATION_TIME_SECOND; i > 0; --i) {
					System.out.println(name + ":" + i + "초 남음, 현재 총 대기 시간 : " + second + "초");
					--second;
					Thread.sleep(1000);
				}
				queue.poll(); // 가장 앞 원소 삭제
				System.out.println("\t" + occupant.getName() + "(이)가 자판기 사용을 완료하였습니다.(대기중 인원 : " + queue);
				reset();
			} catch (InterruptedException e) {
				System.out.println("\t" + occupant.getName() + "의 사용이 중지되었습니다.");
			}
		}
	}
	public boolean isOccupied() {
		return isOccupied;
	}

	public int getSecond() {
		return second;
	}
}
```
