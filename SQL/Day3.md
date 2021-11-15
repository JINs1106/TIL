# Day 3



---

## Review

### JOIN

| SELECT    | 컬럼명 / 2개 이상 테이블 분리                                |
| --------- | ------------------------------------------------------------ |
| **FROM**  | 테이블명1, 테이블2 ---> 테이블1 레코드갯수 * 테이블2 레코드갯수 |
| **WHERE** | 테이블명1.공통컬럼 >= 테이블명2.공통컬럼                     |

|            | ORACLE문법                                 | ANSI문번(표준)                  |
| ---------- | ------------------------------------------ | ------------------------------- |
| INNER JOIN | WHERE E.컬럼 = D.컬럼                      | FROM ~ INNER JOIN ~             |
|            |                                            | ON ~                            |
| OUTER JOIN | WHERE E.컬럼 = D.컬럼(+)                   | LEFT(RIGHT) OUTER JOIN          |
|            | (+) = NULL이 존재하지 않는 곳에 붙임       |                                 |
| SELF JOIN  | WHERE E1.컬럼 = E2.컬럼 (동일 테이블 사용) | INNER JOIN ~ 0N, OUTER JOIN ~ON |



## SUBQUERY : 조회 결과를 또다른 조회 필요

- 단일행 SUBQUERY : SELECT 조회 결과 1개 리턴

- 다중행 SUBQUERY : SELECT 조회 결과 n개 리턴 ( ANY, ALL, = ANY(IN) )



---



## 프로젝트 구현

> 업무 분석 ---> 프로젝트 설계 : 자바, DB 저장, AI  ===> 오라클, 계정, 모델링, 테이블 정의

1. 구매하지 않은 회원의 NULL 컬럼 많다
2. 모든 회원 = 회원테이블
3. 구매한 테이블 = 상품구매테이블
4. NULL컬럼, 중복값 고려





## DDL : 테이블 문법

### CREATE TABLE

```sql
CREATE TABLE 테이블명(
컬럼명 1 타입(길이)
컬럼명 2 타입(길이)
컬럼명 3 타입(길이)
컬럼명 4 타입(길이)
    ...
)
```

- 이름 : 숫자 시작 불가능, 예약어 사용불가능, 30문자 길이 제한

- 타입 : NUMBER(5, 2), VARCHAR2(BYTE), DATE('RR/MM/DD')

- EMP 테이블

  ```sql
  CREATE TABLE emp(
  id NUMBER(5),
  name VARCHAR2(20),
  title VARCHAR2(20),
  dept_id NUMBER(5),
  salary NUMBER(12,2)
  );
  ```

  

### ALTER TABLE

- 테이블 구조 변경(컬럼추가, 수정, 삭제)
- 컬럼 **추가** : ALTER TABLE 테이블명 **ADD** 컬럼명1 타입(길이);
- 컬럼 **삭제**: ALTER TABLE 테이블명 **DROP COLUMN** 컬럼명1 타입(길이);
- 컬럼 **수정**(타입이나 길이): ALTER TABLE 테이블명 **MODIFY** 컬럼명1 타입(길이);
  - 데이터가 삽입되지 않은 상태라면 수정가능
  - 데이터 삽입된 상태에서 컬럼 길이를 줄이는 것은 불가능 할 수 있다. 타입 수정불가

- RENAME COLUMN ~ TO 새이름 (이름 수정) /  



### DROP TABLE

- DROP TABLE 테이블명;
  - 삭제시 영구 삭제(신중)





## DML : 테이블 레코드 대상

| 삽입                                  | 수정                                        | 삭제                                               |
| ------------------------------------- | ------------------------------------------- | -------------------------------------------------- |
| INSERT INTO 테이블명                  | UPDATE 테이블명                             | DELETE 테이블명                                    |
| VALUES(컬럼1값, 2값..); (모든 컬럼)   | SET 컬럼명1 = 변경값; (모든레코드 변경)     | (모든 레코드 삭제. 복구가능)                       |
| VALUES(컬럼 3값, 5값...); (지정 컬럼) | WHERE 변경 조건식 (조건에 맞는 레코드 변경) | WHERE 삭제 조건식(조건 만족 레코드 삭제. 복구가능) |



