# Java_JDBC_Basic

---

데이터의 영구 저장  ===> DB

자바프로그램 ---> 파일 ---> ???ㅍ로그램

 EX. 프로그램 독립적 데이터 저장 / 정해진 형식 취급 / 영구 저장

DB 테이블 정의 컬럼 타입(길이) 제약조건







- 자바프로그램에서 DB 저장/조회 기능 ===> JDBC
  - JAVA DATABASE CONNETIVITY 
  - jdk, oracle db, mysql db  ---> oracle사 제공   

```java
interface Connection {
    voidn connect();
}
class oracle jdbc driver implements Connection {
    public void connect;
}
class mysql jdbc driver implements Connection {
    public void connect;
}
```





```java
Statement st = con.createStatement();
int rows = st.executeUpdate("dml");
```



```java
Connection con = DriverManager.getConnection()
```

JDBC 전송 SQL

DDL  ---> 가능. 권장 X

DCL  ---> 계정 가능, 권장 X

DML  ---> JDBC SQL



INSERT / UPDATE / DELETE  ===> 







java.sql.Connection

java.sql.Statement st = con.createStatement();

java.sql.ResultSet



| JAVA          | ResultSet                        | ORACLE                            |
| ------------- | -------------------------------- | --------------------------------- |
| INT           | getInt("컬럼명"), String 가능    | NUMBER(N)                         |
| DOUBLE        | getDouble("컬럼명"), String 가능 | NUMBER(N, S)                      |
| Strin         | getString("컬럼명")              | VARCHAR2(N)                       |
| java.sql.datr | getDate = "컬럼명"               | DATE ' RR/MM;'                    |
|               | getString("indate")              | SELECT TO_CHAR (날짜데이터, 포맷) |



```java
while(rs.next()) {
    int id = rs.getInt*(1);  ---> rs.getInt("id")
    or
    String id = rs.getString(1)  ---> "100"
    String name = rs.getString("name");
    double salary = rs.getDouble("salay. ")
}
```



rs.next();  : boolean , rs의 다음 레코드로 이동





class EmpDAO

void getEmp() {

driver 로딩

db 연결

sql 전송

emp 테이블의 모든 레코드 조회 sql 결과 검색

// db 해제

}





- **xxxxVO** = VALUE OBJECT = 값 저장 / 추출 용도 **객체**

  - VO = DO = DTO 동일!!

  - EMP테이블  ===> EmpVO
  - EmpDO : DATA OBJECT
  - EmpDTO : DATA TRANSFER OBJECT

- **xxxxDAO** = DATA ACCESS OBJECT = 값 **접근 용도** 객체(직접연결)

  - 자바 <---  JDBC <---  DB값
  - 자바 <---  파일 입력(java.io.FileReader) <---  파일 값


