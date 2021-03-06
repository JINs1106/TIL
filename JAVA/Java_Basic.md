# Java_Basic

---



## Basic

- 기계어 : 컴퓨터가 처리하는 0과 1로 이루어진 코드

  - 소스 파일 = 프로그램밍 언어로 작성한 파일

  - 컴파일 = 소스 파일을 기계어 파일로 번역
  
    
  
- 환경변수 : 운영체제가 실행하는 데 필요한 정보를 제공해주는 변수

  - cmd나 터미널에서 Java 컴파일러와 실행 명령어 사용하기 위해 환경변수 등록 및 Path 환경 변수 수정 필요

- Java : 1995년 마이크로시스템즈 발표 언어로 웹, 다양한 어플개발의 핵심
  - 오라클이 라이센스 소유
  - **객체 지향 프로그램**(OOP)
  - 메모리 자동 정리 / 모든 운영체제 실행 가능 / 풍부한 라이브러리
  - **JDK**(Java Development Kit)
    - java로 개발시 필요 환경 및 도구 제공(컴파일러 역할)
    - Open JDK / Oracle JDK( + LTS : 장기지원서비스)



## Eclipse(이클립스)

> **IDE**(무료 오픈 소스 통합 개발 환경) : 프로젝트 생성, 자동 코드 완성, 디버깅 등 개발에 필요한 여러가지 기능을 통합적으로 제공



### Basic

- 워크스페이스 : 프로젝트 폴더가 저장, 개발 환경 정보와 관련된 메타 데이터(.metadata)가 동시 저장

- 퍼스팩티브(perspective) : 프로젝트 개발 시 유용하게 사용할 수 있는 view를 묶어 이름을 붙여 놓은 것

  -  java, javaEE, git 등등

- 뷰(view) : 이클립스 내부에서 사용되는 작은 창(console view)

- 바이트 코드 파일(.class) ---> **JVM** 로 기계어로 번역 실행

- 자바 프로젝트 - src - package ---> 소스 파일  // 바이트 코드 파일 ===> bin 폴더 내부에 생성

  - 실행 : run as - java application ===> Console 창에서 실행 **OR** 명령프롬프트 창에서 실행

  

### 명령라인 실습

- Java workspace에서 cmd 실행 / dir(파일 목록), tree /f(파일 관계도)

- 컴파일

  ```cmd
  javac -d bin src/소스경로/*.java ---> 컴파일 실행
  ```

- 실행

  ```cmd
  java -cp bin sec03.exam01.Hello  ---> 자바파일 실행 (JDK8 이전)
  
  java -p bin -m chap01/sec03.exam01.Hello  ---> JDK11 이후 버전
  ```
  
  
  
### Module(모듈)
> 외부에서 재사용할 수 있는 패키지들의 묶음(다른 프로그램에서 사용 가능)
>
> 이클립스의 프로젝트는 **하나의 모듈**을 개발하는 것

- 모듈이 필요한 이유 : 패키지 보안, 최적의 런타임 이미지 위해(모듈별 데이터량이 필요하기에 필요한 모듈만 사용)

#### 의존하는 모듈

- 해당 모듈이 실행하기 위해 필요한 외부 모듈 (ex. java.lang, java.math, io, util......) // java.se 모듈

- 기본적으로 java.base 모듈만 사용 가능 / 다른 모듈 사용하기 위해 의존 모듈 등록

  ```java
  module chap01 {
      requires java.desktop;
      requires java.sql;
      /////
      requires java.se;
  }
  ```

#### 프로그램 소스 분석

- 패키지 선언
- 클래스 선언
- 메소드 선언

#### 주석

- 코드에 설명을 붙여 놓은 것
- //,  /* */, /** */





  

  

  