### INSERT

- CREATE TABLE 테이블명 + AS SELECT ......FROM 테이블명 ;  ---> 다른테이블 데이터 복사

```sql
EMP TABLE 모든 컬럼값 삽입
100 김사원 신입사원 20 1234567890.11 '21/08/16'
200 박대리 3년차대리 20 12345678990.11 '18/08/16'
101 최신입 신입사원 10 1234567890.11, SYSDATE
201 이대리 1년차대리 NULL NULL '2020/12/12'
202 박과장 1년차과장 NULL NULL '01-01-2010'

INSERT INTO EMP VALUES(100, '김사원', '신입사원', 20, 1234567890.11, '21/08/16');
INSERT INTO EMP VALUES(200, '박대리', '3년차대리', 20, 1234567899.11, '18/08/16');
INSERT INTO EMP VALUES(101, '최신입', '신입사원', 20, 1234567890.11, SYSDATE);

INSERT INTO EMP VALUES(201, '이대리', '1년차대리', NULL, NULL, '2020/12/12');
OR INSERT INTO EMP(ID, NAME, TITLE, HIREDATE)
VALUES(201, '이대리', '1년차대리', '2020/12/12');

INSERT INTO EMP(ID, NAME, TITLE, HIREDATE)
VALUES(202, '박과장', '1년차과장', '01-01-2010'); ---> DATE FORMAT 에러
2010/01/01 --> 날짜형식 인정(자동형변환)
TO_DATE('01-01-2010'.'MM-DD-YYYY')
INSERT INTO EMP(ID, NAME, TITLE, HIREDATE)
VALUES(202, '박과장', '1년차과장', TO_DATE('01-01-2010', 'MM-DD-YYYY');
```

- EMP 테이블에서 오늘 입사 사원 이름, 입사일 조회

  ```sql
  SELECT NAME, HIREDATE FROM EMP
  WHERE HIREDATE = SYSDATE;   ======> NO ROWS....???
  SO,
  WHERE TO_CHAR(HIREDATE. 'YY/MM/DD') = TO_CHAR(SYSDATE, 'YY/MM/DD');
  ```

  - SYSDATE  : 연월일요일시분초 구성!!!  ===> 문자타입으로 변환해 원하는 데이터 조회

  

### UPDATE

- 급여 변경

  ```SQL
  박과장의 급여 900000
  UPDATE EMP
  SET SALARY = 900000
  WHERE NAME = '박과장';
  
  신입사원들의 급여 800000
  UPDATE EMP
  SET SALARY = 800000
  WHERE TITLE = '신입사원';
  
  대리들의 급여 850000
  UPDATE EMP
  SET SALARY = 850000
  WHERE TITLE LIKE '%대리%';
  ```



### DELETE

- DELETE EMP WHERE TITLE LIKE '%과장' : 선택적 삭제









### SUBQUERY

- 다른 SQL 문장에 포함 ---> INSERT, UPDATE, DELETE 에도 사용가능

- INSERT

  - EMPLOYEES 테이블의 레코드 몇개를(전부) 복사해서 EMP 테이블에 삽입

    | EMPLOYEES                          | EMP                            |
    | ---------------------------------- | ------------------------------ |
    | EMPLOYEE_ID - NUMBER(5)            | ID - NUMBER(5)                 |
    | FIRST_NAME - VARCHA2(20) --성 제외 | NAME - VARCHAR2(20) -- 성 포함 |

    ```sql
    INSERT INTO EMP VALUES(...)
    
    INSERT INTO EMP SELECT * FROM EMPLOYEES;  ---> 갯수는 EMPLOYEE만큼 107개, 에러
    INSERT INTO EMP
    SELECT EMPLOYEE_ID, FIRST_NAME, JOB_ID, DEPARTMENT_ID, SALARY, HIRE_DATE
    FROM EMPLOYEES
    WHERE SALARY >= 15000;  ===> VALUE의 갯수와 타입이 일치
    ```

