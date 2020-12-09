## MEMBER table 만들기
### 조건
* 항목 : 회원번호(no), 아이디(id), 패스워드(password), 이메일(email), 등급(type), 적립금(point)
* 제약조건 : 

		Primary key 는 회원번호다.
		아이디는 중복이면 안된다. (UNIQUE) 
		이메일도 중복이면 안된다. (UNIQUE) 
		아이디는 누락되면 안된다. (NOT NULL)
		등급은 1 ~ 4가 있고 기본값은 1이다.
		적립금은 1000원이 기본값이고 음수일 수 없다.
		

### SourceCode 
```mysql
MariaDB [testdb]> CREATE TABLE MEMBER(
    -> no INT(3) PRIMARY KEY AUTO_INCREMENT,
    -> id VARCHAR(40) NOT NULL UNIQUE,
    -> password VARCHAR(40) NOT NULL,
    -> email VARCHAR(40) NOT NULL UNIQUE,
    -> type INT(1) DEFAULT 1,
    -> point INT(6) UNSIGNED DEFAULT 1000
    -> );
Query OK, 0 rows affected (0.056 sec)

MariaDB [testdb]> DESC MEMBER;
+----------+-----------------+------+-----+---------+----------------+
| Field    | Type            | Null | Key | Default | Extra          |
+----------+-----------------+------+-----+---------+----------------+
| no       | int(3)          | NO   | PRI | NULL    | auto_increment |
| id       | varchar(40)     | NO   | UNI | NULL    |                |
| password | varchar(40)     | NO   |     | NULL    |                |
| email    | varchar(40)     | NO   | UNI | NULL    |                |
| type     | int(1)          | YES  |     | 1       |                |
| point    | int(6) unsigned | YES  |     | 1000    |                |
+----------+-----------------+------+-----+---------+----------------+
6 rows in set (0.071 sec)
```


## QNA table 만들기
### 조건

* 항목 : 질문번호(no), 글쓴이번호(writer_no), 질문 내용(content), 등록일자(regdate)

* 제약조건 : 

		Primary key 는 질문번호다.
		글쓴이번호는 MEMBER 테이블의 회원번호를 참조한다. (FOREIGN KEY)
		글쓴이 회원이 삭제되면 해당 질문도 삭제된다. (CASCADE)	
		질문 내용은 누락되면 안된다.
		등록일자는 기본값이 현재 시간이다. 

### SourceCode 
```mysql
MariaDB [testdb]> CREATE TABLE QNA(
    -> no INT(3) PRIMARY KEY AUTO_INCREMENT,
    -> writer_no INT(3),
    -> content VARCHAR(1000) NOT NULL,
    -> regdate DATETIME DEFAULT CURRENT_TIMESTAMP,
    -> FOREIGN KEY(writer_no)
    -> REFERENCES MEMBER(no) ON UPDATE CASCADE
    -> );
Query OK, 0 rows affected (0.032 sec)

MariaDB [testdb]> DESC QNA;
+-----------+---------------+------+-----+---------------------+----------------+
| Field     | Type          | Null | Key | Default             | Extra          |
+-----------+---------------+------+-----+---------------------+----------------+
| no        | int(3)        | NO   | PRI | NULL                | auto_increment |
| writer_no | int(3)        | YES  | MUL | NULL                |                |
| content   | varchar(1000) | NO   |     | NULL                |                |
| regdate   | datetime      | YES  |     | current_timestamp() |                |
+-----------+---------------+------+-----+---------------------+----------------+
```
