# Explain
getter랑 setter에는 그냥 바로 멤버변수값 가져오면 되는데 왜 getter/setter 또 사용한건지 모르겟다... 바보같당

# SourceCode
```java
package day13.test;
class Pokemon {

	//field
	private String name;
	private int level;
	private int hp;
	private int ap;


	//getters and setters
	public String getName() {
		return name;
	}

	public void setName(String name) {
		if(name.length() > 10) {
			return;
		}
		this.name = name;
	}

	public int getLevel() {
		return level;
	}

	public void setLevel(int level) {
		if(level > 1000) {
			return;
		}
		this.level = level;
	}

	public int getHp() {
		return hp;
	}

	public void setHp(int hp) {
		this.hp = hp;
	}

	public int getAp() {
		return ap;
	}

	public void setAp(int ap) {
		this.ap = ap;
	}


	// methods
	Pokemon(String name){
		this(name, 0);
	}

	Pokemon(String name, int level){
		this.setInfo(name, level);
	}

	void setInfo(String name, int level) {
		this.setName(name);
		this.setLevel(level);
		this.setHp(level*1000);
		this.setAp((int)(Math.random()>0.2 ? this.getLevel()*2 : this.getLevel()*1.5));
	}

	String getInfo() {
		return this.getName() + " / Lv. " + this.getLevel() + " / HP. " + this.getHp() + " / AP. " + this.getAp();
	}

	int levelUp() {
		this.setLevel(this.getLevel()+1);
		setInfo(this.getName(), this.getLevel());
		return this.getLevel();
	}

	boolean isAlive() {
		return this.getHp()>0;
	}

	void attack(Pokemon p) {
		p.setHp(p.getHp()-(int)(Math.random()<0.1 ? this.ap*1.5 : this.ap));
	}
}

class test {
	public static void main(String[] args) {
		Pokemon p1 = new Pokemon("희진", 3);
		Pokemon p2 = new Pokemon("npc", 2);

		System.out.println(p1.getInfo());
		System.out.println(p2.getInfo());

		System.out.println("공격!");
		p1.attack(p2);
		System.out.println(p2.getInfo());
	}

}
```
