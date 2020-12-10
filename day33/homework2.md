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
    -> type INT(1) DEFAULT 1 CHECK(type>=1 && type<=4),
    -> point INT(6) UNSIGNED DEFAULT 1000
    -- 또는 CHECK(point >=0)를 통해 검사 가능
    -- 보통 제약조건들은 순서가 없으나, DEFAULT문은 CHECK문의 앞에 존재해야 한다.
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
    -> content TEXT NOT NULL,
    -- 글이 길어질 수 있으므로 VARCHAR보다는 TEXT 타입을 사용하는 것이 좋다. 
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

### 외래 키(FOREIGN KEY)
QNA 테이블의 writer_no 필드는 MEMBER 테이블의 no 필드를 참조한다. 이 경우 두 필드의 데이터 타입은 같아야 하며, writer_no는 QNA 테이블의 외래 키(foreign key)라고 한다. 
CASCADE 키워드를 사용할 경우 외래 키가 참조하는 테이블의 필드값이 변경될 경우 해당 필드값을 참조하는 다른 테이블들의 레코드들도 수정 및 삭제된다. 
```mysql
FOREIGN KEY(writer_no) REFERENCES MEMBER(no) UPDATE CASCADE; -- 필드값이 변경되면 함께 수정된다.
FOREIGN KEY(writer_no) REFERENCES MEMBER(no) DELETE CASCADE; -- 필드값이 삭제되면 함께 삭제된다.
```
