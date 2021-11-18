# Javascript_library

---

## Review

- html5 = html + css + java script

  - 컨텐츠 + 스타일 + 동작
  - 변수 /  연산자  /  제어문  /  함수  /  객체  /  이벤트 처리

- script를 html 내부에 작성

  ```js
  <script> 
      ,,,
  </script>
  ```

- html 파일 외부의 *.js 파일 작성

  - vue.js  /  react.js  /  angular.js  ===> 자바 스크립트 언어 구현 특정 기능 수행  ( + node.js)
  - jquery 라이브러리



---



## 자바스크립트 라이브러리

> document.write()  /  alert()  /  parseInt()  ...



### 콜백함수 유형

- 자바스크립트 객체 - window
  - (window.) 메소드명()
- window.setTimeout(함수)
  - setTimeout(f, t) { t 시간 경과 후에 f 함수 내용 실행}
  - f();  ---> 즉각 실행



### 객체

- window.(내장객체)  /  window.포함객체  /  window.함수
- Date.toLocaleTimeString();  /  Date.toLocaleDateString();
- "aaaa".indexof('b')  /  "aaaa".substring(1, 2) - "aa"
- "aaaa".split(",")
- 사용자 객체 정의
  - var 배열변수명 = [1, 2, 3, 4, ...];
    - 함수, 배열도 변수로 포함 가능
  - var 객체변수명 = { id:1, name:"이자바", test: function(){...} };



### 문서 객체 모델

- DOM : document object model

- HTML 태그를 자바스크립트 객체 변환 타입

- 정적 구성을 자바스크립트 실행 결과 동적으로 변경

  - 자바스크립트에서 HTML 태그 접근해 내용 변경 작업 수행

- 요소노드  /  속성노드  /  텍스트노드

  

### 이벤트

- 키보드나 마우스 동작 등
- 마우스 이벤트 - 모든 html 태그 가능
- 키보드 이벤트 - input type=text / password 가능
- 포커스 이벤트 - 모든 html 가능
- 구조 변화 이벤트 - input type=checkbox / radipo, select option
- 터치 이벤트 - 지원기기에 따라 종속적
-  이벤트발생객체.on이벤트종류 = 이벤트핸들러함수 or 리스너

```js
function action() {}
window.onload = action;  ---> 로딩 완료시, 함수 실행
document.getElementById("aa").onclick = 함수;
```

- DOM 레벨0 ---> 인라인 / 고전 이벤트 모델
  - 인라인 이벤트모델
  - 고전 이벤트모델

