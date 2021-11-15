# Day 1

> **자바 프로그램**범용
>
> 
>
> **데이터베이스** : 의미 있는 데이터 모아서 저장 조회 관련 시스템
>
> ```
> 학생 ( 학번 - 정0수 5자리. 중복X, NOT NULL
>       이름 -
>       전공 -
>       등등 - ...
> )
> ```
>
> - 영구적(전원 off - on) 데이터 저장, 조회 관련
> - 여러 어플리케이션 공유
> - 데이터베이스 형태 : 네트워크 구조 / 계층형 구조 / **관계형 구조**
>   - 의미있는 데이터를 행과 열의  테이블 구조 표현
>   - RDBMS - Relational Database Manage System
> - 관계형 베이스 구현 제품
>   - ORACLE, MYSQL, DB2 ...
> - 오라클 관계형 DB 저장, 조회 관리 문법 제공 언어 ==> **SQL**(관계형 데이터베이스 언어)



## ORACLE 설치(11G XE)

> 설치 후 run sql command line  // tool : sql developer, orange, toad
>
> eclipse sql 내장 -> 설정 필요

- 관리자 계정 system 암호 system

- run - connect system/system;

- hr 계정 오라클 설치시 포함 -> 잠금해제 필요

- 수업 샘플 데이터

- alter user hr identified by hr(암호) account unlock;

- connect hr/hr; -> hr계정으로 연결

- select * from tab; -> 데이터 목록 출력

- select tname from tab; -> 데이터 테이블 목록

- SYSTEM / hr 2개 계정 존재

- 테이블 정의  / 데이터 저장 계정 생성 필요( + 권한부여) --> user

  ```sql
  create user test(사용자) identified by test(암호); // DDL사용
  grant resource, connect to test(사용자); //grant로 권한부여
  show user; // 현재 사용자 확인
  ```

  



## SQL 문법

- 대소문자 구분 X ( 계정의 암호는 구분 )
- 오라클 문자열 데이터값 --> '문자열값'
- 클래스 생성 X, main X
- sql 문법 문장 1개 ==> 실행
- EDIT; ---> 직전 명령 편집.저장.닫기  ==> /\n

- SQL 종류

  | DQL : select ~                                         | 조회                                     |
  | ------------------------------------------------------ | ---------------------------------------- |
  | **DDL :** create / alter / drop table                  | 테이블 구조 정의 / 변경 / 삭제           |
  | **DML :** insert / update / delete                     | 테이블 내 데이터 저장 / 수정 / 삭제      |
  | **TCL :** commit / rollback                            | 연속 SQL 실행 완료, 취소 / 트랜젝션 처리 |
  | **DCL :** grant / revoke ==> *DBA만 사용(system 계정)* | 계정 특정 권한 부여 / 취소               |



### DQL(조회) : **select** ~

> 학생데이터 = (학번 이름 전공 학년) * n
>
> - 학생테이블
>
> | 학번 컬럼(열)    | 이름 컬럼 | 전공 컬럼 | 학년 컬럼 |
> | ---------------- | --------- | --------- | --------- |
> | 레코드(행) : 100 | 김학생    | it        | 4         |
> | ...              | ...       | ...       | ...       |

 - select 컬럼명
   - *(목록전부),  TNAME(테이블 이름)
   - DESC[RIBE] TABLE : 테이블 구조
   - SELECT FIRST_NAME FROM EMPLOYEES;  (+  SET PAGASIZE 50; 자료구분 사이즈 설정)
   - 실제 컬럼명을 조회 임시변경 : **ALIAS(AS)** 생략가능
   - 직종코드 1개 조회 중복 제거 : **DISTINCT**
   - 함수 사용 : UPPER()
   
- from 테이블명

