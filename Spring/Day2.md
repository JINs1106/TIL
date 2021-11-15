# Day 2



---

## Review

- Spring Framework 특징

  - 경량의 컨테이너(적은 라이브러리 <--> ejb기술)

  - pojo 클래스 사용(dao, vo, service 자바클래스)

  - framework = 반제품(틀) + 나머지(개발환경) ===> 완제품을 구성

  - ioc  /  di 기능으로 스프링은 객체를 생성

    - Inversion Of Controll
    - Dependency Injection
    - 생성자 통해 객체 주입 - 생성자 di

    ```java
    class B { }  /  class Main { B b1 = new B(); /  B b2 = new B(); }
    class A {
        A(B b1) {
            this.b1 = b1
        }
    }
    ```

    - setter 메소드 주입 - setter di

    ```java
    class Main {
        B b1 = new B();
    	B b2 = new B();
        A a1 = new A();
        a1.setB(b2);
    }
    ```

- annotation

  | ioc  /  di | @Component      |
  | ---------- | --------------- |
  |            | @Service        |
  |            | @Repository     |
  |            | @Autowired      |
  | mvc        | @RequestParam   |
  |            | @RequestMapping |
  |            | @ModelAttribute |
  |            | @Controller     |

  



---



## Spring



### Spring MVC

> 기본 필수 ioc  / di

- MVC 란? 웹서버 개발 형식. Model View Controll

  - 모델1 방식 - 흐름 복잡(구현은 편함..)

    - 수많은 jsp가 연결
    - 파일관계 분석이 어려워짐

  - 모델2 방식 = servlet + jsp 구조

    - servlet - 클라이언트 요청 - 분석 - 자바 로직 처리(dao호출)  /  Controller 역할
    - dao, vo - 실제 처리 결과를 생성, 저장  /  Model 역할

    - jsp  /  View 역할

  

#### MVC 구현

- Spring MVC  ---> 강제화. first controller 구현

- dynamic web project로 구현

  | DispatcherServlet | 클라이언트 모든 요청 집중("/") |
  | ----------------- | ------------------------------ |
  |                   | 요청 가장 먼저받아서 view 이동 |
  | HandlerMapping    | 특정 url 컨트롤러 매핑 정보    |
  |                   | hello.spring-new AController() |
  | HelloController   | 특정 url  - model, view 설정   |
  | hello.jsp         | 응답                           |



#### spring mvc

- 스프링 프로젝트 폴더 구조 다르다

| DispatcherServlet   | x-spring api                                                 |
| ------------------- | ------------------------------------------------------------ |
| HandlerMapping      | x-spring api                                                 |
| Controller          | x-spring api                                                 |
| HelloController     | src/main/java                                                |
| hello.jsp           | src/main/webapp/WEB-INF/wiews                                |
| dao, vo             | src/main/java                                                |
| spring mvc 설정 xml | src/mail/webapp/WEB-INF/Spring/appServlet/servlet-context.xml |

- annotation

| mvc  | @RequestParam                    |
| ---- | -------------------------------- |
|      | @RequestMapping - 메소드 위 선언 |
|      | @ModelAttribute                  |
|      | @Controller - 컨트롤러 클래스    |

- 컨트롤러 메소드의 매개변수 자유롭다

  | 서블릿 api            | HttpSession 그대로 사용                                      |
  | --------------------- | ------------------------------------------------------------ |
  | 자바 데이터 타입 변수 | 요청 파라미터 이름과 동일 이름 변수 자동 저장(타입변환 자동) |
  |                       | @RequestParam("요청파라미터이름")                            |
  | 자바 객체             | @ModelAttribute("jsp이름" ) loginVO                          |

- spring mvc

  | web.xml             | "/" - DispatcherServlet |
  | ------------------- | ----------------------- |
  |                     | 한글 인코딩 필요        |
  | servlet-context.xml |                         |
  |                     |                         |

  













