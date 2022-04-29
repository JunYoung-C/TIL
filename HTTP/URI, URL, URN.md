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