# Question
Pokemon 클래스 

	멤버변수 : name, level, hp(체력), ap(공격력)
  
	멤버메서드 : 
		0. Pokemon(name)
			name을 등록 
		   Pokemon(name, level)
			name, level 등록
			체력은 레벨의 1000배
			공격력은 레벨의 1.5배 (20% 확률로 2배)
      
		1. setInfo()
			인자값 : 이름, 레벨
			하는 일 : 인자로 들어온 값들을 멤버변수 name, level 에 모두 저장 
				체력은 레벨의 1000배
				공격력은 레벨의 1.5배 (20% 확률로 2배)
			리턴값 : X
      

		2. getInfo()
			인자값 : X
			하는 일 : "XXX / Lv. @@ / HP. ####" 형태로 name, level, hp 의 값들을 하나의 문자열로 표현
			리턴값 : "XXX / Lv. @@ / HP. ####" 형태의 문자열


		3. levelUp()
			인자값 : X
			하는 일 : level을 1증가
			리턴값 : 증가된 level


		4. isAlive()
			인자값 : X
			하는 일 : 객체의 생사여부 확인( 체력이 0 이하면 죽음 )
			리턴값 : 살아있으면 true, 아니면 false


		5. attack()
			인자값 : 적 포켓몬 객체 (Pokemon형)
			하는 일 : 상대 포켓몬의 체력을 이 객체의 공격력만큼 감소
				10% 확률로 치명타 (공격력 X 1.5배)
			리턴값 : 없음
  
 # SourceCode
```java
package day12.quiz;

class Pokemon{
	String name;
	int level;
	int hp;
	double ap;
	
	Pokemon(String name){
		this.name = name;
	}
	
	Pokemon(String name, int level){
		this.setInfo(name, level);
	}
	
	void setInfo(String name, int level) {
		this.name = name;
		this.level = level;
		this.hp = level*1000;
		this.ap = (Math.random()>0.2 ? level*2 : level*1.5);
	}
	
	String getInfo() {
		return this.name + " / Lv. " + this.level + " / HP. " + this.hp + " / AP. " + this.ap;
	}
	
	int levelUp() {
		++this.level;
		setInfo(this.name, this.level);
		return this.level;
	}
	
	boolean isAlive() {
		return this.hp<0;
	}
	
	void attack(Pokemon p) {
		p.hp -= (Math.random()<0.1 ? this.ap*1.5 : this.ap);
	}
}
public class quiz01 {

}
```
