# Day 5



---

## Review



- 함수
  - function f1() { }  ---> <script> 시작되자마자 함수 정의 선언 //
  - 다른 함수(function() { });
  - var a = function() { }  ---> 변수 선언문 사용시 선언
  - var b = [1, 2, 3, 4];
  - var c = {변수명: 값, ... 변수명: 함수};
  - var d = [다양한 타입, 요소 객체 가능 / 논리값, 함수 등]
- dom : html 태그를 객체 형태로 Document Object Model
  - 1개 태그를 dom 객체로 리턴 ---> dom.gEBI("id"); queryselector
  - 여러 태그명을 dom 배열로 리턴  ---> dom.gEsBTN("태그명"); / queryselectall
  - dom.style
  - dom.innerHTML
  - dom.textContent
  - dom.해당태그속성명
  - img  ---> src, width, height
  - a ---> href
  - dom을 객체인지 배열인지 구분 필수
- 이벤트
  - window.onload
  
  - 모든태그 = onclick, ocdblock, onmouseover/out
  
  - innput type=text ---> onkeydown 1 /press 2 /up 3
  
  - input type=button  --->onclick, onchange
  
  - input type=submit  ---> onsubmit
  
    

---

## j-query

> java script ---> 변수 연산자 함수 객체 dom 이벤트
>
> dom + 이벤트 + 함수  ===> 구조 간결 쉽게 제공. 라이브러리 추가
>
> node.js  ===> 특화 기능 제공. 라이브러리
>
> vue.js,  react.js  ===> 화면 구성 컨텐츠 추가

```html
<script src="jquery.js"></script>
<script>
...
</script>
```

###  문법

- $ = jQuery 객체명 

  - jQuery객체.속성변수 없다.
  - jQuery객체.함수명()
  - $('css selector').jQuery객체포함 함수명()
  - $('css selector') 태그 선택하여 jquery 객체 변환
  - jQuery함수 - 속성 조회 / 설정, 다른태그 추가, 삭제 수정 , 이벤트 처리 함수
    - 문서 객체 조작

  ```html
  $(document).ready(function() {
  $("h1").css("color", "red");
  })
  
  window.onload = function() {
  document.getElementByTagName("h1")[0].style.color = "red";
  }
  ```

  - dom 객체. 속성명 = "값";   ---> javascript



### 함수

| css(스타일)                | ("속성명", "값"); setter형  /  ("속성명"); getter형     |
| -------------------------- | ------------------------------------------------------- |
| attr(속성)                 | attr("태그의 속성명", "값");  /  attr("태그의 속성명"); |
|                            | removeAttr("속성명")   ---> 해당 속성 삭제              |
| html(태그내부 컨텐츠 출력) | == innerHTML 같은 역할 (태그 실행 o)                    |
|                            | $().html("..."); / html(); getter  /  html(" "); setter |
| text(태그내부 컨텐츠 출력) | textContent 변수 같은 역할( 태그 실행 x)                |
| append                     | 이전 컨텐츠 뒤에 추가 역할( += )  /  append(" ..");     |
| empty()  /  remove()       | 속성 내부값 삭제  /  속성 자체를 삭제                   |
| addClass  /  removeClass   | 태그에 클래스 추가 / 삭제  /  .클래스명 { css 정의 }    |
| toggleClass                | 분류시 css  /  add와 remove를 한개로 사용               |
| val()                      | input 입력 / 선택값                                     |

| hide / show  | 일시적                                                    |
| ------------ | --------------------------------------------------------- |
| slideup/down |                                                           |
| on           | 이벤트 처리  /  **$(' ').on('click', function(e) { } );** |
| off          | 이벤트 취소 /  **$(' ').off('click', function(e) { } );** |





































