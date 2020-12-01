```java
package day25.homework.thread;

public class PersonThread extends Thread {

	private VendingMachine[] machines;

	public PersonThread(VendingMachine[] machines, ThreadGroup group, String name) {
		super(group, name);
		this.machines = machines;
	}

	@Override
	public void run() {
		try {
			VendingMachine chosenMachine = machines[0];
			for (VendingMachine machine : machines) {
				if (chosenMachine.getSecond() > machine.getSecond()) {
					chosenMachine = machine;
					continue; // 더 빨리 뽑을 수 있는 자판기가 있는지 더 확인한다.
				}
				if (!machine.isOccupied()) {
					chosenMachine = machine;
					break; // 현재 사용가능한 자판기라면 바로 사용하기 위해 반복을 종료한다.
				}
			}
			System.out.println("\t" + this.getName() + "(은)는 " + chosenMachine.getName() + "를 선택하였습니다.(대기 시간 : "
					+ chosenMachine.getSecond() + "초)");
			chosenMachine.enqueue(this);
		} catch (NullPointerException e) {
			e.printStackTrace();
		}
	}

	@Override
	public String toString() {
		return getName();
	}
}
```
