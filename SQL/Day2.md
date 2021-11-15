

# Day 2



---

## Review

> SQL - RDB 언어

1.  대소문자 구분 x
2.  문법 맞는 문장 실행
3. db설치 컴퓨터 - db 설치 컴퓨터 네트워크

| DQL     | select              | 조회                                |
| ------- | ------------------- | ----------------------------------- |
| **DDL** | create, alter, drop | 테이블 정의 수정 삭제               |
| **DML** | insert              | 테이블 내 데이터 저장 / 수정 / 삭제 |
| **DCL** | grant / revoke      | DB 사용권한 부여 회수               |
| **TCL** | commit              | 트랜젝션 처리                       |

- SELECT 문법

  | SELECT    | 필수 / 컬럼명 : *, 연산식, 별칭(AS), DISTINCT, \|\|, 함수 |
  | --------- | --------------------------------------------------------- |
  | FROM      | 필수 / 테이블명                                           |
  | WHERE     | 생략가능 /  조회 레코드 조건, 레코드 수 줄어듬            |
  | GROUP  BY | 생략가능 / 집계함수 적용 그룹 컬럼명                      |
  | HAVING    | 생략가능 / 집계함수 조건식                                |
  | ODER BY   | 생략가능 / 정렬 순서 컬럼명(INDEX, 별칭) DESC, ASC        |

- 연산자

  | 산술연산자      | =  -  /  *            |
  | --------------- | --------------------- |
  | 비교연산자      | >  <  >=  <=  !=  =   |
  | 조건결합 연산자 | AND  OR  NOT          |
  | NULL 처리연산자 | IS NULL,  IS NOT NULL |
  | 목록연산자      | IN(A,B,C,..)          |
  | 범위 연산자     | BETWEEN A AND B       |
  | 유사패턴비교    | LIKE '_A%'            |

- 함수

  | 집계함수     | COUNT(칼럼, *)                                   |
  | ------------ | ------------------------------------------------ |
  | 문자형함수   | LENGTH(B),  INSTR,  SUBSTR                       |
  |              | UPPER.  LOWER,  INITCAP                          |
  |              | TRIM,  PAD                                       |
  | 숫자형함수   | ABS 삼각함수,  ROUND(반올림),  TRUNC(버림),  MOD |
  | 날짜형함수   |                                                  |
  | NULL처리함수 |                                                  |
  | 순위함수     | X                                                |

- 데이터 타입

  | 날짜 | RR-MM-DD                |
  | ---- | ----------------------- |
  | 문자 | VARCHAR2(100)           |
  | 숫자 | NUMBER(5), NUMBER(5, 2) |



---



## 함수

> 분석 순위 함수 x

### 숫자함수

> ```sql
> SELECT LENGTH('JAVA') FROM DUAL; --> 4(1행 함수 결과 가상 테이블 제공)
> 
> SELECT LENGTH(FIRST_NAME) FROM EMPLOYEES;  --> 107행
> 
> SELECT 34.5678, TRUNC(34.5678), ROUND(34.5678) FROM DUAL;  --> 34.5678  34  35
> 
> SELECT 34.4678, TRUNC(34.4678), ROUND(34.4678) FROM DUAL;  --> 34.4678  34  34
> 
> SELECT 34.4678, TRUNC(34.4678, 1), ROUND(34.4678, 1) FROM DUAL;
> --> 34.4678  34.4  34.5
> SELECT 34.4678, TRUNC(34.4678, -1), ROUND(34.4678, -1) FROM DUAL;
> --> 34.4678  30  30
> ```

- TRUNC(숫자, X) /  ROUND(숫자, X)

  - X - 0  버림 / 반올림한 후, 정수 1자리까지 표현

  - X - 양수  버림 / 반올림한 후, 소수점 자리까지 표현

  - X - 음수  버림 / 반올림한 후, 정수 자리까지 표현

  - 급여평균 

    ```sql
    SELECT ROUND(AVG(SALARY)) FROM EMPLOYEES;  --> 반올림하여 정수 자리까지 표현
    ```

- MOD

  ```sql
  SELECT TRUNC(10 / 3) 정수몫, MOD(10, 3) 나머지 FROM DUAL;
  ```

  - 사번 칼럼 ID 짝수인 사원의 사번, 이름 조회

    ```SQL
    SELECT EMPLOYEE_ID 사번, FIRST_NAME 이름 FROM EMPLOYEES
    WHERE MOD(EMPLOYEE_ID, 2) = 0
    ORDER BY EMPLOYEE_ID ASC;
    ```



