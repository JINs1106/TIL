# Day 5



---

## Review

- spring
  - pom.xml
    - 자바 객체를 자동으로 json으로 변환해주는 api가 필요
    - < dependency > 로 설정
  - $.ajax  /  @ResponseBody
    - $.ajax( { url: "" ,  data, type, dataType, success})
    - ResponseBody는 메소드 위에 사용
  - 문자열을 json 객체 형변환 ===> JSON.parse()
  - json을 문자열로 형변환 ===> JSON.stringfy()

- mybatis
  - xml 설정 ---> spl 문장을 자바 코드 제거하고 xml 별도 설정
  - connectionpool 자동 생성. 관리
  - 반복코드x
  - sql 조회  결과를 다양한 타입으로 조회 가능
  - 다양한 태그
    - < select id=" " resultType= " " parameterType= " " >
    - < insert > , < update >, < delete > 등
  - < typeAliases > < typeAlias type= " " alias= " "  ---> 객체의 타입 설정
  - sql-mapping.xml ---> sql 코드 제공
    - forEach 다른 태그 포함. 반복



---



## Mybatis

> web.xml에 스프링 전달 추가 설정  ---> 추가설정xml을 등록



### Spring 연동

| xml                                | 내용                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| mybatis-config.xml                 | 데이터 소스 생성, 타입, 매퍼 파일                            |
| mapper.xml                         | sql 정의                                                     |
| **스프링+마이바티스 연동설정 xml** | spring bean 설정 파일 / ioc, di 설정                         |
| servlet-context.xml                | spring mvc 설정                                              |
| web.xml                            | 웹서버 설정                                                  |
| pom.xml                            | 4개 라이브러리 jar // mybatis, ojdbc8, mybatis-spring, spring-jdbc |

- DataSource 생성  ---> mybatis-config.xml 설정 삭제
- SqlSessionFactory 생성 ---> mybatis-config.xml, sql-mapping.xml
- **SqlSessionTemplate 생성**

- @(annotation) 사용 위해  /  < context:component-scan 사용







## Spring Boot



### Spring 과의 차이

- pom.xml 에 스프링 프레임 워크 버전 설정 x
- 메인메소드가 존재
- tomcat서버의 자동실행. 포트 충돌시 properties에서 포트 변경 필요
- jsp가 기본 view가 아니다. 추가 설정 필요
- applications.properties는 스프링 설정 xml 파일들을 대신하는 설정 파일이다.
- web.xml이 존재x ---> SpringBootServletInitializer 클래스가 대신
- tomcat 시작되면 현재 부트 프로젝트 컨택스트명은 / 이다
  - **http://ip:port/...**

