- UPDATE

  - STEVEN의 TITLE을 김과장의 TITLE로 변경

    ```SQL
    - 사장으로 변경
    UPDATE EMP SET TITLE = '사장'
    WHERE NAME = 'Steven'
    
    - 박과장의 TITLE로 변경
    UPDATE EMP SET TITLE = (SELECT TITLE FROM EMP WHERE NAME = '박과장')
    WHERE NAME = 'Steven';
    ```

  - STEVEN과 같은 TITLE을 가진 사원의 급여 2배인상

    ```sql
    UPDATE EMP
    SET SALARY = SALARY * 2
    WHERE TITLE = (SELECT TITLE FROM EMP WHERE NAME = 'Steven');
    ```

    

  - 김사원과 같은 TITLE을 가진 사원의 급여를 이대리의 급여로 인상

    ```sql
    UPDATE EMP
    SET SALARY = (SELECT SALARY FROM EMP WHERE NAME = '이대리')
    WHERE TITLE = (SELECT TITLE FROM EMP WHERE NAME = '김사원');
    ```

- DELETE

  ```sql
  DELETE EMP WHERE NAME = 'Neena';
  ```

  - Neena와 같은 급여 받는 사원 삭제

    ```sql
    DELETE EMP WHERE SALARY = (SELECT SALARY FROM EMP WHERE NAME = 'Neena');
    ```






## 추가사항(TCL, 시퀀스)

- (동일 레코드 다른 창에서 작업시) 명령어 먼저 입력한 창에서 COMMIT 이나 ROLLBACK이 필요

  - 다른 창에선 **LOCK**이 걸린 상태

- **ROLLBACK** ===> **COMMIT**(영구반영)시점으로 복귀(테이블 내 데이터 복구 가능)

  - TANSACTION CONTROLL LANGUAGE = TCL
  - 논리적 1개의 업무이지만 단일 업무 여러개 구성 - 여러개 SQL 결합하여 1개 업무 처리
    - 계좌이체 ( A --> B) 업무 : 출금 + 입금
    - **ALL**   OR   **NOT THING**
    - DML에 특히 필요

  ```sql
  - 계좌 테이블
  CREATE TABLE ACCOUNT(
  CODE NUMBER(5),
  BALANCE NUMBER(8,2)
  );  ===> 자동 COMMIT (DDL)
  INSERT INTO ACCOUNT VALUES(12345, 10000);
  INSERT INTO ACCOUNT VALUES(54321, 5000);
  
  -계좌이체 : 12345 계좌에서 54321 계좌로 이체 5000
  UPDATE ACCOUNT
  SET BALANCE = BALANCE - 5000
  WHERE CODE = 12345;  ===> 12345에서 출금
  UPDATE ACCOUNT
  SET BALANCE = BALANCE + 5000
  WHERE CODE = 54321;
  COMMIT;  ===> 계좌이체 영구 반영
  
  UPDATE ACCOUNT
  SET BALANCE = BALANCE -1000
  WHERE CODE = 12345;
  UPDATE ACCOUNT
  SET BALANCE = BALANCE + '1000
  WHERE CODE = 54321;
  ROLLBACK;  ===> COMMIT 시점으로 복구 (계좌이체 실패)
  ```