### 날짜함수

- 날짜 연산

  - +,  -  연산 가능 (날짜 + 숫자(1일))  ==> 날짜

  ```sql
  SELECT SYSDATE - 1 어제, SYSDATE 오늘, SYSDATE + 1 내일 FROM DUAL;
  ```

  - 오늘 날짜와 입사일 사이 경과  일수, 년수 조회  ==> 숫자가 리턴(일단위)

  ```sql
  SELECT SYSDATE - HIRE_DATE FROM EMPLOYEES;  --> 경과 일 수
  SELECT (SYSDATE - HIRE_DATE) / 365 FROM EMPLOYEES;  --> 경과 년 수
  SELECT TRUNC((SYSDATE - HIRE_DATE) / 365) FROM EMPLOYEES;
  ```

- **SYSDATE** : 현재시각 표현 함수 RR/MM./DD

- 경과 개월수 : **MONTHS_BETWEEN(SYSDATE, HIRE_DATE)**

  ```sql
  SELECT MONTHS_BETWEEN(SYSDATE, HIRE_DATE) FROM EMPLOYEES;
  ```

- **ADD_MONTH(날짜, 개월숫자)**

  ```sql
  SELECT ADD_MONTHS(SYSDATE, 3) "3개월 후" FROM DUAL;
  ```



### 형 변환 함수

- NULL 변환 함수 : **NVL**(컬럼명, NULL값을 대체하는 값)  ===> 해당하는 컬럼의 타입을 고려

  - COMMISSION_PCT 못 받는 사원  ==> 공백으로 표현

  - 모든사원 커미션 포함 조회하되 NULL 사원은 0이라고 표현

    ```SQL
    SELECT NVL(COMMISSION_PCT, 0) FROM EMPLOYEES;
    ```

  - 사원이름 과 부서이름 - NULL값은 배치이전으로 조회

    ```SQL
    SELECT FIRST_NAME, NVL(DEPARTMENT_ID, '배치이전') FROM EMPLOYEES;  ==> 동작X(칼럼타입)
    ```

    ==> TO_함수 사용

- **TO_CHAR**(날짜와 숫자를 **문자로**)  /  **TO_NUMBER**(문자를 **숫자**로)  /  **TO_DATE**(문자를 **날짜**로)

  - 숫자가 날짜로 바꿔지는 방법 x  ==> 문자가 중요

  ```SQL
  SELECT FIRST_NAME, NVL(TO_CHAR(DEPARTMENT_ID),'배치이전') FROM EMPLOYEES;
  SELECT TO_CHAR(1000, '$9,999') FROM DUAL;
  SELECT TO_NUMBER('$1,000', '$9,999') + 2000 FROM DUAL;
  SELECT SYSDATE, TO_CHAR(SYSDATE, 'YYYY-MM-DD DAY HH24:MI:SS') FROM DUAL;
  ```

  - ,  /  YY(연도)  /  MI(분)  / DAY(요일)  / HH, HH24(시간)  /  L(로컬통화) 둥등

  ```sql
  SELECT HIRE_DATE FROM EMPLOYEES
  WHERE TO_CHAR(HIRE_DATE, 'MM') = '02';
  ```

  

### 조인

> 2개 이상의 테이블이 서로 관계되어 있는 상태

- INNER JOIN(내부 조인)
  - 오라클 독자 문법
  
    ```sql
    SELECT FIRST_NAME, e.DEPARTMENT_ID, DEPARTMENT_NAME
    FROM DEPARTMENTS d, EMPLOYEES e
    where d.DEPARTMENT_ID = e.DEPARTMENT_ID;
    ```
  
  - ANSI JOIN(DB 표준 문법)
  
    ```sql
    SELECT FIRST_NAME, e.DEPARTMENT_ID, DEPARTMENT_NAME
    FROM DEPARTMENTS d INNER JOIN EMPLOYEES e
    ON d.DEPARTMENT_ID = e.DEPARTMENT_ID;
    ```
  
