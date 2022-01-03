# HTTP 웹 기본 지식

> 참고자료 : 김영한 - 모든 개발자를 위한 HTTP 웹 기본지식

---

# 인터넷 네트워크

- 인터넷 프로토콜 스택의 4계층
  ![image](https://user-images.githubusercontent.com/87891581/147866395-ef10da8b-819c-43d1-ab6e-1734e34b11a4.png)
- 애플리케이션 계층 - HTTP, FTP
- 전송 계층 - TCP, UDP
- 인터넷 계층 - TP
- 네트워크 인터페이스 계층

## 1. 인터넷 통신

- 두 컴퓨터가 정보를 주고 받으려면 서로 연결이 되어 있어야 한다.
- 인터넷을 통해 서로 연결될 수 있다.
- 정보를 주고 받으려면 도착지 위치와 같은 부가적인 정보가 필요하다.

## 2. IP(Internet Protocol)

- 지정한 IP 주소(IP Address)에 데이터 전달
- 패킷(Packet)이라는 통신 단위로 데이터 전달
- **IP 패킷**

![image](https://user-images.githubusercontent.com/87891581/147866287-cf9593db-7932-43d7-9edd-c301e02123ce.png)

### 한계점

- 비연결성
  - 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷을 전송한다.
- 비신뢰성
  - 중간에 패킷이 유실될 수 있다.
  - 패킷이 순서가 바뀔 수 있다.
- 프로그램 구분
  - 같은 IP를 사용하는 서버에서 통신하는 애플리케이션을 구분할 수 없다.

## 3. TCP, UDP

### 1) TCP

- 전송 제어 프로토콜(Transmission Control Protocol)
- 신뢰할 수 있는 프로토콜
- 현재는 대부분 TCP 사용
- **TCP/IP 패킷**
  ![image](https://user-images.githubusercontent.com/87891581/147866498-90715019-50e8-4f3b-b3f3-60b7e731d225.png)

#### 특징

- 연결 지향
  - TCP 3 way handshack(가상 연결)
    1. 클라이언트가 SYN(접속 요청)을 보냄
    2. 서버가 SYN + ACK(요청 수락)를 보냄
    3. 클라이언트가 ACK을 보냄(데이터도 함께 전송 가능)
- 데이터 전달 보증
  - 서버가 데이터를 받으면 받았다는 신호를 보냄
- 순서 보장
  - 순서가 잘못되면, 서버는 잘못된 부분부터 재전송을 요청

### 2) UDP

- 사용자 데이터그램 프로토콜(User Datagram Protocol)
- 애플리케이션에서 추가 작업 필요
- 성능 향상을 위해 기능이 거의 없는 UDP의 사용빈도 증가

#### 특징

- 연결 지향 - TCP 3 way handshake X
- 데이터 전달 보증 X
- 순서 보장 X
- 즉, IP에 PORT, 체크섬 정도만 추가되었다.

## 4. PORT

- 같은 IP 내에서 프로세스 구분 가능
  - 아파트 동 -> IP, 호수 -> PORT
- 0 ~ 65535 할당 가능
- 0 ~ 1023 잘 알려진 포트, 사용하지 않는 것이 좋다.
  - FTP - 20, 21
  - TELNET - 23
  - HTTP - 80
  - HTTPS - 443

## 5. DNS

- 도메인 네임 시스템(Domain name System)
- 도메인 명을 IP 주소로 변환
  1. 클라이언트가 도메인 명(ex. google.com)으로 요청
  2. DNS 서버에서 도메인 명과 대칭과는 IP 주소 응답
  3. 클라이언트는 해당 IP 주소로 접속
- IP는 기억하기 어렵고, 변경될 수 있기 때문에 사용한다.

---

# URI, URL, URN

## 1. URI

- Uniform Resource Identifier
  - Uniform : 리소스를 식별하는 통일된 방식
  - Resource : 자원, URI로 식별할 수 있는 모든 것(제한 없음)
  - Identifier : 다른 항목과 구분하는데 필요한 정보
- URI는 로케이터(Locator), 이름(Name)또는 둘다 추가로 분류될 수 있다.
  ![image](https://user-images.githubusercontent.com/87891581/147871549-b5e50fdc-4e0f-46d3-aa44-f413560f6394.png)

## 2. URL과 URN

![image](https://user-images.githubusercontent.com/87891581/147871575-1fbe4958-30f3-45f8-b08d-91c6ff0a46d5.png)

- URL - Locator : 리소스가 있는 위치 지정
- URN - Name : 리소스에 이름을 부여
  - 예 urn:isbn:896077731
- 위치는 변할 수 있지만, 이름은 변하지 않는다.
- URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음

## 3. URL 문법

`scheme://[userinfo@]host[:port][/path][?query][#fragment]`
`• https://www.google.com:443/search?q=hello&hl=ko`

- scheme
  - 주로 프로토콜 사용
  - 프로토콜 : 어떤 방식으로 자원에 접근할 것이가 하는 약속 규칙. 예) http, https, ftp 등
    - https는 http에 보안 추가(HTTP Secure)
- userinfo
  - URL에 사용자 정보를 보항해서 인증
  - 거의 사용하지 않음
- host
  - 호스트명
  - 도메인명 또는 IP 주소를 직접 사용 가능
- PORT
  - 포트
  - 접속 포트
  - 일반적으로 생략.
  - http는 80포트, https는 443 포트를 주로 사용.
- path
  - 리소스 경로(path)
  - 계층적 구조
  - 예
    - /home/file1.jpg
    - /members
- query
  - key=value 형태
  - ?로 시작, &로 추가 가능
    - 예) ?keyA = valueA&keyB=valueB
  - query parameter, query string등으로 불림.
  - 문자 형태
- fragment
  - html 내부 북마크 등에 사용
  - 서버에 전송하는 정보 아님

---

# 웹 브라우저 요청 흐름

![image](https://user-images.githubusercontent.com/87891581/147872285-1d70ff36-74e9-4f2c-843f-56557f0fac2c.png)

1. 웹 브라우저가 HTTP 메시지 생성
2. SOCKET 라이브러리를 통해 전달

- A : TCP/IP 연결 - 3way handshake 이용
- B : 데이터 전달

3. TCP/IP 패킷 생성, HTTP 메시지 포함

---

# HTTP

- HyperText Transfer Protocol
- HTTP 메시지에 모든 것을 전송
  - HTML, TEXT
  - IMAGE, 음성, 영상, 파일
  - JSON, XML (API)
  - 거의 모든 형태의 데이터 전송 가능
- 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용

## 1. 기반 프로토콜

- TCP : HTTP/1.1(가장 많이 사용), HTTP/2
- UDP : HTTP/3

## 2. 특징

### (1) 클라이언트 서버 구조

- Request Response 구조
- 클라이언트는 서버에 요청을 보내고, 응답을 대기
- 서버가 요청에 대한 결과를 만들어서 응답

### (2) 무상태 프로토콜(스테이스리스)

- 서버가 클라이언트의 상태를 보존하지 않는다.
  - 중간에 서버가 변경되어도 요청과 응답에 지장이 없다.
- 장점 : 서버 확장성 높음(스케일 아웃)
- 단점 : 클라이언트가 추가 데이터 전송

#### 실무 한계

- 모든 것을 무상태로 설계할 수 있는 경우도 있고 없는 경우도 있다.
  - 무상태 : 로그인이 필요없는 단순한 서비스 소개 화면
  - 상태유지 : 로그인
- 로그인 한 사용자의 경우 로그인 했다는 상태를 서버에 유지

### (3) 비연결성

### (4) HTTP 메시지

### (5) 단순하고 확장 가능