- [where] : 레코드 조건식   --> 만족하는 자료만 도출

   - 이름 급여(10000이상) 조회 : WHERE SALARY >= 10000;

   - WHERE 컬럼명 연산자 값;

   - 숫자 = 대소비교, 문자 = 사전 나열 순서(앞 작다, 뒤 크다)

   - 암호나 데이터 문자값 대소문자 구분!!!!

   - COMMISSION_PCT 컬럼 --> 실수 ==> 0.14 (<= 1)  OR **NULL**( RUN SQL 커맨드출력 : 공백)

     - 다른 커맨드에서는 공백이 아닐 수 있다!!

     | 비교연산자     | >, >=, <, <=, =, !=(<>)                                      |
     | -------------- | ------------------------------------------------------------ |
     | 산술연산자     | +, -, *, /  --> 나머지는 함수로                              |
     | 논리연산자     | SALARY >= 10000 **AND** EMPLOYEE_ID = 100, **OR,** **NOT**   |
     | 범위연산자     | **BETWEEN** A **AND** B                                      |
     | 목록           | **IN** ( A, B, D, C);  --> 만족시 도출                       |
     | 유사패턴연산자 | **LIKE** '_a%' --> 두번째 자리가 a인 문자값 / 대소문자 구분!! |
     | NULL비교연산자 | IS NULL / IS NOT NULL                                        |

 - [group by]

 - [having]

 - [order by] : 정렬 순서  ==> SELECT - WHERE - ORDER 순으로 실행

   - ORDER BY FIRST_NAME ASC; (오름차순 조회)

   - ORDER BY FIRST_NAME DESC; (내림차순 조회) 

   - 2개 조건 

     ```
     SELECT FIRST_NAME 이름, SALARY 급여 FROM EMPLOYEES
     ORDER BY 2 DESC, 1;
     ORDER BY 급여 DESC, 이름;
     
     SELEC COMMISSION_PCT FROM EMPLOYEES
     ORDER BY COMMISSION_PCT NULLS LAST(FIRST); ---> NULL 값을 마지막(처음) 으로 보여줘
     ```

   - **ROWNUM**(고정) 과 **SAMPLE**(랜덤)

     ```
     SELECT EMPLOYEE_ID FROM SAMPLE(5); ---> 5개 랜덤 추출
     
     SELECT EMPLOYEE_ID FROM EMPLOYEES
     WHERE ROWNUM <= 5;  ---> 조회 순서대로 5개 추출
     ```


 ```sql
 SELECT SYSDATE FROM DUAL; --> 오라클 현재시각 함수 '21/08/12'날짜형식(RR/MM/DD)
 SELECT TO_CHAR(SYSDATE, 'YYYY-MM-DD HH24:MI:SS') FROM DUAL;
 
 DESC EMPLOYEES;
 SELECT SALARY*12 AS 연봉 FROM EMPLOYEES; --> 연산식으로 조회 가능 / (AS) 명령어 사용
 SELECT DISTINCT JOB_ID FROM EMPLOYEES;
  
 SELECT UPPER(FIRST_NAME) FROM EMPLOYEES; --> 함수 UPPER로 대문자변경
  
 SQL> SELECT FIRST_NAME, SALARY FROM EMPLOYEES
   2  WHERE SALARY >= 10000 AND SALARY <= 15000; -->  효율적인 방식 선택
   2  WHERE SALARY BETWEEN 10000 AND 15000;
   3  WHERE EMPLOYEE_ID IN (100, 101, 111, 200, 350);
 
 SQL> SELECT HIRE_DATE FROM EMPLOYEES  --> 날짜도 대소 비교가 가능하다
   2  WHERE HIRE_DATE >= '02/01/01'
   3  AND HIRE_DATE <= '02/12/31';
   
 SQL> SELECT FIRST_NAME FROM EMPLOYEES  --> 대소문자 구분 / % = 어떤 문자가 와도 상관 X
   2  WHERE FIRST_NAME LIKE '%Jo%';
   
 SQL> SELECT COMMISSION_PCT FROM EMPLOYEES
   2  WHERE COMMISSION_PCT IS NOT NULL;  --> 커미션 받는 사원 조회 / NULL값이 아닌 사람
   
 SELECT ROWNUM, SALARY FROM EMPLOYEES
 WHERE ROWNUM <= 5
 ORDER BY SALARY DESC;
 
 SELECT ROWNUM, SALARY
 FROM EMPLOYEES
 ORDER BY SALARY DESC;
 1. FROM 절 테이블 가져온다
 2. SELECT 절 실행하면 SALARY 칼럼 가져올때마다 ROWNUM 생성 -> ROWNUM이 먼저 붙게 된다
 3. 급여 많은 사원부터 2번 결과의 순서 변경
 ====> SUBQUERY 이용하면 해결 가능
 ```

