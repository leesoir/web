# 11.18 숙제
1. 깊은 복사와 얕은 복사 조사하기  
할아버지 : 홍길동 70세, 할머니 : 김피카츄 65세 
어머니 : 김피츄 35세, 아버지 : 홍또도가스 40세
아들 : 홍뚜벅초 10세, 딸 : 홍푸린 5세

푸린 객체 생성 시 깊은 복사/얕은 복사 중 어떤 것을 해야하는지 생각하고, 푸린 객체를 뚜벅초 객체의 복사를 통해 구현하라.

```java
package day18.homework;

class Person{
	private String name;
	private int age;
	private Person father;
	private Person mother;
	
	
	//constructorss
	public Person() {
		this("", 0);
	}

	Person(String name, int age){
		this.name = name;
		this.age = age;
		this.setParents(null, null);
	}
	
	
	// getters and setters
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public Person getFather() {
		return father;
	}

	public void setFather(Person father) {
		this.father = father;
	}

	public Person getMother() {
		return mother;
	}

	public void setMother(Person mother) {
		this.mother = mother;
	}
	
	
	// methods
	void setParents(Person mother, Person father) {
		this.mother = mother;
		this.father = father;
	}
	
	@Override
	public String toString() {
		return "이름 " + this.getName() + ", 나이 " + this.getAge() + "\n";
	}

}

public class Quiz01 {
	// 할아버지 : 홍길동 70세, 할머니 : 김피카츄 65세
	// 어머니 : 김피츄 35세, 아버지 : 홍또도가스 40세
	// 아들 : 홍뚜벅초 10세, 딸 : 홍푸린 5세

	Person granpa = new Person("홍길동", 70);
	Person granma = new Person("김피카츄", 65);
	
	Person mom = new Person("김피츄", 35);
	Person dad = new Person("홍또도가스", 40);
	mom.setParents(grandma, grandpa);
	dad.setParents(grandma, grandpa);
	

	// 푸린 객체 생성 시 깊은 복사/얕은 복사 중 어떤 것을 해야하는지 생각하고, 푸린 객체를 뚜벅초 객체의 복사를 통해 구현하라.
	
	Person daughter = new Person("홍푸린", 5);
	Person son = new Person("홍뚜벅초", 10);
	daughter.setParents(mom, dad);
	son.setParents(mom, dad);
	
	// question : 푸린 객체의 생성 시 deep copy와 light copy 중 어느 것을 사용하여야 하는가?
	// heejin : light copy(객체 레퍼런스 참조). 
	// daughter.mother = mom; // mom 객체의 래퍼런스 값이 dauther.mother에 들어간다. 두 객체는 같은 레퍼런스를 참조한다.
	// 그러나 이 경우 daughter.mother.age = 를 통해 정보를 본인이 아닌 객체가 함부로 바꿀 수 있다.
	
	// +) 아니면 해당 dauhter.mother.age/name값을 복사(deep copy)해와서 새로운 객체를 만들어 mother/father값에 할당해줘야 하나 ? 
	// 어느 쪽이 더 나은 방법인지 모르겠다. 
}
```


# thinking : deep copy와 light copy를 통한 푸린 객체의 생성
```java
// 1. light copy
Person daughter = new Person("홍푸린", 5); 
daughter.setParents(mom, dad); 
// setParents 메소드를 통해 푸린의 mother, father 필드를 지정한다. 이 때 mother/father에는 mom, dad 객체의 래퍼런스가 들어가며 두 객체는 같은 주소를 참조한다.
// 이 경우 푸린.mother의 값이 변경되면 mom의 정보도 변경되므로, 딸이 엄마아빠의 정보를 함부로 바꿀 수 있다.

// 2. deep copy
Person daughter = new Person("홍푸린", 5);
daughter.setMother(new Person(mom.getName(), mom.getAge()));
daughter.setFather(new Person(dad.getName(), dad.getAge()));
// 이렇게 되면 깊은 복사를 통해 mom, dad의 이름과 age 값만 가져와 새로운 Person 객체를 생성하여 mother, father 필드에 할당하게 된다. 
// 깊은 복사를 통해 필드 값을 할당하면 본래 객체의 정보를 변경할 수 없다. daughter.mother와 mom 객체는 전혀 다른 객체이다.
```
어떤 것이 더 좋은 방법일까?
