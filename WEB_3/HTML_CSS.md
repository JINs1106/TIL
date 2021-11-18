# HTML/CSS

---

## Review

- 웹 : 인터넷 서비스
  - 텍스트 / 이미지 / 동영상 / 음향
  - 링크 / 목록 / 테이블 표현 언어
  - html 5 사용
  
- 웹서버 프로그램 TOMCAT
  - 이클립스 연동  ---> dynamic web project
  - scr x / web content 에 저장
  - http://localhost:9090/프로젝트명/test.html
  
- html 태그

  **<태그 속성이름1 = '속성값1' 속성이름2 = '속성값2' > 내용 </태그>**

  - 태그 종류별로 다양
  - 제목 태그 : h1 ~ h6
  - p  /  br  /  &nbsp  :  공백  /  줄바꿈
  - 테이블 태그 : table  tr  th  td
  - 연결 태그 : a href = '링크url' (하이퍼링크)
    - http://www.multicampus.com
    - http://localhost:9090/프로젝트명/파일명
    - /프로젝트명/파일명  ---> 내 서버의 특정파일
    - ../다른 프로젝트 명/다른 파일명  ---> 현재 파일과 같은 서버
    - 파일명  ---> 현재 파일과 같은 경로
  - 멀티미디어 태그 : img, audio, video
    - ( + src =)  : 파일 속성
    - alt / poster : 이미지 대신 문자열  /  동영상 대신 이미지
    - controlls  :  audio, video 속성에 필요 / 재생버튼
  - 입력양식 태그
    - form, input, select 등



---



## HTML5



### 입력 태그 / 구조 태그



#### 입력태그 추가

| text, password              | 키보드 입력                                                  |
| --------------------------- | ------------------------------------------------------------ |
| checkbox(단일), radio(다중) | 화면에 출력, 마우스 선택                                     |
| hidden                      | action 지정 파일로 전송, value 필수                          |
| file, image                 | 파일 선택창 열림                                             |
| submit                      | 버튼, 클릭  /  기능 ---> action 지정 피일로 전송             |
| reset                       | 버튼, 클릭  /  기능  ---> 입력 취소, 전송 취소               |
| button                      | 버튼, 클릭  /  기능 ---> 내장 기능 x,  사용자 정의(jsp와 연동) |
| (html5 추가)                | 브라우저마다 조금씩 다르거나 미지원                          |
| number                      | color                                                        |
| range                       | date                                                         |

- form 태그 포함 태그

  | input           | 키보드 1줄 입력     |
  | --------------- | ------------------- |
  | select - option | 드롭다운 선택리스트 |
  | textarea        | 키보드 여러줄 입력  |

  

- button : 기능 정의가 필요
  - onclick 속성  ---> 클릭했을 시 반응

- hidden : value 속성 필수



#### 구조화 태그

- 공간 분할 태그  ---> 화면상 표현 x, 다른 태그 그룹지어 의미있는 공간 차지
  - ex. 일정 구역 색상 변경

- 시멘틱 태그 : (의미론적인) 구분의 의미 / 시멘틱 태그를 사용한 시멘틱 웹 구현
  - html5 : header, footer, article, section 등
- div : 전체적인 영역구분
- span : 한줄에 연속되어 있을때 영역 구분





---



## CSS

> css - --> cascading style sheet
>
> cascade  ---> 태그 내부 포함 다른 태그 효과 전달
>
> style  ---> 태그 색상 크기 정렬 모양 설정 방법
>
> sheet  ---> 스타일 따로 모아서 정의 그룹

```html
<head>
    <title> 브라우저 탭 제목 </title>
    <style>
        #pink { color : red; }
    </style>
</head>
```



### CSS 적용

- inline 방식 정의  ---> 특정 태그에만 적용

  <태그 style = "css 속성명:값;" >

- 현재 파일 head 태그 내부 style 태그 정의 방식
  - 여러 동일태그에 동일적용
- 외부 css 파일 정의 연결 방식 link태그
  - share.css  ---> css에 정의 여러 파일 공통 사용
  - link 태그



### CSS 문법

> 어떤 스타일을 어떤 값으로 어떤 태그에 사용

- 선택자 종류

  - 매우 다양
  -  ' * '  /  부모 (공백) 자식 /  #아이디  /.클래스
    - 아이디  태그  클래스 '*' 순으로 ccs 적용
  - 자손 선택자  ---> 바로 밑에 것  ===> ' > '
  - 후손 선택자  ---> 밑에 모든 것  ===> (공백)

  



#### STYLE

```html
<h1 style = "color : 빨간색 ; background=color:pink;;"
```





### CSS 속성



#### 박스 속성

- 가로길이가 브라우저 길이와 동일

- 페이지 전체와의 내장여백이 존재( = margin)  ---> margin 네 방향의 사이즈를 다르게 설정 가능

  - auto 로 자동조절 가능

- 내부여백( = padding) + 선굵기( = border)

  ===> 박스의 형태를 가진다

- border

  - style, color, width 변경가능
  - 사방 테두리 각각 변경 가능

  - radius로 테두리 둥글게 가능 / 사방 다르게 적용 가능 / 시계 방향 적용

-  ex. div
- 검사로 코드 분석 가능



#### 가시속성

-  display 
  - none 으로 안보이게 가능
  - block : 한줄에 한 태그 적용
  - inline : 하나의 라인에 표현
    - margin과 padding 속성을 왼쪽 오른쪽만 조절가능
    - block : 원하는 만큼 크기 조정가능. 한라인에 표현



#### 배경속성

- background
  - image, size, repeat, attachment(scroll,fixed)
  - position, color 등



#### 글자속성

- 다국적 사용자 대상용 글꼴
  - 고정폭 글꼴, serif체
- font
  - 마지막 글꼴은 웹브라우저 기본 글꼴 두기
  - 크기, 굵기 등을 조절
- text
  - align : 텍스트 위치



---

#### 색상

- rbg모드 색상 조합
  - red 0-255  / green 0-255 / blue 0-255

- 색상 코드 : #000000 ~ #FFFFFF

---





