| 집계함수     | 급여총합 --> 1개의 레코드 도출       |
| ------------ | ------------------------------------ |
| = 다중행함수 | SELECT SALARY FROM EMPLOYEES;        |
| 단일행함수   | SELECT UPPER(FIRST_NAME)             |
|              | FROM EMPLOYEES --> 107개 레코드 바뀜 |

- 함수명(매개변수...) : SUM, MAX, MIN, AVG, COUNT

  - SUM, AVG : 숫자타입 컬럼만 적용가능
    - 집계함수 SELECT 시는 다른 컬럼 같이 조회 불가능
    - 단, GROUP BY 뒤 나열 컬럼명은 같이 조회 가능

  - MAX, MIN : 모든 타입 컬럼 가능
  - COUNT : 모든 타입 컬럼의 NOT NULL 데이터 갯수만 계산
    - COUNT(*) : NULL 값을 포함한 갯수

```sql
SELECT SALARY FROM EMPLOYEES;
SELECT SUM(SALARY) FROM EMPLOYEES; ---> 총합
SELECT AVG(SALARY) FROM EMPLOYEES; ---> 평균
SELECT MAX(SALARY), MIN(SALARY) FROM EMPLOYEES;  --> 최대 급여, 최소 급여
SELECT COUNT(SALARY) FROM EMPLOYEES; ---> 급여받는 사원 수
SELECT COUNT(DEPARTMENT_ID) FROM EMPLOYEES; ---> 부서에 속한 사원 수

SELECT SUM(SALARY) FROM EMPLOYEES
WHERE DEPARTMENT_ID = 10;

 [ 부서별 급여 총합 조회 ] 
  SELECT DEPARTMENT_ID, SUM(SALARY) FROM EMPLOYEES  // + 이름 출력 FIRST_NAME
  WHERE DEPARTMENT_ID IS NOT NULL ==>  (부서원 없는 = NULL 값 제외하자)
  GROUP BY DEPARTMENT_ID
  ORDER BY SUM(SALARY) DESC;  --> 총합 많은 부서 순
  + (부서별 총합이 10000이상만 조회)
  WHERE SUM(SALARY) >= 100000   ===> GROUP BY 위에 위치하면 작동 X
                                     GROUP BY 아래 WHERE 대신 HAVING 사용

 [ 가장 먼저 입사 사원 입사일자, 최근 입사 사원 입사일자 ]
  SELECT MIN(HIRE_DATE), MAX(HIRE_DATE) FROM EMPLOYEES;
  SELECT MIN(HIRE_DATE) 사장님의입사일, MAX(HIRE_DATE) 신입사원의 입사일 FROM EMPLOYEES;
  ===> 별칭 붙이기 가능
  
 [ 이름 알파벳 순서상 가장 처음, 마지막 이름 ]
  SELECT MIN(FIRST_NAME) 처음, MAX(LAST_NAME) 마지막 FROM EMPLOYEES;
  
```

- 마무리

  SELECT 컬럼명 FROM 테이블명

  [ WHERE 조회 데이터 조건식 ]

  [ GROUP BY 집계함수 적용 기준 컬럼 ]

  [ HAVING 집계함수 조건식 ]

  [ ORDER BY 정렬순서 컬럼명 ASD/DESC NULLS FIRST/LAST ]

  (실행순서)

  - FROM  -->  WHERE   --> GROUP BY   -->  HAVING  -->  SELECT  -->  ORDER BY



