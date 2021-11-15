# Day 2



---

## Review



### JDBC

> 사용자 이용 (프로그램 - 자바) + DB

- 자바언어  ---> OS 독립적(win, mac, linux 등) + 플랫폼 독립적(hw, os)
- **JDBC**  ---> DB 독립적
  - DB JDBC driver 호출
    - oracal jdbc driver
    - mysql jdbc driver

- 기본 라이브러리 제공 + **ojdbc6.jar** (라이브러리 경로에 추가) ---> jdk 1.6 이상
- spring + mybatis  ---> ojdbc8.jar
- Connection  ---> Statement, PreparedStatement  --->  ResultSet

```java
Class.forName("oracle.jdbx.driver.OracleDriver");  // 드라이버 호출
Connection con =
DriverManage.getConnection("DB마다 상이/jdbdc:oracle:thin:@db ip:1521:xe", "계정", "암호");

Statement st = con.createStatement();  ---> sql 저장 / 전송
    
int rows = st.executeUpdate(dml : "insert | update | delete");

ResultSet rs = st.executeQuery("select");
while(rs.next()) {
 ...   
}
```

- **sql.ResultSet** : get + 타입명();  ---> Date, Double, Int 등
- **sql.Connection** 객체 생성
  - jdbc 프로그램 = **dml 자동 commit**  <--->  run sql command line = commit /  rollback 필요
  - command line 사용중 jdbc로 동일 데이터 수정시 commit과 rollback이 필요
- **Connection con**
  - con.close(),  con.createStatement(),   con.prepareStatement()
  - con.setAutoCommit(true / false) : 자동 / 수동 commit  ---> **자동이 기본**
  - 수동 : con.commit(),  con.rollback()





---



## java.sql



#### java.sql.PreparedStatement

- interface PreparedStatement extends Statement

  ===> 상속 그대로 포함 / 오버라이딩 / 추가 메소드

- executeUpdate()  ---> int

- executeQuery()  ---> ResultSet

  - tcl - jdbc sql
  - 이클립스 data explorer  ---> sql 작성 - 실행 - 결과 조회

  ```java
  Statement st = con.createStatement();
  
  ResultSet rs = st.executeQuery
  ("select id from emp where id = 100")
  rs.next();
  rs.getXxxx("id");
  ...
  rs = st.executeQuery
  ("select id from emp where id = 200");
  rs.next();
  rs.getXxxx("id");
  ```

  - db sql 전송받아서 실행 단계
    1. 구문 문법 분석 = parsing
    2.  컴파일(텍스트 ---> 이진코드 변환)
    3.  실행 결과 리턴
  -  ( 1~3 반복 )  =====> 1, 2 실행 후 저장 대기 반복x 구현(아래)

  ```java
  PreparedStatement pt = con.prepareStatement  // sql 미리전송 (재사용 목적)
  ("select id from emp where id = ?"); // creat와는 달리 미리 sql문장 삽입
  
  pt.setInt(1, 100);  ---> ?에 100 값을 줌
  ResultSet rs = pt.executeQuery();
  rs.next();
  rs.getXxxx("id");
  ...
  pt.setInt(1, 200);  ---> ?에 200 값을 줌 (재사용)
  ResultSet rs = pt.executeQuery();
  rs.next();
  rs.getXxxx("id");
  ...
  ```

  

​     



## Data Explorer

> 이클립스 내부에서 run sql command line 툴 사용

































































