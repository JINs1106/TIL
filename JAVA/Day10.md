# Day10. 네트워크 기능



---

## Review

### java.io 패키지의 클래스들

> 표준 장치(= 물리적장치) = 키보드 입력 모니터 출력 / 파일 등의 입출력 기능 / 파일 시스템 정보 추출

| System.in  --> java.io.InputStream 타입               |      |
| ----------------------------------------------------- | ---- |
| System.in.read()  --> 키보드 입력  - 1byte 영문, 숫자 |      |
| java.util.Scanner                                     |      |
| Scanner s = new Scanner(System.in)                    |      |
| s.nextInt(); s.nextDouble(); s.next();                |      |

- 파일

  | java.io.FileReader / FileInputStream (입력) | java.io.FileWriter / OutputStream (출력) | java.io.File         |
  | ------------------------------------------- | ---------------------------------------- | -------------------- |
  | 한글 깨지거나 제대로거나                    |                                          | 파일 시스템 정보제공 |
  | windows 파일 출력 - a.txt                   |                                          | 입출력 메소드 없다   |
  | read(); close();                            | write(char c[]) / (String); close();     | window 탐색기 기능   |

- 보조스트림  ==> Scanner로 구현 가능

  - InputStreamReader : 1byte -> 2byte (한글)    /// OutputStream
  - BufferReader : 입력속도 향상(내부메모리 기억 readLines(); )  /// BufferWriter
  - DataInputStream : 자바 데이터 타입 변환 입력   /// DataOutputStream

  ```java
  System.in.read();
  Scanner s = new Scanner(System.in);
  // 입력데이터 원본(= 출발지) --> Scanner 변환(보조스트림)
  ```



> java.io.50여개 클래스 --> 복잡 --> 여러개 클래스 기능 --> jdk 1.5 Scanner



---



## 18장. 네트워크 기능

> 물리적 통신 회선으로 연결된 다른 컴퓨터와의 입출력

- ip adress : 연결 컴퓨터 식별 번호 / 인터넷상 모든 컴퓨터 고유한 식별 번호 (중복X)
  - ipv4 = ip(256 * 256 * 256 * 256)
  - ipv6 = ip + port
  - 클라이언트의 요청과 서버의 처리



### java.net.InetAddress 클래스

- IP확인



### 통신

| tcp 통신 방식 - 전화방식             | udp 통신방식 - 우편방식            |
| ------------------------------------ | ---------------------------------- |
| java.net.ServerSocket                | java.net.DatagramSocket            |
| java.net. Socket                     | java.net.DatagramPacket            |
| 연결 - 데이터 - 연결해제 / 상호 전달 | 대량 메시지 동시 발송 / 답변보장 X |

- 이미 구현 공 네트워크 방식
  - 인터넷 = 웹 = http / 파일 전송 특화 --> FTP / 원격 접속 = telnet
  - http://www.xxx.xxx
  - protocol = 통신 컴퓨터 약속 규칙

| 서버역할 프로그램                         | 클라이언트프로그램                  |
| ----------------------------------------- | ----------------------------------- |
| 1. 서버 시작한다.(port)                   | 1. 서버 접속 요청(ip + port 필요)   |
| 3. 클라이언트 요청 승인한다.              | 4. 서버로 로그인 아이디와 암호 전송 |
| 5. 클라이언트가 전송한 내역을 입력 / 처리 |                                     |
| 6. 처리결과를 클라이언트에게 전송         | 7. 서버가 전송한 결과를 이용        |
| 9. 클라이언트와 접속 해제                 | 8. 서버와의  접속 해제              |
| 바이트 배열 -> String                     | String -> 바이트배열 변환 후        |

```java
// 서버
ServerSocket ss =  new ServerSocket(9999);
Socket s = ss.accept);
byte[] id_byte = new byte[100]
InputStream is = s.getInputStream();
???  --> is.read(id_byte_server);  //5번 구현
String id  = new Stting(id_byte_ server); // "multi"
OutputStream os = s.getOutputStream();  // 6번 구현
os.write(....);
s.close();
```

```java
// 클라이언트
Socket s = nwrSocket(ip, 9999)
String id = "멀티";  // bytep[] id_byte = id.getBytes();
OutputStream os = s.getOutputStream();  // 4번 구현
os.write(....);
s.close();
```

- java.net.ConnectExceprtion : 서버 시작 X  ==> 서버 먼저 시작
- java.net.BindException : 이미 사용중  ==> 서버가 이미 시작된 상태에서 또 실행(포트 중복)



### 스레드 병렬 처리

- 채팅 서버 1개 / 채팅 클라이언트 여러개 : 스레드, [  awt, swing, java fx : GUI 구성 ]



### UDP 네트워킹

> 대량의 메시지 동시 발송(회신보장X), 신뢰성 유의





> DB와 자바의 연동 ==> jdbc  /  SQL 문법