- OUTER JOIN(외부 조인) : 외부 레코드 조인

  - 사원, 이름 부서 조회 하되 부서코드 NULL인 사원도 포함

    ```sql
    SELECT FIRST_NAME, NVL(e.DEPARTMENT_ID, 0), NVL(DEPARTMENT_NAME, '없음')
    FROM DEPARTMENTS d, EMPLOYEES e
    WHERE d.DEPARTMENT_ID(+) = e.DEPARTMENT_ID;
    ```

  - JOIN 시에 1개 테이블에 존재하는 값이 다른 테이블에 존재하지 않는 경우,

    - JOIN 포함X ===> (+) ===> **OUTER JOIN**

    ```SQL
    SELECT NVL(FIRST_NAME, '부서원없음'), e.DEPARTMENT_ID, DEPARTMENT_NAME
    FROM DEPARTMENTS d, EMPLOYEES e
    WHERE d.DEPARTMENT_ID = e.DEPARTMENT_ID(+);
    ===> 사원, 이름 부서 조회 하되, 사원이름 '부서원없음' 조회 
    ```

  - LEFT / RIGHT OUTER JOIN ON

    

- SELF JOIN : 자기자신 테이블이 두개이상 있다고 정의

  - 모든 사원의 상사 이름 급여 조회(상사 없는 사람 포함)

    ```sql
    SELECT ME.FIRST_NAME, ME.MANAGER_ID, MANAGER.FIRST_NAME, MANAGER.SALARY
    FROM EMPLOYEES ME, EMPLOYEES MANAGER
    WHERE ME.MANAGER_ID = MANAGER.EMPLOYEE_ID(+);
    ```

  - JENNIFER 사원의 상사 이름 급여 조회

    ```sql
    SELECT ME.FIRST_NAME, ME.MANAGER_ID, MANAGER.FIRST_NAME, MANAGER.SALARY
    FROM EMPLOYEES ME, EMPLOYEES MANAGER
    WHERE ME.MANAGER_ID = MANAGER.EMPLOYEE_ID
    AND ME.FIRST_NAME = 'Jennifer';
    ```

  - INNER JOIN ON



### SUBQUERY

> SELECT (SELCET ...) FROM (SELECT...)
>
> WHERE (SELECT...)
>
> 쿼리 내부의 쿼리
>
> EX. Neena와 같은 부서 사람의 급여조회

- 동일비교 
  - 단일행  --> =  IN
  - 다중행  -->  IN  (...)
- 대소비교
  - 단일행  -->   **<  =  >  >=   <=**
  - 다중행  --> ANY(최솟값보다 크다), ALL(서브쿼리 모두보다 크다)

- WHERE 절 포함 (단일행 서브쿼리)

```sql
SELECT FIRST_NAME, SALARY FROM EMPLOYEES
WHERE UPPER(FIRST_NAME) = UPPER('NEENA');  ---> NEENA의 급여조회

SELECT DEPARTMENT_ID FROM EMPLOYEES
WHERE FIRST_NAME = 'Neena';   ---> Neena의 부서 코드
== 같은 부서 급여 조회 ==
SELECT DEPARTMENT_ID, FIRST_NAME, SALARY FROM EMPLOYEES
WHERE DEPARTMENT_ID = (SELECT DEPARTMENT_ID FROM EMPLOYEES WHERE FIRST_NAME = 'Neena');
```

- SELECT 절 포함

```sql
SELECT SALARY, (SELECT SUM(SALARY) FROM EMPLOYEES)
FROM EMPLOYEES;
```

- WHERE 절 포함 (다중행 서브쿼리)

```sql
SELECT DEPARTMENT_ID, FIRST_NAME, SALARY FROM EMPLOYEES
WHERE DEPARTMENT_ID IN (SELECT DEPARTMENT_ID FROM EMPLOYEES 
                        WHERE FIRST_NAME = 'Jennifer');
                      (10, 50)
```

- Neena의 급여보다 더 많은 급여 받는 사원의 급여와 이름 조회

  ```sql
  SELECT SALARY FROM EMPLOYEES WHERE FIRST_NAME = 'Neena';
  
  SELECT FIRST_NAME, SALARY FROM EMPLOYEES
  WHERE SALARY >= (SELECT SALARY FROM EMPLOYEES WHERE FIRST_NAME = 'Neena');
  ```

- Jennifer의 급여보다 더 많은 급여 받는 사원의 급여와 이름 조회

  ```SQL
  SELECT FIRST_NAME, SALARY FROM EMPLOYEES
  WHERE SALARY > ANY (SELECT SALARY FROM EMPLOYEES WHERE FIRST_NAME = 'Jennifer');
  
  SELECT FIRST_NAME, SALARY FROM EMPLOYEES
  WHERE SALARY > ALL (SELECT SALARY FROM EMPLOYEES WHERE FIRST_NAME = 'Jennifer');
  ```

  







