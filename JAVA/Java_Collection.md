# Java_Collection

---

## REVIEW



###  java.lang.Object

- 최상위 클래스 - 모든 메소드들은 다른 자바 클래스 포함. 그대로 사용
- 오버라이딩 - **toString()** / **equals()**
- **toString()** : 패키지명.클래스명@16진수주소값

​                             출력문장 내부 자동 호출. 객체 출력 내용 변경

- **equals()** : 객체의 (주소)동등성 비교

​                         객체의 주소가 아닌 특정 변수 데이터값 동등성 비교 변경



### java.lang.String

- +연산자 이용 문자열 결합

- new 키워드 이용하지 않아도 문자열 객체 생성

  ```java
  String s1 = "java";   // 100번지 
  String s2 = "java";   // 100번지
  String s3 = new String("java");  //300번지
  String s4 = new String("java");  //400번지
  ```

  ```java
  // == : "문자열" 저장 메모리 주소 / 같은 객체인지 비교
  s1 == s2 --> true
  s3 == s4 --> false
  ```

  ```java
  s1.equals(s2)
  class String extends Object {
      equals() 오버라이딩 "문자열"내용 비교 수정 + 추가 메소드
  }
  s1.equals(s2) --> true
  s3.equals(s3) --> true
  ```

 - 생성자

     ```java
     new String("java");
     new String(new byte[] {65,66,67,68}) ==> "ABCD"
     new Strring(new char[] {'a','b','c','d'}) ==> "ABCD"
     ```
     
- 메소드

     ```java
     equals / equalsIgnoreCase : 문자열 내용 동등성 비교
     toUpperCase / toLowerCase : 대소문자 변경
     replace('k','a') : k를 a로 변경
     "java".substring(1) : 2번째 문자부터 마지막문자까지 추출 --> "ava"
     "java".substring(1, 3) : 2번째 문자부터 3번째 문자까지 추출 --> "av"
     "java".indexOf('j') : j 문자 몇번째인지 --> 0번째
     "javaprogramming".indexOf("program") : program 이며 몇번째인지 --> 4
     "java".length() : 문자열 몇개 --> 4
     String s2 [] = new String[4];  ==> s2.length --> 4 //배열의 갯수
     String details[] = "java sql jdbc html javascript css servlet jsp spring".split(" ");
         //하이픈을 기준으로 분리 --> 9개 배열 발생
     StringBuilder / StringBuffer / StringTokenizer
     ```



### java.util.Date / Calendar

- import java.util.*;    or  import java.util.Date;

- 날짜 시간 표현 (국가,  지역, 컴퓨터 마다 표현방법 차이)

- Date 클래스의 대부분 메소드는 **deprecated**(사용자제)

- Date 클래스의 대부분 기능은 Calendar 클래스로 이동

  ```java
  Date d = new Date();
  Date d2 = new Date(1/1000초 long타입 데이터);
  ```

  ```java
  Calendar cal = Calendar.getInstance();  //static getInstance() 
  new Calendar();  //abstract 클리스 -> 이미 상속 메소드 오버라이딩 클래스 객체 생성까지
  ```

- cal.get(Calendar.static변수)

  ```java
  cal.get(Calendar.YEAR) //원하는 날짜값(연도) 등
  ```



### java.text.SimpleDateFormat / DecimalFomat

- **SimpleDateFormat ** :날짜시간 표현 포맷 미리 설정

- "yyyy - MM - dd  HH:mm:ss E"

  ```java
  SimpleDateFormat sf = nwe SimpleDateFormat("yyyy - MM - dd  HH:mm:ss E")
  sf.format(Date 객체나 메소드)
  sf.format(new Date());
  sf.format(cal.getTime());
  ```

- **DecimalFormat** : 숫자 표현 포맷 미리 설정

  ```ja0
  # : 1자리의 숫자. 의미없는 0 표시 x
  0 : 1자리의 숫자. 의미없는 0 표시 o
  "#.000" 
  ```



---



## 15장. 컬랙션 프레임워크

>  객체 여러개 저장 자바 변수 '배열' -> 동일타입의 데이터 여러개 저장 변수
>
> - 동일 타입만 저장 한계가 존재
>
> - 배열 정적 크기 유지
>
>   ```java
>   int[] i = new int[5]; // 100번지
>   ...
>   i = new int[10]; // 선언은 가능. but, 200번지에 10개 생성 -> 앞선 5개 데이터 사용불가...
>   A ai[] = nwe A[10];
>   ai[0] = new A[];
>   ```



### java.util.객체여러개저장클래스 (배열과는 차이)