- 자동으로 증가하는 시퀀스(DB마다 방법 다르다)
  - INSERT 레코드 저장할 때 숫자 1증가  ---> 100번, 101번...
  - 몇부터 시작 몇씩 증가 몇까지 종료  ===> 변경 가능
  - ORACLE 자동 증가 숫자값 생성 = SEQUENCE
    1.  정의
       - 테이블 정의 / 시퀀스 정의 / 사용자 정의 ---> CREATE 사용
       
       - CREATE SEQUENCE 시퀀스명 ;  ---> 1부터 시작 1씩 증가, 최댓값
       
       - START WITH  시작값
       
       - INCREMENT BY 증가치
       
       - MAXVALUE 종료값
       
         ```sql
         CREATE SEQUENCE EMP_ID_SEQ
         START WITH 300
         INCREMENT BY 1
         MAXVALUE 999;
         
         SELECT EMP_ID_SEQ.NEXTVAL FROM DUAL;  ---> 300
         SELECT EMP_ID_SEQ.NEXTVAL FROM DUAL;  ---> 301
         SELECT EMP_ID_SEQ.NEXTVAL FROM DUAL;  ---> 302
         
         SELECT EMP_ID_SEQ.CURRVAL FROM DUAL;  ---> 302
         ```
       
    2. 레코드 저장할 때 활용  ---> 지나간 번호는 지나가면 끝! (용도에 맞게 사용)

       ```sql
       INSERT INTO EMP VALUES(EMP_ID_SEQ.NEXTVAL, '서부장', '고참부장', 20, 1000000, '05/01/01');
       INSERT INTO EMP VALUES(EMP_ID_SEQ.NEXTVAL, '박부장', '고참부장', 20, 1000000, '05/01/01');
       INSERT INTO EMP VALUES(EMP_ID_SEQ.NEXTVAL, '김부장', '고참부장', 20, 1000000, '05/01/01');
       SELECT EMP_ID_SEQ.NEXTVAL FROM DUAL;  ---> 번호 한개 넘어가게 됨
       INSERT INTO EMP VALUES(EMP_ID_SEQ.NEXTVAL, '최부장', '고참부장', 20, 1000000, '05/01/01');
       ```

    3.  시퀀스 없이 유사 방법

       ```sql
       EMP 테이블 지금까지 저장 ID 최댓값 +1
       SELECT MAX(ID) + 1 FROM EMP
       INSERT INTO EMP VALUES((SELECT MAX(ID) + 1 FROM EMP), '최부장', '고참부장', 20, 1000000, '05/01/01');
       INSERT INTO EMP VALUES((SELECT MAX(ID) + 1 FROM EMP), '이부장', '고참부장', 20, 1000000, '05/01/01');
       INSERT INTO EMP VALUES((SELECT MAX(ID) + 1 FROM EMP), '이부장', '고참부장', 20, 1000000, '05/01/01');
       ```

  - MERGE : 1개 SQL(저장 또는 수정 모두 가능)  ---> 모든 DB에서 존재X

- GRANT 권한명  TO 계정
- REVOKE 권한명 FROM 계정





## 제약 조건



1.  데이터 저장 / 수정 / 삭제 DML 사용시 데이터 상태 모순 방지

2.  데이터 제약 조건 = INTEGRITY CON

3.  제약조건 종류

   | 종류        | 내용                                                   |
   | ----------- | ------------------------------------------------------ |
   | NOT NULL    | 컬럼값 비어있으면 안된다 조건 지정                     |
   | UNIQUE      | 컬럼값 중복되면 안된다 조건 지정 / NULL값도 1개만 허용 |
   | PRIMARY KEY | NOT NULL + UNIQUE 조건 지정 (레코드 식별자)            |
   | CHECK       | 사용자 정의 조건 지정                                  |
   | FOREIGN KEY | 다른 테이블의 컬럼에 포함 값들만 사용 조건 지정        |

4.  제약조건 문법

   - CREATE TABLR 테이블명( 컬럼명1 타입(길이) ??? ...)

   | 종류        | 문법                                                   |
   | ----------- | ------------------------------------------------------ |
   | NOT NULL    | ID NUMBER(5) CONSTRAINT EMP_ID_NN NOT NULL             |
   | UNIQUE      | CONSTRAINT EMP_ID_UK UNIQUE                            |
   | PRIMARY KEY | CONSTRAINT EMP_ID_PK PRIMARY KEY                       |
   | CHECK       | CONSTRAINT EMP_ID_CK(사용자 지정)  ---> (ID >= 1000)   |
   | FOREIGN KEY | CONSTRAINT EMP_ID_FK  REFERENCES 참조테이블명(DEPT_ID) |

