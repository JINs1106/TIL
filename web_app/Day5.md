# Day 5



---

## Review

- jsp는 서블릿보다 간결 응답
- jsp 기본
  - <% 형태의 태그  ---> 자바 문장 그대로

- 내장객체 : 서블릿 api  그대로 사용
  - request - 요청(forward, include 파일까지 공유)
  - response, out - 응답
  - exception - 예외(<% page isErrorPage="true" ...)
  - session - 세션(=브라우저 내부 공유)
  - application - 다른 브라우저 공유(서버종료시 종료)
- 액션태그 : <jsp:xxx
  - <jsp: include page= "(컨택스트 루트)/a.jsp" 컨택스트의 a.jsp
  - <jsp: forward page= "a.jsp" 현재 파일과 같은 경로
  - <jsp:useBean id=" " class= "패키지명.클래스명"
    - scope 속성 : request  /  session  /  application
  - <jsp:setProperty property= "name" name=" vo" (value="java" or param="id")
    - property와 파라미터 명이 같다면 생략 가능0
  - <jsp:getProperty property=" " name=" "  // 알아서 출력까지 진행



---



## JSP



### EL  /  JSTL

- 표현언어  /  Jsp Standard Tag Library(라이브러리 파일 추가 설치 후 사용 태그)

- 자바 웹서버 프로그램  ---> 서블릿만 존재 
- 자바 구현 가능 / 응답 HTML 태그 불편  ===> HTML + <%  자바문장 형태  %>
- JSP 파일 = 웹개발자 + 웹디자이너 "자바문장 최소화 정책"



#### EL

- Expression Language - 브라우저 응답 내용 쉽고 간결 표현 가능 언어 (jsp 파일 내부 사용)

- <% request.getParameter("id"); %>  ===> ${param.id}

- ${ el 언어 문법 }

  - 타입  /  논리값  /  정수  /  실수  /  문자열 ' ', " "  /  null  /  (대소문자구분필요)

- 내장객체

  - jsp 내장객체 / el 내장객체  ---> 파라미터
  - ${ param.id }  ==  request.getParameter("id");
  - ${ paramValues.hobby[0] } ==  request.getParameterValues("hobby");

  | jsp 내장객체 | el 내장객체               |
  | ------------ | ------------------------- |
  | x            | param.파라미터명          |
  | x            | paramValues.파라미터명[i] |
  | pageContext  | pageScope                 |
  | request      | requestScope              |
  | session      | sessionScope              |
  | application  | applicationScope          |

  - 빈 = jsp bean = jsp 사용 자바 객체





## Spring Framework

> eclipse  ---> jsp  /  servlet  /  jdbc  실행
>
> sts  --->
>
> spring.io  ===> tool4

































