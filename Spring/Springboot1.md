# Day 1

9/13 ~ 14 : spring boot + git hub

9/15 ~ 17 : 파이썬 + 프로젝트 전처리

9/23 ~ 24 : ai makers 스피커 + 라즈베리파이 연동


---

## Review

- Spring Boot 와 Legacy mvc project  비교
  - pom.xml 스프링 프레임워크 버전 설정 x, 부트에서 자동 설정
  - boot 에서는 @SpringBootApplication 이 설정 메인메소드가 존재
  - run-spring boot app로 실행
  - 내장 tomcat 서버는 Main 실행시 자동 시작  ---> port 번호 확인
  - boot 에는 web.xml이 존재x  --->SpringBootServletInitializer 클래스가 대신
  - tomcat 실행시 프로젝트 컨텍스트명은 / 이다
  - 리소스파일은 src/main/resources/static 폴더에 저장
  - resources/application.properties는 설정파일

---



## Spring Boot

 ### ajax 실행

- jackson-databind 라이브러리 : 별도 추가 x
- js 파일이나 image 파일 경로 올바른가 테스트



### file upload 실행

- < context: component-scan base-package=" upload " / >  ---> 기존 방식

  ===> @ComponentScan(basePackageClasses = ) annotation 사용 // main 메서드에 사용

  ** 일정 패키지만 component시 현재 패키지의 컨트롤러 인식x  ---> @Component-scan 사용 인식(현재 페이지 스캔)



### @Configuration

- 웹서버 != 웹클라이언트 폰 / 패드 / 노트북 등
- 웹브라우저 서버 url 입력 - 접속 - 서비스 - html 태그 응답
- 서버 폴더 접근제한  ---> static 폴더 내부로 제한  ===> 설정 변환 필요
- webmvcconfigurer 상속받아 사용
- < context path="내부경로" uri=" " 추가 or application.properties 에 설정



### mybatis 실행

| spring mvc                                                   | spring boot                           |
| ------------------------------------------------------------ | ------------------------------------- |
| pom.xml : 4개 dependency 연동                                | spring boot starter 항목 설정         |
|                                                              | jdbc api  /  oracle driver /  mybatis |
| spring-mybatis.xml : db연결 / mapping 파일정보               | application.properties 파일 설정      |
| mybatis-config.xml : 클래스의 alias 정보                     | 그대로 사용                           |
| sql-mapping.xml : sql 매핑                                   | 표현방법 수정이 필요(그대로 사용)     |
| web.xml  ---> spring-mybatis.xml 를 연동설정 등록            | x(불필요 - application.properties)    |
| servlet-context.xml  ---> < context component-scan + 경로 / api | @ComponentScan 사용  /  부트 내장     |



```java
@Mapper
// EmpDAO 클래스 ---> 인터페이스 변경
@Autowired
SqlSession session;
...
List<xx> emplist(); // xml에서 id 동일시 자동ㅎ
...
session.selectList("emplist");
session.selectOne;
...
```



```xml
<!-- sql-mapping.xml -->
<mapper namespace="xxx.EmpDAO"></mapper>
<select id="emplist" resultType=" " parameterType=" ">
...
</select>
```
