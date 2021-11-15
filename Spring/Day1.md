# Day 1



---

## Review

- 자바 문장  ---> 서블릿 api + 자바 api 사용

- 응답 출력 간결하고 쉽게  ===> 웹디자이너와 공유

- 자바 문장 대신 수행 태그들

- <jsp: xxx

- jstl : 액션태그 없는 기능들 추가 라이브러리 

  - web-inf\lib\jstl=xxx.jar 에 파일 위치 필요
  - 추가사항 : jsp 파일 내부 <%@ tag lib prefix="c" uri="jst문법 url / http://java.sun.com/jsp/jstl/core />"

  - <c:set  /  out  /  remove  /  **if**  /  **choose**  /  **forEach**

    - if : < c:if test="$(10>20)"  /  반드시 el태그 아니여도 된다.  /  />  or < /c:if >

    - choose : < c:choose > <c:when test="${ 10>20 }"> 조건 만족시 수행 < /when > < /otherwise >

    - forEach : <c:forEach begin="1" end="20" step="2" />

      배열 리스트 사용 ---> items="배열 리스트 맵" var="1개 데이터 변수명"

      ${ vo.xxxx } /  vo.key, vo.value  /  varStatus="vo" ---> vo.index, vo.first, vo.current



---



## Spring Framework

> 프레임워크 = 일정 규격 맟주어 프로그래밍 진행 / 강제화
>
> 뼈대 설계 + 몸통(사용자) 구현

- Spring - 자바 구현 대표적 프레임워크 툴. ioc, di, aop, mvc 다른 프레임워크 연동

  - IOC - Inversion Of Controll  /  특정 타입으로 제한(인터페이스 사용)

    ---> 제어의 역전. 원하는 객체 생성하고자 한다면 new XXX()  ===> 수정의 편의 위해 제어권 메인x

  - DI - Dependency Injection  /  IOC 개념 구현 방법

    ---> main 전달받아 사용  ===> 생성된 객체만 주입 받아 실행



### 환경설정

1. sts4 툴 새로 설치 - sqring3 추가, web, server 기능 사용 추가

2. spring.io  ---> spring3 툴 다운도 가능

3. eclipse 툴 내부 설치 가능

   

### Spring project

> java project  /  dynamic web project  /  spring project  /  spring boot project



#### 의존성 주입

- DAO와 VO 이용하기  ---> java  application  servlet  jsp  spring

  - 프레임워크 반 + XML + 나머지 반 구현

  - 경량의 컨테이너(필요한 라이브러리가 적음)

    ---> servlet, jsp ===> tomcat, jdk

    ---> java app ===> jdk

  - 독립적 실행가능

  - pojo 클래스 사용  ---> plain old java object

  - ioc / di

#### SERVICE 추가하기

- dao 메소드 1개 단위 - sql 1개 실행단위  [구체적]
- 기능 = 서비스 1개 단위 [추상적]  ===> 인터페이스로 구현
- <bean <property <constructor-arg

- @WebServlet("/a")  ---> annotation  ---> 클래스 선언부

  - 자바 실행 환경으로 알려주는 설명(jdk, tomcat, spring)

  - spring annotation

    | ioc di xml 방식                        | annotation 방식                          |
    | -------------------------------------- | ---------------------------------------- |
    | <bean id="a" class="ss.A"              | @Component("a")  ---> class A { }        |
    | <bean id="a" class="ss.xxxServiceImpl" | @Service("a")  ---> class xxxServiceImpl |
    | <bean id="a" class="ss.ADAO"           | @Repository("a")  ---> class ADAO { }    |
    |                                        | @Autowired                               |
    |                                        | @Qulifier                                |

- 기능

  | di ioc                           | 필수                          |
  | -------------------------------- | ----------------------------- |
  | aop(aspect oriented programming) | x                             |
  | mvc                              | 가장 많이 활용 (spring + web) |
  | spring jdbc                      | x                             |
  | mybatis                          | o                             |
  | spring - mybatis 연동            | 필수                          |
  | annotation                       | 일부 학습 + ....              |
  | sts 스프링 - sts 설치 설정파일   |                               |
  | spring web 고급기술              | ajax  /  json  /  rest        |
  |                                  | spring boot                   |

  

































