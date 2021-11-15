# Day 3



---

## Review

- Spring 기술

  - aop  /  mvc  /  spring jdbc  /  프레임워크 연동
  - mvc = model + view + controller  ===> servlet + jsp 구조
  - mvc + front controller 로 의무적 구현
    - 요청1, 2, 3.. - c - m - v  응답1, 2, 3..

  | /hello.mvc |                         |                          |
  | ---------- | ----------------------- | ------------------------ |
  | 요청       | -> web.xml              |                          |
  |            | => dispatcherServlet    | -> xxxController         |
  |            |                         |                          |
  |            | => selvlet-context.html | -> view 파일 / 결과 리턴 |
  | 응답       | <-                      | <-                       |

- annotation 태그 (xml 태그 + annotation)

- sts에서 컨택스트 명

  - http://ip:port/prjerct명
  - spring mvc project ---> package명이 컨택스트명으로 위치

- 컨트롤러 메소드의 매개변수는 자유로움

  - servlet api  ---> HttpSeesion 그대로 사용

  - 자바데이터타입 변수  ---> @RequestParam("요청파라미터")  /  요청 파라미터 이름과 동일 이름 저장

    (자동형변환)

  - 자바객체  ---> @ModelAttribute("jsp이름")

    (모든 요청 파라미터값들을 객체 필드변수명으로 동일 매핑)

- 컨트롤러 메소드의 리턴타입 자유

  - ModeAndView - 모델과 뷰 이름 설정
  - void -  @RequestMapping("uri") uri와 같은 이름의 뷰 설정
  - String - model x, 뷰이름 설정  /  return "a" ---> WEB-INF/view/a.jsp
    -  return "redirect/a"   ---> 컨트롤러 내부 /a 메소드 호출 이동

- spring mvc 실행

  - web.xml  ---> "/" **DispatcherServlet** (*.spring 등 확장자 변경 가능) + 한글인코딩 설정
  - servlet-context.html  ---> **view 저장경로 , 확장자(.jsp)**  /  @xxx 설정 인식 패키지 설정
    - base-pa... = "일정 형식" / < context:component-scan >

- 오류코드

  | 번호     | 내용                                                         |
  | -------- | ------------------------------------------------------------ |
  | 400      | controller - @RequestMapping("/") -> 메소드와 매핑 메소드 타입이 일치x |
  | 404      | spring /  @RequestMapping  / @Controller 확인  /  jsp 존재 확인 |
  | 405      | get ---> doPost  /  post ---> doGet   // jspd서는  동일 취급 |
  | 500      | 자바 예외들                                                  |
  | 200, 300 | 정상실행                                                     |

---



## Spring



### get / post

- http 요청 클라이언트 방식

  | get                     | post                             |
  | ----------------------- | -------------------------------- |
  | default값 / 주소입력 등 | html 파일 내부 /  Method ="post" |



### resource

| src/main/java                        | 컨트롤러, 패키지명.xxx(@인식 설정 필요)            |
| ------------------------------------ | -------------------------------------------------- |
| webapp/WEB-INF/views                 | 폴더.*.jsp                                         |
| webapp/resources(mvc 무관 실행 가능) | html / *.css / *.js / jquery-3.2.1..min.js / image |



### 비즈니스 로직과 mvc연동

- 비즈니스 : vo  /  dao  /  service(impl)
  - web.xml  ---> 참조하고 하는 xml을 context-param 태그에 추가!



### MVC 다양한 기능 

- file upload

  - html 태그 업로드 기능
    - < form action=""
    - method ="post"  + multipart/form-data
    - <input type="file"  ---> 파일 선택 열기 창  ===> **MultipartFile** 로 매개변수 선언(서버에서 받기)
  - 서버파일 전송받는 기능(**sping api** + jsp api)
    - pom.xml  ---> file upload, ajax 등 추가 라이브러리 설정
    - file uplooad  ---> commons-fileupload, io 다운 및 설정  ===> MVN Repository 에서 태그 복사
    - servlet-context.xml
      - 파일업로드 - Multipart.class(인식태그)  ===> < bean > 태그 사용해서 객체 사용

- restful 기능

  - a.jsp 실행 ---> 내용 + < div > 태그 속 b.jsp     <-- 객체로 전달(결과물)

- http

  - 요청 - 응답

  - 기본적 요청 처리 시간 동안 클라언트 대기. 화면 변화x

    ---> 동기화 통신 방식(synchronous)  <<-->>  비동기화 통신 방식(asynchronous) : java script

  -  변경 - 요청 - 화면 - 응답 - 변경

  - http는 이전 상태정보 유지할 수 없으니 추가 HttpSession 구현 or json / ajax

  - 비동기화 통신 방식 ===> ajax (asynchronous + java script and xml)

    - xml (초기 비동기통신시 전달 데이터 형태)  ---> **java script** 객체로 바꿈

    - json  ---> java script object notation
    - excel  /  json
    - a = { "변수명":"값", "...":"..." ...}  ===> a.변수명 --> 값 출력

- @ResponseBody





