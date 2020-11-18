# 11.18 숙제
1. 깊은 복사와 얕은 복사 조사하기  
할아버지 : 홍길동 70세, 할머니 : 김피카츄 65세 
어머니 : 김피츄 35세, 아버지 : 홍또도가스 40세
아들 : 홍뚜벅초 10세, 딸 : 홍푸린 5세

푸린 객체 생성 시 깊은 복사/얕은 복사 중 어떤 것을 해야하는지 생각하고, 푸린 객체를 뚜벅초 객체의 복사를 통해 구현하라.

```java
package day18.homework;

class Person{
	String name;
	int age;
	Person father;
	Person mother;

	public Person() {

	}

	Person(String name, int age){
		this.name = name;
		this.age = age;
	}
	
	void setParents(Person mother, Person father) {
		this.mother = mother;
		this.father = father;
	}

}

public class Quiz01 {
	// 할아버지 : 홍길동 70세, 할머니 : 김피카츄 65세
	// 어머니 : 김피츄 35세, 아버지 : 홍또도가스 40세
	// 아들 : 홍뚜벅초 10세, 딸 : 홍푸린 5세

	Person granpa = new Person("홍길동", 70);
	Person granma = new Person("김피카츄", 65);
	
	Person mom = new Person("김피츄", 35);
	mom.setParents(granma, granpa);
	
	Person father = new Person("홍또도가스", 40);
	

	// 동일한 어머니, 아버지를 둔 뚜벅초와 푸린을 생성 시 
	Person son = new Person("홍뚜벅초", 10);
	son.father = fatherPerson;
	son.mother = motherPerson;

	// 푸린 객체 생성 시 깊은 복사/얕은 복사 중 어떤 것을 해야하는지 생각하고, 푸린 객체를 뚜벅초 객체의 복사를 통해 구현하라.
}
```