- 1) CREATE TABLE 테이블명 (컬렁명1 타입(길이) ???,,,)

- 2.  CREATE TABLE 테이블명 (컬럼명1 타입(길이), ...,

     CONSTRAINT EMP_ID_PK PRIMARY KEY(컬럼명1) ,

     )

- 3.  ALTER TABLE ADD 컬럼 1개 추가

     ALTER TABLE ADD CONSTRAINT ....

  | C_EMP 테이블                           | C_DEPT 테이블                           |
  | -------------------------------------- | --------------------------------------- |
  | EMP_ID 5자리정수 중복X, NULL X         | DEPT_ID 5자리 정수, 중복X, NULL X       |
  | NAME 30자리 문자열, NULL X             | DEPT_NAME 30자리 문자열, NULL X, '부서' |
  | SALARY 소수점이하 2(전체 10), 1000이상 | CITY 20자리 문자열                      |
  | INDATE 날짜                            |                                         |
  | TITLE 30자리 문자열,                   |                                         |
  | DEPT_ID 5자리 숫자,                    |                                         |

  ```sql
  CREATE TABLE C_DEPT
  (DEPT_ID NUMBER(5) CONSTRAINT C_DEPT_ID_PK PRIMARY KEY,
   DEPT_NAME VARCHAR2(30) CONSTRAINT C_DEPT_NAME_CK CHECK (DEPT_NAME LIKE '%부서'),
   CITY VARCHAR2(20)
   );
   
  CREATE TABLE C_EMP(
  EMP_ID NUMBER(5) CONSTRAINT C_EMP_ID_PK PRIMARY KEY,
  NAME VARCHAR2(30) CONSTRAINT C_EMP_NAME_NN NOT NULL,
  SALARY NUMBER(10,2) CONSTRAINT C_EMP_SAL_CK CHECK (SALARY >= 1000),
  INDATE DATE,
  TITLE VARCHAR2(30) CONSTRAINT C_EMP_TITLE_CK CHECK (TITLE IN('사원', '대리', '과장','부장', '임원')),
  DEPT_ID NUMBER(5) CONSTRAINT C_EMP_ID_FK REFERENCES C_DEPT(DEPT_ID)
   );
   
  INSERT INTO C_DEPT VALUES(10, '인사부서', '제주시');
  INSERT INTO C_DEPT VALUES(20, '교육부서', '부산시');
  INSERT INTO C_DEPT VALUES(NULL, '전산부서', '부산시');  ---> NOT NULL
  INSERT INTO C_DEPT VALUES(30, '기획부', '서울시');  ---> CK 위반 '부서'
  
  INSERT INTO C_EMP VALUES(100, '박사원', 2000, SYSDATE, '사원', 10);
  INSERT INTO C_DEPT VALUES(1000, '신생부서', '서울시');
  INSERT INTO C_EMP VALUES(200, '김대리', 5000, SYSDATE, '대리', 1000);
  ```

- 제약조건 지정 조회

  ```sql
  SELECT * FROM USER_CONSTRAINTS; 
  DESC USER_CONSTRAINTS;
  
  SELECT CONSTRAINT_NAME, CONSTRAINT_TYPE, SEARCH_CONDITION
  FROM USER_CONSTRAINTS
  WHERE TABLE_NAME = 'C_DEPT';  ---> 테이블명 대문자
  ```

- UPDATE, DELETE 명령 시에도 제약조건의 효력은 발생

  - UPDATE로 수정시, 제약조건에 맞게 수정
  - DELETE시, 대표적으로 참조되는 테이블은 참조하는 테아블을 먼저 삭제해야 삭제가능
  - 부모 테이블은 자식 테이블보다 먼저 정의된다





