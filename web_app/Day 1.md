# Day 1



---

## Review

| 웹클라이언트 기술                      | 웹서버 기술                             |
| -------------------------------------- | --------------------------------------- |
| 브라우저가 해석하고 실행               | 브라우저의 요청을 받아 실행             |
| html  /  css  /  javascript  /  jquery | servler  /  jsp  /  php  /  asp  /  cgi |
| 한정 - db 이용 기술                    |                                         |







---



## 웹 어플리케이션

> 웹페이지를 만들어내는 파일들 모음
>
> *.html  +  *.java  +  *.jsp  +  *.xml  +  sql



### 형태 규칙

- 이클립스 개발 규칙 / 그외 개발 규칙

- 이클립스

  - = web context = dynamic web project

  | java resources | src  ---> 자바소스파일 저장(서블릿)       |
  | -------------- | ----------------------------------------- |
  |                | system library                            |
  | **webcontent** | WEB-INF 폴더 - web.xml  /  lib            |
  |                | *.html  /  *.jsp  /  image  /  css  /  js |

  - localhost:9090/context(web application) 이름/



### Servlet

> server side java program   <--->   html(client side)
>
> - html 파일 실행  ---> 브라우저 표현 출력 ( 요청분석 후, 파일 찾아 클라이언트에게 전송)
> - SampleServlet.java   ---> @WebServlet("sample")
>   - sample 맵핑된 값을 찾아다님  / 컴파일 후,  클라이언트에게 전송

- 자바 파일 정의한 후, tomcat 서버 설정 알려주는 2가지 방법

| @WebServlet | class 서블릿 extends HttpServlet  / doGet 오버라이딩 |
| ----------- | ---------------------------------------------------- |
| web.xml     | class 서블릿 extends HttpServlet  / doGet 오버라이딩 |
|             | <servlet> ... </servlet>   ===> 정의 필요            |

- 서블릿 실행과정 (서블릿 컴파일 후)
  - 서블릿 객체를  메모리 heap 영역에 생성
  - 생성자 실행  --->  init 실행
  - doGet 실행  ===> 클라이언트에게 응답반복
  - 서버 메모리 삭제 
- http 프로토콜 규칙
  - **url?**파라미터명=값&...  ---> '직접입력 가능' or 'form태그 자동변경'
  - form action="서블릿url" **method="get(기본)  /  post"**
    - get : url 뒤 전송 보인다
    - post : url 뒤 전송 숨김  ---> encoding(utf-8) 변환 필요





#### 서블릿 API

- javax.servlet.http.패키지

  | 모든  서블릿 상속         | HttpServlet                                        |
  | ------------------------- | -------------------------------------------------- |
  | 모든 서블릿 오버라이딩    | doGet / doPost / doxxx / init / destroy            |
  |                           | protected void doGet(xxRequest rq, xxReseponse rp) |
  | 클라이언트 요청 처리 객체 | HttpServletRequest                                 |
  | 클라이언트 응답 처리 객체 | HttpServletResponse                                |

  | javax.servlet.Servlet                    | 인터페이스                     |
  | ---------------------------------------- | ------------------------------ |
  | class GenenicServlet implements Servlet  | 클래스는 5개 메소드 오버라이딩 |
  | class HttpServlet extends GenericServlet | + doGet \| doPost 추가         |

- 메소드

  | 메소드  | (자동 실행순서) 기능                                         |
  | ------- | ------------------------------------------------------------ |
  | doGet   | (2) / 호출할 때마다 여러번 실행 , 매번 요청시 처리           |
  | doPost  | (2) / 호출할 때마다 여러번 실행                              |
  | service | (2) / 호출할 때마다 여러번 실행                              |
  | init    | (1) / 서버 시작 1번만 실행(서블릿 최초 초기화 수행 작업)     |
  | destroy | (3) / 서버 종료시, 서블릿 코드 수정-재컴파일시, 이전서블릿 객체 삭제시 |

- get / post

  | get                          | post                                  |
  | ---------------------------- | ------------------------------------- |
  | url 뒤 붙어서 전송           | url 별도 분리 전송                    |
  | url?변수명 1 =값1&...        | 한글인코딩처리 메소드 호출            |
  | 길이 제한(파일전송불가)      | 길이 무제한(파일전송가능)             |
  | 보안 취약                    | 보안 유리                             |
  | form태그  /  주소표시줄 입력 | form태그 method=post (html 파일 필요) |
  | **doGet**                    | **doPost**                            |

- http 프로토콜 오류코드

  | 번호 | 오류                                                |
  | ---- | --------------------------------------------------- |
  | 404  | ulr 지정 파일 없다 / 서블릿 매핑 오류 / 파일명 오류 |
  | 405  | get  ---> doPost()  /  post  ---> doGet()           |
  | 500  | 서블릿 실행 오류들 / 오류이름. 메시지. 라인번호     |

  



 







