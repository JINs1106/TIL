# Java_xxxput

---

## Review



### java.util.컬랙션프레임워크 클래스

> 여러개 객체 저장 / 동일타입이거나 서로 다른 타입 / 갯수 정적 동적
>
> | ArrayaList                 | HashSet                      | HashMap                      |
> | -------------------------- | ---------------------------- | ---------------------------- |
> | 저장 순서대로 관리         | 저장 순서 없다               | 저장 순서 없다               |
> | index - 0 부터             | index 없음                   | key는 data 구분 식별자       |
> | 동일 객체 여러번 저장 가능 | 동일 객체 여러번 저장 불가능 | 동일 key  여러번 저장 불가능 |
> | data = value               | data = value                 | data = key + value           |



### GENERIC

> jdk 1.0.1.1
>
> jdk 1.2  ->  새로운 api 대량 추가 1.3, 1.4
>
> jdk 1.5  -> 새로운 문법 도입 1.6 ,1.7
>
> jdk 1.8 (jdk 8)  -> 새로운 문법, api, 내부 동작 원리, generic ~ 13

-  여러개 객체 저장 : 저장 객체 동적 변경 장점 / Object 타입 자동 형변화 간주

- 저장 객체 타입 복원 명시적형변환 후에 필드변수 사용(**단점**)

- 1개 객체 저장 필요 --> 컴파일러 미리 저장 객체 타입 정하여 알려준다. 명시적형변환 없다.

  ```java
  ArrayList list = new ArrayList(); //여러 타입 객체 저장
  list.add(Object o);
  list.get(0); // Object o
  ArrayList<String> list2 = new ArrayList< String>(); //String 객체 저장
  list2.add(String o);
  list2.get(String 0) // String o
  ```

- ArrayList<E> list2 = new ArrayLIst<E>(); ==> String 객체 저장

  - 리스트 내 1개 데이터 = 원소 = ELEMENT
  
  ```java
  class UserClass<T> {
      T id; //학번, 사번, 주민번호 등
      ////
  }
  UserClass<String> user1 = new UserClass<String>();
  usrt.id = "10000-200"
  UserClass<Integer> user2 = new UserClass<Integer>();
  user2.id = 100200
  ```
  
  

---



## 18장. io 기반 입출력 및 네트워킹

>  (입력)  --> Java 프로그램 --> (출력)
>
> **입출력** : 자바 프로그램 외부 환경으로부터 데이터 전달
>
> **java.sql.**(DB입출력), **java.net*.*, *** java.io.***



### java.io. 50여개 클래스

> |                     | 입력 용도 클래스                      | 출력 용도 클래스                |
> | ------------------- | ------------------------------------- | ------------------------------- |
> | 2byte씩(문자단위)   | Reader(FIleReader, BufferReader)      | Writer                          |
> | 1byte씩(바이트단위) | InputStream                           | OutputStream                    |
> | File 클래스         | 입출력 기능 X, 파일이나 디렉토리 크기 | 리스트 목록, 파일저장경로... 등 |
>
> 이미지 파일 - a.png 파일 - 자바 입력 - (이미지 -> 이진수 차례로 입력)  --> 출력
>
> 문자파일 - a.txt, b.doc, c.hwp  - 자바 입력
>
> ascii code(알파벳), 1byte --> unicode(전세계 모든 문자) 표현, 2byte
>
> ```java
> class Reader();
> calss FileReader extends Reader { 자동포함 + 오버라이딩 메소드 + 추가 메소드 }
> class InputStream();
> calss FileputStream extends InputStream { 자동포함 + 오버라이딩 메소드 + 추가 메소드 }
> ```

#### InputStream / Reader

- 입력 공통 / 1바이트씩 / 2바이트씩

  | read()                                                       | 입력(1바이트씩 / 2바이트씩)                                  |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | close()                                                      | 입력 종료 파일 반납 문장.  try-catch-finally                 |
  | InputStream                                                  | Reader                                                       |
  | read(byte b[]);  --> 1바이트씩 입력 문자데이터를 b 배열로 저장 | read(char b[]);  --> 2바이트씩 입력 문자데이터를 b 배열로 저장 |

#### OutputStream / Writer

