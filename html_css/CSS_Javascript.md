# CSS / Javascript

---

## Review

- web client 기술

  - 웹서버 요청  ---> 요청 방식 + 서비스 응답
  - 웹 브라우저(url + html 방식 출력)

-  html5  ===> html 태그 + css 스타일 + java script 언어

  - html 파일 내부 정의 = 각 문법 다르다

  | html 태그          | css                             | java script                |
  | ------------------ | ------------------------------- | -------------------------- |
  | 화면 내용 구성     | 색상 크기 모양 배치 결정        | 동작 추가                  |
  | <body> ... </body> | <head> <style> </style> </head> | html 태그에 동작 추가 언어 |
  |                    | <link href = "a.css">           | <script> </script>         |

- css 선택자

  - ' * '  /  #id값  /  .class값
  - 부모태그명 자식태그명 (자식의 자식도 포함) /  태그명, 태그명  /  태그명 > 태그명 (직전의 자식만 포함)
  - 태그명[속성 = 값]  ---> ' * ' =. $= 등

- 색상 / 크기 / 모양 / 여백 / 선 / 배경

  - color, border-color,  background-color  ---> 영문색상명, #rrggbb (16진수 6자리)
  - width, height  ---> 태그 내장 div, hi 태그
  - px, 0.5em(50%)
  - font-family : 서체, font-size : 15px(기본)
  - text-align : right, left, center
  - box-shadow : px px px(흐리기) color / text 에도 적용가능
  - "모든 태그 박스 모델"  ---> 이미지 비디오 텍스트 모두 박스 형태
  - margin : auto(좌우 중앙정렬)  /  padding
  - border : 굵기 종류 색상
  - background - image : url("이미지파일 경로")



---



## CSS



### css속성

#### 위치 속성

- 기본 설정 포지셔닝

  - 컨텐츠 사이즈에 따라 박스 사이즈가 결정
  - 기본 설정이 block인 경우 가로길이는 화면 끝까지
  - 코드 순서에 따라 디스플레이에 나타남
  - 부모, 자식 태그에서 자식 태그가 우선 적용

- 배치o (static)  /  배치x (relative, absolute, fixed)

  - relative : 원래 있었어야 할 위치를 기준으로 좌표가 이동

    (상대적 위치)

  - absolute : 부모 태그 영역 내부에서 top, bottom... 이동

    - 부모영역 내에서 내 위치 고정시킬 때

  - fixed : 전체 브라우저 내부를 기준으로 위치 조정

  - z-index : 겹치는 경우 우선순위를 표시 / 크면 클수록 우선헤서 표시

    - (없으면) 0 이라고 생각

- overflow : 크기에 비해 내용이 많을 경우 처리방법

  - hidden, scroll 등





---



## Java Script

> 문법적으로 자바와 유사  ===> ECMA SCRIPT
>
> but, 전혀 다른 언어



### 기본 용어

- 표현식 : 값을 만들어내는 코드
- 문장 : 실행 최소 단위(;)
  - ' ; '  ---> 자바는 필수 / 스크립트는 엔터키가 대신 가능
- 키워드 : 자바와 거의 유사
- 식별자 : 자바와 유사( _, $, 숫자 문자들, 숫자 시작 불가능, 키워드 사용 불가능...)
- 주석 : //,  /* ... */
- 변수 : 다르다
- 연산자 : 자바와 거의 유사

 | 산술         | +  -  *  /  --> 10 / 3 (java 3 / jsp 3.333..)                |
 | ------------ | ------------------------------------------------------   ------ |
 | 비교         | >  >=  <  <==  !==  ==(값동일 비교)  /  js : === (값과 타입 동일 비교) |
 | 논리         | &&  \|\|  !  /  sql : and or not                             |
 | 대입         | =                                                            |
 | 조건삼항비교 | ?:  /  a?b:c  /  a판별 true  --> b  /  a판별 false  --> c    |

- 자료형

  | 숫자   | 정수 실수 표현 가능      |
  | ------ | ------------------------ |
  | 논리값 | true  /  false  2개 표현 |
  | 문자열 | ' xxx', "xxx"            |

- 변수

  | 숫자            |      |
  | --------------- | ---- |
  | 논리값          |      |
  | 문자열          |      |
  | 함수            |      |
  | 객체(배열 포함) |      |
  | undefined       |      |

  - 변수 선언

    - var i  ---> 타입은 모름. i = true; 등 가능  ===> 자바에 비해 유연함
    - int i;  ---> 정수 선언 i = 100;
    - es6 : let, const 추가

  - undefined

    ```jsp
    var j;
    alert(j);  ===> undefined
    j = first;
    alert(j) = 'first'
    ```


- 배열

  - ArrayList 와 유사

  - 여러개 타입 자료 저장 가능

  - 동적인 길이

  - 문법은 java와 차이가 존재 / 생성, 수정 등이 유연

    ```js
    var a1 = [1, 3.14, 'java', true, undefined, null];  ===> 배열 선언 생성 초기화
    a1.length;  ===> 6
    a1[0] 출력  ===> 1
    a1[6] = "추가합니다";  ===> 추가
    a1[6] 출력  ===> "추가합니다"
    a1[0] = 100;  ===> 수정
    
    var a2 = [];  ===> 배열 선언 생성
    a2[0] = 100;  ===> 배열에 추가
    
    var a1 = new Array[5];
    ```

- 반복문

  ```js
  for(var i = 0; i < a1.length; i++) {
   document.write(a1[i]);
  }
  
  
  
  a1.join(",");  ===> a1 배열 0 ~ 마지막 인덱스 데이터 / 각 데이터 분리자
  ```

  

- 함수 : **function** - 자바 메소드 구조 / 기능(객체동작) 유사

  - 리턴타입?

  ```js
  function (i, j, k) { //갯수
      ....
      return xxxx;
  }
  ---> 무명의 함수 정의 + 1번 호출 실행
  
  var contents = function (i, j, k) {return xxx;}  ---> 함수 정의 소스 내용/ 함수를 변수로
  contents(1, 2, 3);  ===> 실행
  ```

  ```js
  function 함수명(i, j, k) {//갯수
      return xxx
  }  ---> 유명의 함수 정의
  ===> 호출 후 여러번 사용
  var r1 = 함수명(1, 2, 3);
  ```

  
