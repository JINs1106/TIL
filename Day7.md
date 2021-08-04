<h1>
    Day7. 예외처리, 자바 라이브러리
</h1>


---


<h2>
    Day6 Review
</h2>



<h3>
    abstact
</h3>

- 상속과 오버라이딩 의무

  ```java
  abstract class A {
      abastract void m();
      void m2() { s.o.p("m2"); }
  }
  ```

- 객체 생성 불가능

  ```java
  A a1 = new A(); //객체생성 불가
  ```



<h3>
    인터페이스
</h3>

1. 클래스 단일 상속(**extends** 1개 클래스 정의)
2. 모든 메소드 **public abstract** 선언 약속 -> 오버라이딩 구현 정의 => **자동 선언**

3. ***객체 생성 불가능***

4. 다중 상속

   ``` java
   class A implements I1, I2, ... { }
   ```


5. **public static final** 필드 변수 선언 약속

   

<h3>
       예외처리
</h3>

> (실행 조건에 따라) 발생 오동작. 프로그래머 프로그램 수준의 제어 => **예외**

 - 예외상황은 다양. 예외 클래스 존재 = **class xxxxxException**

 - 예외 발생시, 오류 메시지 출력 -> 중단

 - **try-catch** 구문 추가하면 예외 발생시 catch 블럭 수행 후 흐름 변경

   ```jav
   trt {
     ....
   } catch {
     ....
   } 
   ```
   
- **finally** 구문 : **try-catch**구문 마지막에 사용하여 특정 문장 종료.

  - 시스템 프로그램 공유자원(파일, DB, 네트워크 회선 등) 사용 후 종료가  필요하기 때문

---

  

<h2>
    throws
</h2>

> 예외 떠 넘기기

- throws 단독 사용 -> 메소드 선언부. 예외클래스명



> 자바 라이브러리에는 무수한 예외 클래스 정의 + 사용자 정의 예외 클래스



-------