- 출력 공통 / 1바이트씩 / 2바이트씩

  | write(int i)                                      | 출력(1바이트씩 / 2바이트씩)                          |
  | ------------------------------------------------- | ---------------------------------------------------- |
  | close                                             | 출력 종료 파일 반납 문장 -> finally 작성 문장        |
  | OutputStream                                      | Writer                                               |
  | write(byte b[]); --> byte 배열 b 저장한 내용 출력 | write(char c[]); --> char 배열  c 저장한 내용을 출력 |
  |                                                   | write(String s) --> String s 저장한 내용을 출력      |

#### 키보드 입력 / 모니터 출력

> =  표준 입력 / 표준 출력

- System.in.read() : InputStream 하위.  --> 1바이트만 표현 가능 / 데이터타입 변환 불가능

  - **java.util.Scanner  클래스 ** -->  키보드 입력 데이터를 자바 데이터타입 변환 입력 역활

    ```java
    // 생성자
    Scanner s = new Scanner(System.in);
    // 메소드
    s.nextInt() ==> int, 정수 타입 변환 입력
    s.nextDouble() ==> double d
    s.nextBoolean ==> boolean b
    s.next() ==> String s1
    s.nextLine() ==> String s2
    ```

- System.out.print()

  - System 클래스 : java.lang 패키지. 자바 실행 컴퓨터 정보 제공 클래스

- System.out 변수 : 자바 실행 컴퓨터의 모니터 장치 변수. java.io.PrintStream 타입 선언(OutputStream 하위)

- System.out 메소드 : java.io.PrintStream(write(), close()) 클래스 포함.
  - System.out.print()/println();

#### 파일 입출력

> File : 입출력 기능 X, windows 탐색기 기능. 길이. 출력가능 파일 형태 판단 (보조기능)
>
> FileInputStream / FileOutputStream : 1바이트 파일 입출력
>
> FileReader / FileWriter : 2바이트 파일 입출력

- File

  - 파일과 폴더 = 파일 시스템 = 모든 os 파일 시스템 관리

  - 생성자 / 메소드

    ```java
    File f = new File("a.txt"); // workspace/프로젝트(현재폴더) // 상대경로
    File f = new File("c:/test/a.txt")  // 절대경로
    File f = new File("c:/test") // 확장자 X, 파일인지 디렉토리 인지 구분 X
    File f = new File(".") // 상대경로. (기준 폴더)
    File f = new File("..") // 상대경로 (상위폴더)
    ```

    ```java
    f.canRead(). f.canWrite() // 입력가능 (window 파일 기본 입력 / 출력가능
    f.length()  --> byte 단위[]
    f.lastModifide() ==> 파일 최근 수정시각 // 1/10000초
    f.getxxxxpate();
    File f = new File("e:/test/a.txt")
    f.exists  ===> false
    ```

- 파일입력

  ```java
  FileInputStream fi = new FileInputStream("a.jpg");
  while(true) {
      int r = fi.read(); // 1바이트씩
      if(r == -1) { break; }
  }
  fi.close(); // 다른 프로그램이 a.txt 파일 사용하려고 대기중이였다면 사용가능
  
  FileReader fr = new FileReader("a.txt");
  while(true) {
      int r = fr.read();  //2바이트씩 문자열
  }
  fr.close();
  ```

- 파일출력

  ```java
  FileOutputStream fo = new FileOutputStream("a.jpg");
  a.jpg 존재하는 파일 --> 파일 원래 저장 내용 삭제 + 처음
      
  FileOutputStream fo = new FileOutputStream("a.jpg", true);
  a.jpg 존재하는 파일 --> 파일 원래 저장 내용 유지 + 처음
  
  FileOutputStream fo = new FileOutputStream("a.jpg", false);
  a.jpg 존재하지 않는 파일 --> 새롭게 파일 생성 + 츨력 시작
  
  fo.write(65);
  fo.write(66);
  ...
  fo.close(); // 다른 프로그램이 a.jpg 파일 사용하려고 대기중이였다면 사용가능
  
  FileWriter fw = new FileWriter("a.txt");
  a.txt 존재하는 파일 --> 파일 원래 저장 내용 삭제 + 처음
  fw.write(65);
  fw.write(66);
  fw.close();
  ```

  