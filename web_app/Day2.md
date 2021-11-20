# Day 2



---

## Review

- web application = web context : 웹 서비스 위해 사용 ㅇ여러가지 파일 모음
  - src ---> *.java
  - webcontent  ---> jsp, html, css, js, jpg, **web.xml**(웹서비스 환경설정 파일 )
  - http://서버Root url /CONTEXT(dynamic web project)/ *.html
- servlet.java
  - url 맵핑이 필요  ---> @WebServlet  /  web.xml  ---> 절대 중복 불가
  - 실행과정
    - 서블릿 객체 매모리 생성  ---> 생성자 실행  ---> init 실행 (종료시까지 한번만 실행)
    - 요청(HttpServletRequest)  ---> 응답(HttpServletResponse) 객체 생성 (계속 반복)
    - (종료시, 재컴파일시)  서블릿 객체 메모리 삭제
- 요청
  - String  ---> request.getParameter("input name 속성값 1개");
  - String[]  ---> request.getParameterValues(속성값이 여러개)
  - request.setCharacterEncoding("utf-8");  ---> 한글의 경우 인코딩이 필요
  - 요청방식  ===> **get(default)  /  post**  <입력양식 유도>
- 응답
  - response.setContentType("text/html;charset=utf-8")  // images/gif 등 가능
  - PrintWriter o = response.getWriter();
  - o.println("태그입력 가능  //  h1태그 등")
  - get ---> doGet메서드  /  post  ---> doPost메서드  // 전부 service로 받을 수 있음
- 처리  ===> 자바의 모든것

---



## Servelet

> 요청 => 처리 => 응답 (반복)



### 로직처리

JDBC활용



### Connection pool

- tomcat server를 활용
- 일정 갯수 생성 - 공유
- 설정 ---> dbcp 라이브러리 이용  ===> javax.sql.DataSource 객체
  - 이클립스 Server/tomvet local.../context.xml or server.xml

```xml
<Context docBase="servlettest" path="/servlettest" reloadable="true"     source="org.eclipse.jst.jee.server:servlettest">
      <Resource type="javax.sql.DataSource" 
      name="jdbc/myoracle" 
      username="hr" url="jdbc:oracle:thin:@127.0.0.1:1521:xe" 
      password="hr" 
      driverClassName="oracle.jdbc.driver.OracleDriver" 
      maxIdle="5" 
      MaxActive="5"/>
</Context>
```

- servlet - servlet 호출(서버 내부 2개 이상의 파일 연동)

  ```java
  class AServlet extends HttpServlet
  doGet() {
      MemberDAO dao = new ...;
      dao.메소드()
  }
  BServlet b = new BServlet();  ---> tomcat 최초1번만
  b.init;
  b.doGet();
  
  doGet() {
      RequestDispatcher rd = request.getRequestDispatcher("/bservlet");--->BServlet 호출
      rd.include(request, response);  // A-B-A
      // or rd.forward(request, response); A - 결과 B
      AServlet 남은 내용 처리
  }
  ```

- forward / include (서블릿끼리 연동)  /// **dispatch 포워딩**

  - include  --> 요청한 A결과 + A에서 연동된 B의결과 포함
  - forward  ---> 요청한 A 중 forward 전까지의 결과 + forward 이후 B의 결과




