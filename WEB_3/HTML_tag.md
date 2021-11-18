# HTML_tag



- **설치**

  - http 서버 프로그램  ---> apache-tomcat
  - http 클라이언트 프로그램  ---> web browser
  - java, sql, html 작성 / 편집  ---> 이클립스

- java와 tomcat 연동

  | JAVA resources\src                  | *.java  자바파일 저장    |
  | ----------------------------------- | ------------------------ |
  | Webcontent                          | *.html  *.jsp   파일저장 |
  | jre system library,  tomcat library | 웹서버 동작              |

  



## HTML5

> 웹 서비스를 보여주는 언어

### Web 동작

- protocol : 인터넷 상 모든 컴퓨터 통신 방식
- 요청 - 응답  ---> 브라우저 이용 요청 방식
- **http://ip:port/a.html**
  - 프로토콜명:// 서버사이트식별자 / 프로그램 이름
  - url uniform resource lacation web 표준 - 서버 식별방법
  - 프로토콜 : 서버와 클라이언트간의 약속된 규칙
    - tcp,  http,  ftp,  telnet,  jdbc
- 웹서버만 독자 이름 부여! (google.com/**a.jsp**)
- 웹서버 내컴퓨터
  - http://127.0.0.1:8080/프로그램명
- 서버 프로그램(백엔드) / 클라이언트 프로그램(프론트엔드)
- 웹 표준 기술  ===>  HTML5 + CSS3 + JS  (+ JQUERY)  //  웹 표준 2.0



### 기본 용어



#### 태그와 요소

- **h1 태그** : 제목 크고 굵게 표시 기능

  ```html
  <h1> 내용 </h1>
  ```

- **img 태그** : 이미지 표시기능. 부가설명 필요

  - 부가적 설명.src  속성  --->  이미지이름 alt  속성 = 이미지 표시 불가능한 경우 대체문자열

  ```html
  <img src = "a.jpg" alt = "이미지 삭제되었어요" >
  ```

- html 구성요소

  - 태그  /  속성  /  내용

- 주석 : <!-- 내용반영 x -->



#### 페이지 구조와 작성

> html  -  head  --  body  --  html\

- html 태그
  - title, script, link, style
- 오류와 검증





### 기본 태그



#### 글자 태그

- 제목과 본문 글자 태그
- h, 제목 크기 6단계
- P : 내용 입력 띄어쓰기나 줄바꿈은 태그가 필요

- text  :  문자,

- hyper text : 문자 링크 따라가서 다른 문서 조작  ===> 앵커 태그 'a href'

  ```html
  <p>
      다음 사이트 
  </p>
  
  <a href = "http://www.daum.net" > 다음 사이트 </a>
  ```

- 앵커 태그

  - 절대 경로 : url 전부 입력
  - 상대 경로 : 비슷한 경로일경우 생략 가능 ex. '../other/another'  or  '/other/another'
  - 아이디 경로 : id 속성이 name인 태그의 위치로 이동 ! ---> #name
  - 메일 경로

- 글자 모양 태그 : b,  i,  small,  sub 등등



#### 목록 태그

- 순서 / 기호 에 따른 목록 표현
- 내비게이션 메뉴
  - ul(순서가 없는 목록) - 타입의 변환 가능
  - ol(순서가 있는 목록) - 타입의 변환 가능
  - li(목록요소)



#### 테이블 태그

- 테이블 구성을 위한 태그

- table : 표삽입

- tr : 표에 행 삽입

- th : 표의 제목 셀 생성

- td : 표의 일반 셀 생성  ---> colspan 가로 확장, rowspan 세로 확장

  ```html
  <table>
      <tr> <td> </td> <td> </td> </tr>
      <tr> <td> </td> <td> </td> </tr>
  </table>
  ```

  

#### 미디어 태그

- video, audio, img  전부 사용 가능
- (html5 이전) 플러그인으로 사용  ---> 브라우저 종속적
- 이미지 크기 조정  ===> width(가로), height(세로)
- audio 태그( + controls 필요!)
- vedio 태그 ( + controls 필요!) ---> 크기 조절 가능 / poster 설정 가능
- audio, video 모두 브라우져 마다 지원하는 확장자가 조금씩 다름
  - 크롬, 파이어폭스는 모두 지원





### 입력 양식 태그 / 구조화 태그



#### 입력 양식

- form 태그 : 영역 생성 / 입력양식의 시작과 끝을 표시  ---> input 태그 타입 사용
- action - form 내부의 값을 정해진 파일로 전송  ===> xxx.js 등
- input type : 다양한 입력 양식이 존재  + value = 입력전 최초값
  - text  --->  글자 입력 양식 생성
  - maxlength = '10'  //  size = '5'  ---> 총 10글자 5글자씩 끊기
  - check box  ---> 체크 박스 생성
  - file  ---> 파일 입력 양식 생성
  - hidden  ---> 해당내용 표시 안함
  - password  ---> 비밀번호 입력 양식 생성
  - submit value =XXX  ---> xxx 이름을 가진 제출버튼 생성
  - select  ---> 선택 양식 생성
    - option(group)  ---> 옵션 생성 및 옵션 그룹화
    - multiple  (= "multiple") ---> 다중선택가능