### 집계함수 / 단일행 함수

| 집계함수   | SUM, AVG, MAX, MIN | COUNT                                 |
| ---------- | ------------------ | ------------------------------------- |
| 단일행함수 | 문자열함수         | LENGTH, LENTHB(바이트수), UPPER/LOWER |
|            | 숫자함수           |                                       |
|            | 날짜함수           |                                       |
|            | 타입변환함수       |                                       |
|            | NULL처리 함수      |                                       |

#### 문자열함수
- **ASCII('A')**

  - SELECT 컬럼명, 함수명 FROM 테이블명 --> SELECT ASCII('A') FROM DUAL;

  - DUAL : 가상 테이블로 SELECT 결과 저장 임시 테이블

  - SELECT **ASCIISTR('가')** FROM DUAL;  --> 16진수

- **CONCAT** 연산자  OR  **||** 문자열 결합 -----> XXX 사원은 급여 XXX를 받습니다.

  - (자바) 이름변수 +ㅡ "사원은 급여 " + 급여변수 + "를 받습니다."

  - (오라클) SELECT FIRST_NAME || ' 사원은 급여 ' || SALARY|| '를 받습니다.' FROM EMPLOYEES;

    --> AS 급여정보 // 별칭으로 축약

  - SELECT CONCAT( CONCAT( CONCAT(FIRST_NAME, '사원은 급여') , SALARY), '를 받습니다,');

- **INSTR** : 특정 문자열 찾은 위치 리턴

  - SELECT FIRST_NAME FROM EMPLOYEES

    WHERE INSTR(FIRST_NAME, 'ex') >= 1;  ==> 이름에 ex 포함된 인덱스 -1

- **LOWER / UPPER / INITCAP** : 대소문자 변경

  - SELECT FIRST_NAME FROM EMPLOYEES
    - WHERE FIRST_NAME = INITCAP('neena'); ---> 첫문자만 대문자로 변경
    - WHERE LOWER(FIRST_NAME) = LOWER('neena'); ---> 전부 소문자로 변경 (UPPER 는 대문자)

- **INSTR, SUBSTR**

  - INSTR('Neena', 'na') --> 문자 입력 위치 도출
  - SUBSTR('Neena', 1, 2) ---> 위치 입력 문자 도출
  - WHERE HIRE_DATE >= '02/01/01' AND HIRE_DATE '02/12/31';
  - WHERE HIRE_DATE LIKE '02%';
  - WHERE SUBSTR(HIRE_DATE, 1, 2) = '02';
  - WHERE INSTR(HIRE_DATE, '02') = 1;

- **TRIM, PAD** --> LENGTH로 결과 확인 (공백제거)

  - LPAD, LTRIM - 왼쪽 ? 추가, 왼쪽 공백 제거
  - RPAD, RTRIM - 오른쪽
  - SELECT LENGTH(TRIM('     JAVA')) FROM DUAL;
  - SELECT LPAD('JAVAPROGRAM', 20, '-');



---

## ORACLE의 데이터 형식

> 숫자 / 날짜 / 문자 / 이진수 - 대용량 동영상 이미지 음향

| 숫자          | NUMBER(38)                                                   |
| ------------- | ------------------------------------------------------------ |
|               | 정수 NUMBER(5, 0), 실수 NUMBER(10, 2)                        |
| **날짜**      | **DATE** 년 월 일 시 분 초   // 0~49 : 2000년대 //50~99 : 1900년대 |
| '내부에 작성' | 기본적 타입 형식 -> RR/MM/DD (변경가능)                      |
| **문자**      | **VARCHA2** -> 최대 / 동적으로 크기 조정가능 최대 4000BYTE   |
| 내주에 작성'  | CHAR(10) -> 고정 데이터 타입으로 낭비 가능성                 |