| java.util.List 인터페이스  |   java.util.Set 인터페이스   |          java.util.Map           |
| :------------------------: | :--------------------------: | :------------------------------: |
|   ArrayList, LinkedList    |       HashSet, TreeSet       |        HashMap, HashTable        |
| 다른 타입 데이터 저장 가능 |  다른 타입 데이터 저장 가능  |    다른 타입 데이터 저장 가능    |
| 저장 데이터 갯수 동적 변경 |  저장 데이터 갯수 동적 변경  |    저장 데이터 갯수 동적 변경    |
|   저장 순서 유지 = index   |  저장 순서 유지 x = index x  |    저장 순서 유지 x = index x    |
| 같은 데이터 중복 저장 가능 | 같은 데이터 중복 저장 불가능 | 같은 key 데이터 중복 저장 불가능 |
|       학생 점수 저장       |         로또번호 6개         |       데이터(key + value)        |



#### List 컬랙션

> List 포함 메소드 오버라이딩

**ArryaList** 

자바 모든 타입 저장 가능. 최초 5개 객체 저장 가능한 길이 생성. 부족시 +2개씩 추가.  ArrayList

```java
ArraList list = new ArrayList(); // ArrayList(5), ArrayList(5, 2)
ArraList<객체타입고정> list = new ArrayList<객체타입고정>(); //해당 타입만 list에 저장
A ai[] = new A[10];
```

- 저장메소드

  ```java
  list.add(100);
  list.add(3.14); list.size();
  list.add(new A());
  list.add("java");
  list.addObject / list / addElement()
  ```
  
- 삭제메소드

  ```java
  list.remove(1); // 1번 인덱스 삭제
  list.remove("java");
  ```
  
- 수정메소드

  ```java
  list.set(1, "aaa");
  ```
  
- 조회메소드

  ```java
  list.size(); -> int // 장데이터 갯수 조회
  list.get(1); -> Object // 데이터 내용 조회
  list.indexOf("java"); -> int // 데이터 저장 위치 조회
  list.contains("java"); -> boolean // 데이터 포함 여부 조회
  ```

- list.add(Object타입)

- ArraList<객체타입고정> list = new ArrayList<객체타입고정>();

  - 지정 객체 클래스로만 사용 제한 



#### Set 컬렉션

**HashSet**

객체 중복 저장 불가. ex. HashSet, TreeSet 등

데이터 저장 순서 X.

- add(Object o)

- set() --> List에서 수정 X

- remove(Object o)

- size()

```java
for(배열저장데이터타입 변수명 : a) {  //간결. 향상된 반복문
    s.o.p(변수명);
}
ArrayList(Integer) a = new ArrayList<Integer> ();
for(int i = 0; i < a.size(); i++) {
    s.o.p(a.get(i));
}
```

```java
  HashSet<String> set = new HashSet<String>();
  HashSet set = new HashSet();
  set.add(1);
  set.add(2);
  set.add("aaa");
  set.remove(1);
  for(int i = 0; i < set.size(); i++) {
      s.o.p(set.xxx(i)); ----> error
  }
  for(Object one : set) {
      s.o.p(one); ===>
  }
```



 #### Map 컬렉션

> 데이터 = ( key, 값 )

**HashMap**

KEY 는 중복 X, VALUE 는 중복 가능

```java
HashMap map = new HashMap();
HashMap<> map = new HashMap<>();
HashMap<String, Integer> map = new HashMap<String, Integer>();
```

- 저장 : put(KEY. VALUE)

  ```java
  map.put("TITLE", "자바");
  map.put("DAYS", 30);
  map.put("SCORE", 'A');
  ```

- 수정 : 앞에 등록된 적이 있다면 수정

  ```java0
  map.put("TITLE", "SQL");
  ```

- 삭제

  ```java
  map.remove(key값);
  ```

- 조회

  ```java
  for(int i = 0; i < map.size(); i++) {
      map.get(key값);
  }
  ```

  

---

## 13장. GENERIC

> ```java
> ArrayList<E> i = new ArrayList<E>();
> //동적크기 + 1가지 타입 저장
> ```

- 리스트 저장 1개 원소 = 데이터 = ELEMENT 타입 클래스명

- 컴파일러에게 미리 타입 알려줌

- 고정 타입 데이터만 저장

- 동적 타입 저장 X

- 컬렉션 프레임워크 내부 타입 한정 활용

- 사용자 정의

  ```java
  class Apple {}
  class Paper {}
  class Box {
      Object contensts; //어떤 타입을 줄지 모를때 Object 타입이 적합
  }
  // 불편, 개선 ==> generics
  ```

  

















