# Day 4



## Review

- set / get / remove Attribute  ---> 정보를 다른 서블릿에서도 처리
- session.set / get / remove Attribute  ===> 공유의 범위가 훨씬 늘어남
- 서블릿과 jsp의 쿠기와 세션 사용
  - 쿠키 - 클라이언트, 문자열, 보안취약(인코딩)
  - 세션 - 서버, 자바객체, 보안강호, 데이터무제한
- 쿠키 사용
  - 클라이언트의 요청
  - 쿠키를 객체로 생성 / 클라이언트 응답  ---> 브라우저 전송
  - (반복) 클라이언트 요청  ---> 클라이언트로부터 쿠키 사용
- 세션 사용
  - 클라이언트의 첫요청
  - 처리(세션 데이터 저장)  ---> 공유
  - session.setAttribute("세션속성명", Object값);
  - 클라이언트의 요청
  - getSession - -->  getAttribute
  - 로그아웃 요청  ---> 있는 정보로 removeAttribute

- api(서블릿과 jsp)

  - 상속(jsp 필요x) - HttpServlet
  - 매개변수 선언 - request/response
  - 데이터공유 - session

- 서블릿 /  jsp

  - 서블릿 - 자바클래스, 메소드, 오버라이딩, 자바문장 내부  html태그 포함
  - jsp - 상속, 오버라이딩 필요x

- jsp

  - html, css, jsp, jquery 사용

  - jsp기본 : 지역변수 선언 / 필드변수 선언 / 메소드 정의, 주석, 출력( <%=)
    - <%@ page import=""
    - <%@ include / taglib



---



## JSP



### 내장객체

- 자주 사용 객체 미리 변수 선언 제공

- **_jspService()** - <%!를 제외한 모든 실행코드 포함

- **_jspService()** 지역변수처럼 취급

  | 내장객체이름    | 타입                            | 역할                                   |
  | --------------- | ------------------------------- | -------------------------------------- |
  | **request**     | http.HttpServletRequest         | 요청 처리                              |
  | **response**    | http.HttpServletResponse        | 응답 처리                              |
  | **out**         | jsp.JspWriter(PrintWriter 하위) | 응답 출력 객체 생성                    |
  | **session**     | http.HttpSession                | 브라우저 내부 공유                     |
  | page            | lang.Object(클래스 this와 유사) | 현재 jsp 소스를 서블릿 소스 변환       |
  | pageContext     | jsp.PageContext                 | 현재 jsp 내장객체 조회 객체            |
  | config          | servlet.ServletConfig           | web.xml 파일에 변수 저장 현재 jsp 사용 |
  | **application** | servlet.ServletContext          | 현재 context에 변수 저장 모든 jsp 사용 |
  |                 | get(set)Attribute("변수")       |                                        |
  | **exception**   | lang.Trowable                   | 예외객체                               |

  - request  /  **session**  /  application  Attribute  ---> 범위의 확장

  - exception

    - http 프로토콜 응답코드

      | 오류코드 | 내용                                                  |
      | -------- | ----------------------------------------------------- |
      | 200, 300 | 정상 실행 정상 결과 응답                              |
      | 404      | 요청파일 서버내부 존재X                               |
      | 405      | get 방식 --> doPost 처리  /  post 방식 --> doGet 처리 |
      | 400      | su = aaa  ===> (스프링) 처리메소드(int su) / 타입오류 |
      | 500      | 서블릿이나 jsp 논리 오류  ---> exception              |

      ```jsp
      a.jsp
      NullPointerException 발생 = 500
      try{} catch{}
         ---> c.jsp <%@ page isErrorPage="true"  //예외 처리 전담
              exception 내장객체 사용 가능
      <%@ page errorPage = "c.jsp" //예외발생시
          
      b.jsp
      NullPointerException 발생 = 500
      try{} catch{}
      ---> <%@ page errorPage = "c.jsp"
      ```

- welcome 파일  ---> context까지만 입력시 동작되는 파일

  - web.xml에서 <welcome-file> 지정



### 액션 태그

- 서블릿
  - RequestDispatcher rd = request.getResquestDispatcher("/b or b.jsp");
  - rd.include;  /  rd.forward;
- **jsp**(서블릿, 자바를 쉽게 사용)
  - <jsp:include page="/b or b.jsp" />
  - <jsp:forward page="/b or b.jsp" />
  - <jsp:useBean id="vo" class="vo.MemberVO" scope="request" />
  - <jsp:get(set)Property

- useBean / setProperty

  ```jsp
  <%@ page import="vo.MemberVO"
  <%=vo.getMemberid() %>
  ---->
  <jsp:useBean id="vo" class"MemmerVO" />
  <jsp:setProperty name="vo" property="memberid" value="member1" />
  <jsp:getProperty name="vo" property="memberid" />
  ===>jsp(html태그 웹디자이너 + 자바문장 웹개발자)
  ```

  



































