# Day 3



---

## Review

- 웹클라이언트  ---> html,  css,  jquery
- 웹서버  ---> tomcat + jdk,  servlet,  jsp,  spring



### Servlet

- 작성(4.0 기준 / tomcat 9 + jdk 8)

  ```java
  @WebServlet("/a")   ===> web.xml 파일 대신 설정
  or  <servlet> 
      <servlet-name> (임심)서블릿이름
      <servlet-class> 패키지명.서블릿실제클래스명
      </servlet>
          
      <servlet-mapping> 
      <servlet-name> (임시)서블릿이름
      <url-pattern> /a
      </servlet-mapping>
  class A extends HttpServlet
      doGet / doPost 오버라이딩
  ```

  

- 실행

  - http:/ip:port/컨택스트명/a

- 클라이언트로부터 입력

  - 요청  ---> 처리  ---> 응답 

  ```java
  doGet(HttpServletRequest request, HttpServletResponse response)
  String id = request.getParameter("id"); ===> 정수라면, Integer.parseInt
  ```

- db 연동하기

  - 처리 / 로그인, 회원가입, 게시물조회  ---> db조회 / 저장

  ```java
  class A extends HttpServlet() {
      doGet(..) {
          요청 ---> 응답
      }
  }
  ```

- 자바 클래스 연동하기

  - xxxDAO(각 기능 1개 SQL 메소드) /xxxDTO(VO)(레코드 1개 표현 객체) 클래스 사용

- 다른 서블릿과 연동

  - include  /  forward  ---> tomcat 요청

  ```java
  BServlet b = new BServlet();
  b.init();  ===> 최초 1번 서블릿 호출
  b.doGet(); ===> 호출시마다 사용 / 여러번 실행
  RequestDispatcher rd = request.getRequestDispatcher("/b");
  rd.include(); a-b-a
  rd.forward(); a-b
  ```

  



---



## Servlet

| 종류                      | API                                              |
| ------------------------- | ------------------------------------------------ |
| 상속                      | javax.servlet.http.HttpServlet                   |
| 매개변수 선언             | javax.servlet.http.HttpServletRequest / Response |
| 다른 서블릿 포함 이동     | javax.servlet.RequestDispatcher                  |
| 다른 서블릿과 데이터 공유 | javax.servlet.http.Cookie / HttpSession          |



### 다른 서블릿과 데이터 공유

```java
< AServlet >
request.setAttribute("name", "capmus");
RequestDispatcher rd = request.getRequestDispatcher("/b");
-
request.removeAttribute("");
    
< BServlet >
String name = (String) request.getAttribute("name");

< CServlet > 
- attribute 사용불가
```

- Cookie  /  Session

  - 하나의 서블릿에서만 공유가 아닌 다른 여러 서블릿에서 사용
  - session.setAttribute/getAttribute/removeAttribute
  - 요청 ---> 프로토콜 url 연결생성  ---> 처리 ---> 응답  ---> 연결해제 (요청 / 응답객체 삭제)
    - doGet / doPost 완료시 삭제
  - 서버는 모든 클라이언트의 정보를 서버에 남기지 않는다
    - 1개의 서버가 다수개 클라이언트 처리로 메모리 한계에 종착

  | 쿠키                            | 세션                   |
  | ------------------------------- | ---------------------- |
  | 브라우저 종료시 / 지정 시각까지 | 브라우저 종료시        |
  | 클라이언트 컴퓨터측 저장 기술   | 서버컴퓨터에 저장 기술 |
  | 문자열 저장 가능 (인코딩 설정)  | 자바객체 저장 가능     |
  | 보안 취약(영문도 암호화)        | 보안 유리              |

  - Cookie 사용

  | 1. 클라이언트에게 요청                   | 2. 서버에서 쿠키 객체로 생성               |
  | ---------------------------------------- | ------------------------------------------ |
  |                                          | Cookie c  = new Coolie("쿠키명", "값");    |
  |                                          | c.setMaxAge(60);  ---> 최대치 설정(초단위) |
  | 4. 쿠키 내용이 브라우전 전송             | 3. 클라이언트 응답                         |
  | 5.클라이언트에게 또 요청(쿠키 같이 전송) | response.addCookie(c);                     |
  |                                          | 6. request.getCookie                       |
  |                                          | Cookies[] coo = request.getCookie();       |
  |                                          | coo[0].getName();  coo[0].getVale();       |

  - Session 사용

  | 1. 클라이언트가 요청             | 2. 처리-세션 데이터 저장 공유                          |
  | -------------------------------- | ------------------------------------------------------ |
  | (로그인)                         | HttpSession session = request.getSession();            |
  |                                  | (true 이전 연결 / false 최초 연결)                     |
  | 요청                             | 3. session.setAttribute("세션속성명", 값(object));     |
  | 4. 클라이언트가 요청             | 5. HttpSession session = request.getSession();         |
  |                                  | 6. Object o = session.getAttribute("세션속성명");      |
  | 7. 응답                          | ===> 원래 타입 형변환 필요시                           |
  | 8. 클라이언트 요청한다(로그아웃) | 9. HttpSession session = request.getSession();  (true) |
  | ---> 서버에 남겨놓은 정보 삭제   | 10. session.removeAttribut("세션속성명");              |

  



## JSP

- 자바 웹서버 - 서블릿 구조 제공 + jsp 구조 제공

| 서블릿  .java                                | jsp .jsp                         |
| -------------------------------------------- | -------------------------------- |
| class A extends HttpServlet                  | <% doGet메소드에서 구현 문장; %> |
| doGet() {응답 자바 내부 html 언어 포함 형식} | <html> <body> 등                 |
| 서블릿 api 사용 처리                         | 서블릿 api + html 언어 독립적    |

- jsp = java server page
  - html + java
- 작성 ---> 실행   ===> servlet api + jsp api + 내장객체들
  - jsp 내부 tomcat server 서블릿 변환(xxx.java) - 컴파일(xxx.class) - 객체생성 - init - doGet...
  - 
- <%  %>  기본태그 /  <jsp:    > 액션태그 /  <c:    > 커스텀태그 /  ${x} el
- 1개 웹페이지 = html + css + js + servlet + jsp 연동

| html       | html, css, js, jquery                                        |
| ---------- | ------------------------------------------------------------ |
| jsp 기본   | <%  for()  %> (지역변수) / 표현문 %= /  선언문  %! (메소드, 필드변수) |
|            | 주석문  %--  /  지시문 %@ (디렉티브 태그)                    |
| jsp action | <jsp:xxxx      />                                            |
| jsp custom | ${ i}   <script>  /  $("#i")  <script>                       |
| 내장객체   | jsp는 서블릿보다 간결 응답, servlet api                      |
|            | requestl, response, exception, session  ..                   |















