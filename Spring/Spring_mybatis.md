#  Spring_mybatis

---

## Review

- ResponseBody-ajax ---> return json객체 { ... }
- http 요청 클라이언트 방식
  - get  ---> @RequestMapping(value="/...", method=RequestMethod.GET)
  - POST  ---> @RequestMapping(value="/...", method=RequestMethod.POST) 

- resources 폴더
  - CLASSPATH(spring/main/java)  /  webapp - views, resources(mvc 무관 실행)

- 비지니스로직 + mvc

  - web.xml : classpath:annotation/service/컨택스트명/xxx.xml (참조하는 xml)
  - xxxController  ---> @Autowired

- 파일 업로드 기능

  - < input type=file  ---> 파일 선택 열기창
  - =====
  - 서버 파일 전송 기능 - spring api추가
  - pom.xml  ---> mvnrepository 에서 스프링 api 다운
    - 라이브러리, 이름, 버전 선택  /  < dependency > 태그 사용
    - commons-fileupload, io 다운
  - servlet-context.xml
    - < beans id = "multipartResolver" 태그 사용해서 라이브러리 사용

- ajax와 json

  - 웹 접속 기기 다양  ---> 화면에 적절한 내용이 필요
  - 기본 화면구성 + 동적 내용 변경
  - xml  ---> 초기 비동기 통신신 전달 데이터 형태 초기
  - 비동기화 통신 방식(asynchronous)  ===> ajax + json(java script object notation)

- spring xml 파일들

  | xml                 | 내용                                                        |
  | ------------------- | ----------------------------------------------------------- |
  | pom.xml             | 스프링 라이브러리 다운로드, 버전 설정                       |
  | web.xml             | src/main/webapp/WEB-INF  웹관련설정  ===> DispatcherServlet |
  | (스프링 시작 이전)  | encodimng ---> utf-8 설정                                   |
  |                     | 스프링 전달 추가 설정 xml 정보                              |
  | servlet-context.xml | WEB-INF/spring/appServlet  스프링 설정                      |
  |                     | view 경로와 확장자 설정 (default : jsp)                     |
  |                     | 웹 정적 요소들 - html css js image 경로                     |
  |                     | < context:component-scan                                    |
  | 추가 설정 xml       | member.xml + ...                                            |



---



## My Batis

> | Spring                         | Mybatis     |
> | ------------------------------ | ----------- |
> | java                           | java        |
> | 통합 기능                      | db연동 기능 |
> | ioc/di + mvc + aop + db연동 등 |             |
>
> | jdk / jdbc          | spring jdbc      | Mybatis                               |
> | ------------------- | ---------------- | ------------------------------------- |
> | java.sql.*          | 스프링 제공 jdbc | jdbc 프레임워크                       |
> | 코드 반복 심하다    |                  | xml 별도설정(sql 문장 자바 코드 제거) |
> | 수동 선택 연결 유지 |                  | connectionpool (자동생성-관리)        |
> |                     |                  | sql 조회 결과를 정한 타입으로 설정    |
>
> - 초창기 ibatis라는 이름으로 시작
> - mybatis.jar + oracle db jdbc driver  //  + spring-mybatis.jar spring-jdbc.jar



### Config. xml

- DB연결 정의

| 객체 type 설정         | < typeAlias                 |
| ---------------------- | --------------------------- |
| 연결할 DataSource 설정 | < environment 다중환결 설정 |
| mapper 파일 설정       | < mapper                    |



### Sql-mapping.xml

| select | id="자바 sql 실행 식별자" resultType="1개 레코드 타입"  ---> 필수 |
| ------ | ------------------------------------------------------------ |
|        | parameterType = " 자바에서 sql로 전달 데이터"                |
| insert | id = 필수  /   resultType 필요x                              |
| update | id = 필수  /  resultType 필요x                               |
| delete | id = 필수  /  resultType 필요x                               |

| resultType                             | xxxVO -> int / String             |
| -------------------------------------- | --------------------------------- |
| parameterType / 한가지 변수만 사용가능 | xxxVO -> int / String / **int[]** |

