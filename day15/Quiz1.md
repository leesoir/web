```java
package com.javalec.quiz;
/*
 * 부모클래스 : Book 
 *   필드 : 책이름, 저자, 가격
 *   메소드 : printData() - 책이름, 저자, 가격 정보를 sysout
 *           setData() - 인자값 3개(책이름, 저자, 가격)를 받아서 
 *                       각 필드에 저장해주는
 * 자식클래스 : 
 *  1) Novel 
 *   필드 : 책이름, 저자, 가격, 장르
 *  2) Comic 
 *   필드 : 책이름, 저자, 가격, 주인공 이름, 장르
 *  3) Textbook 
 *   필드 : 책이름, 저자, 가격, 출판사, 과목
 * 
 * 메인메소드에서.. 
 * 자식클래스 3개를 모두 객체 생성 1개씩 하고 
 * 각 필드에 값 저장, 출력해서 확인 (입력 필요 X)
 */


class Book{
	String name;
	String author;
	int price;
	
	public void printdata() {
		System.out.println("책 이름 : " + this.name + " / 저자 : " + this.author + " / 가격 : " + this.price);
	}
	
	public void setData(String name, String author, int price) {
		this.name = name;
		this.author = author;
		this.price = price;
	}
}

class Novel extends Book{ // 필드 : 책이름, 저자, 가격, 장르
	String genre;
	
	//constructors
	Novel(){
		
	}
	
	Novel(String name, String author, int price, String genre){
		this.setData(name, author, price);
		this.genre = genre;
	}
}

class Comic extends Novel{ // 필드 : 책이름, 저자, 가격, 주인공 이름, 장르
	String heroName;
	
	Comic(){
		
	}
	
	Comic(String name, String author, int price, String genre, String heroName){
		super(name, author, price, genre);
		this.heroName = heroName;
	}
}

class Textbook extends Book{ // 필드 : 책이름, 저자, 가격, 출판사, 과목
	String publiser;
	String subject;
	
	Textbook(){
		
	}
	
	Textbook(String name, String author, int price, String publiser, String subject){
		this.setData(name, author, price);
		this.publiser = publiser;
		this.subject = subject;
	}
}

public class Quiz01 {
	public static void main(String[] args) {
		Novel novel = new Novel();
		Comic comic = new Comic();
		Textbook textbook = new Textbook();
		
		novel.setData("나미야 잡화점의 기적", "히가시노 게이고", 9000);
		comic.setData("작은 아씨들", "루이자 메이 알코트", 14220);
		textbook.setData("슬기로운 생활", "대한민국", 5000);
		
		novel.printdata();
		comic.printdata();
		textbook.printdata();
	}
}
```
