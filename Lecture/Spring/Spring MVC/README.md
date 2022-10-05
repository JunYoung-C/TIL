# Spring MVC

## 목차

- [웹 서버 & 웹 애플리케이션 서버](#웹-서버--웹-애플리케이션-서버)
- [서블릿](#서블릿)
- [동시 요청 - 멀티 쓰레드](#동시-요청---멀티-쓰레드)
- [SSR & CSR](#ssr--csr)
- [redirect vs forward](#redirect-vs-forward)
- [Spring MVC](#spring-mvc-1)
- [HTTP 요청 데이터 조회 방법](#http-요청-데이터-조회-방법)
- [HTTP 응답 데이터를 만드는 방법](#http-응답-데이터를-만드는-방법)
- [@Controller vs @RestController](#controller-vs-restController)
- [HTTP 메시지 컨버터](#http-메시지-컨버터)
- [Thymeleaf](#thymeleaf)
- [메시지, 국제화](#메시지-국제화)
- [BindingResult](#bindingresult)
- [검증](#검증)
- [필터 & 인터셉터](#필터--인터셉터)
- [예외 처리와 오류 페이지](#예외-처리와-오류-페이지)
- [API 예외 처리](#api-예외-처리)
- [컨버터 & 포맷터](#컨버터--포맷터)
- [파일 업로드](#파일-업로드)

---

## 웹 서버 & 웹 애플리케이션 서버

### 1. 웹 서버(Web Server)

- HTTP 기반으로 동작
- 클라이언트가 요청하는 정적 리소스를 제공한다.
  - 정적 리소스 : 정적(파일) HTML, CSS, JS, 이미지, 영상
- 예) NGINX, APACHE

### 2. 웹 애플리케이션 서버(WAS, Web Application Server)

- HTTP 기반으로 동작
- 프로그램 코드를 실행해서 애플리케이션 로직 수행
    - 동적 HTML, HTTP API(JSON) 제공
- 웹 서버 기능 포함
- 예) 톰캣, Jetty, Undertow

### 3. 차이점

- 웹 서버는 정적 리소스(파일)를 제공하고, WAS는 애플리케이션 로직을 수행한다.
- 하지만 웹 서버가 프로그램 실행 기능을 포함하기도 하고, WAS가 웹 서버의 기능을 제공하기도 한다.
- WAS는 애플리케이션 코드를 실행하는데 특화되어 있다고 보면 된다.
- 자바는 서블릿 컨테이너 기능을 제공하면 WAS이다.
    - 하지만 서블릿 없이 자바 코드를 실행하는 서버 프레임워크도 있다.

### 4. 웹 시스템 구성

![image](https://user-images.githubusercontent.com/87891581/148025065-0830c2ff-6298-425a-964a-66015785b9f5.png)

- 정적 리소스는 웹 서버가 처리하고, 애플리케이션 로직같은 동적인 처리가 필요하면 웹 서버가 WAS에게 요청을 위임한다.
- WAS와 DB 만으로 시스템 구성이 가능하다. 하지만 아래와 같은 한계가 있다.
    - WAS가 너무 많은 역할을 담당, 서버 과부하 우려
    - 가장 비싼 애플리케이션 로직이 정적 리소스 때문에 수행이 어려울 수 있다.
    - WAS 장애시 오류 화면도 노출 불가능

#### 장점

- 효율적인 리소스 관리
    - 정적 리소스가 많이 사용되면 Web 서버 증설
    - 애플리케이션 리소스가 많이 사용되면 WAS 증설
- WAS, DB 장애시 Web 서버가 오류 화면 제공 가능
    - 정적 리소스만 제공하는 웹 서버는 잘 죽지 않음.

## 서블릿

- 클라이언트의 요청을 처리하고, 결과를 반환하는 자바 웹 프로그래밍 기술이다.
- 프론트엔드의 요청을 응답하기 위해서는 비즈니스 로직 실행 뿐만 아니라 TCP/IP 연결, HTTP 요청 메시지 파싱 및 내용 해석, 응답 메시지 작성 등의 여러 과정이 존재한다.
- 서블릿을 지원하는 WAS를 사용한다면, 개발자는 비즈니스 로직만 신경쓰면 된다.

### 1. HTTP 요청, 응답 흐름

![image](https://user-images.githubusercontent.com/87891581/148026205-20013787-499d-499e-98c3-350f5afaa8c4.png)

1. HTTP 요청
2. WAS는 Request, Response 객체를 새로 만들어서 URL에 맞는 서블릿 객체 호출
3. 개발자는 Request 객체(HttpServletRequest)에서 HTTP 요청 정보를 편리하게 꺼내서 사용
4. 개발자는 Response 객체(HttpServletResponse)에 HTTP 응답 정보를 편리하게 입력
5. WAS는 Response 객체에 담겨있는 내용으로 HTTP 응답 정보를 생성

### 2. 서블릿 컨테이너

![image](https://user-images.githubusercontent.com/87891581/148026414-160e27e4-7ee6-4b1f-8632-122396aa0994.png)

- 톰캣처럼 서블릿을 지원하는 WAS를 서블릿 컨테이너라고 한다.
- 서블릿 컨테이너는 서블릿 객체를 생성, 초기화, 호출, 종료하는 생명주기 관리
  - 서블릿 컨테이너 종료시 함께 종료
- 서블릿 객체는 싱글톤 관리
  - 요청마다 객체를 생성하는 것은 비효율적이다.
  - 모든 요청은 동일한 서블릿 객체 인스턴스에 접근
- JSP도 서블릿으로 변환되어서 사용
- 동시 요청을 위한 멀티 쓰레드 처리 지원

## 동시 요청 - 멀티 쓰레드

- 멀티 쓰레드 부분도 WAS가 처리해주기 때문에 편리하게 소스 코드를 개발할 수 있다.
- 멀티 쓰레드 환경이므로 싱글톤 객체(서블릿, 스프링 빈)는 주의해서 사용한다.

### 1. 쓰레드

- 애플리케이션 코드를 하나하나 순차적으로 실행하는 것이 쓰레드이다.
  - 한번에 하나의 코드 라인만 수행
- 자바 메인 메서드를 처음 실행하면 main이라는 이름의 쓰레드가 실행
- 쓰레드가 없다면 자바 애플리케이션 실행 불가능
- 하나의 요청을 하나의 쓰레드가 담당
  - 동시 처리가 필요하면 쓰레드를 추가로 생성

### 2. 동시 처리 해결방안

#### 1) 요청마다 쓰레드 생성

- 장점
  - 동시 요청 처리 가능
  - 리소스(CPU, 메모리)가 허용할 때 까지 처리 가능
  - 하나의 쓰레드가 지연되어도, 나머지 쓰레드는 정상 동작한다.
- 단점
  - 쓰레드는 생성 비용이 매우 비싸다
    - 고객 요청이 올 때마다 쓰레드를 생성하면, 응답 속도가 늦어진다.
  - 쓰레드는 컨텍스트 스위칭 비용이 발생한다.
    - CPU는 여러 쓰레드를 번갈아가면서 실행한다.
  - 쓰레드 생성에 제한이 없다.
    - 요청이 너무 많으면 CPU, 메모리 임계점을 넘어서 서버가 죽을 수 있다.

#### 2) 쓰레드 풀

- 특징
  - 필요한 쓰레드를 쓰레드 풀에 보관하고 관리
  - 쓰레드 풀에 생성 가능한 쓰레드의 최대치를 관리한다. 톰캣은 최대 200개 기본설정(변경 가능)
  - 최대 쓰레드가 모두 사용중이어서 쓰레드 풀에 쓰레드가 없다면, 기다리는 요청을 거절하거나 특정 숫자만큼만 대기하도록 설정할 수 있다.
- 장점
  - 쓰레드가 미리 생성되어 있으므로, 쓰레드를 생성하고 종료하는 비용(CPU)이 절약되고, 응답 시간이 빠르다.
  - 생성 가능한 최대치가 존재하므로, 너무 많은 요청이 들어와도 기존 요청은 안전하다.

#### 실무 팁

- WAS의 주요 튜닝 포인트는 최대 쓰레드 수이다.
- 너무 낮게 설정하면, 동시 요청이 많을 때 서버 리소스는 여유롭지만 응답이 지연된다.
- 너무 높게 설정하면, 동시 요청이 많을 때 CPU, 메모리 리소스 임계점 초과로 서버가 다운된다.
- 장애 발생시
  - 클라우드라면, 서버부터 늘리고 이후에 튜닝
  - 클라우드가 아니라면, 열심히 튜닝
- 적정 값은 애플리케이션 로직의 복잡도, CPU, 메모리, IO 리소스 상황에 따라 모두 다르다.
  - 최대한 실제 서비스와 유사하게 성능 테스트 시도
    - 툴 : 아파치 ab, 제이미터, nGrinder

## SSR & CSR
### SSR
- 서버 사이드 렌더링
- HTML 최종 결과를 서버에서 만들어서 웹 브라우저에 전달
- 주로 정적인 화면에 사용
- 관련 기술 : JSP, 타임리프

### CSR
- HTML 결과를 자바스크립트를 사용해 웹 브라우저에서 동적으로 생성해서 적용
- 주로 동적인 화면에 사용, 웹 환경을 마치 앱처럼 필요한 부분을 변경할 수 있음
- 관련 기술 : React, Vue.js

### 참고
- CSR, SSR을 동시에 지원하는 웹 프레임워크도 있다.
- SSR을 사용하더라도, 자바스크립트를 사용해서 화면 일부를 동적으로 변경 가능

## redirect vs forward
- 리다이렉트는 클라이언트로 요청에 대한 응답이 나갔다가, redirect 경로로 새로 요청하는 것이다.
  - 클라이언트가 인지할 수 있고, URL 경로도 실제로 변경된다.
- 포워드는 서블릿이나 JSP가 요청을 받은 후 다른 서블릿이나 JSP로 처리를 위임하는 것이다.
  - 서버 내부에서 일어나는 호출이기 때문에 클라이언트가 전혀 인지하지 못한다.

## Spring MVC
- 모델, 뷰, 컨트롤러로 이루어진 디자인 패턴이다.

### MVC 패턴
- 서블릿으로만 개발한다면, 뷰 화면을 위한 HTML을 만드는 작업이 자바 코드에 섞여서 지저분하고 복잡하다.
- HTML 작업을 편리하게 하기 위해 JSP를 사용하더라도, 코드가 복잡하고 유지보수가 어렵다는 문제는 유효하다.
- 이에 대한 해결 방안으로 비즈니즈 로직은 Controller로, 화면을 그리는 일은 View로 분리한 다음에 뷰가 필요한 데이터는 Model에 담아서 넘기는 방법이 등장하였다.
  - 이를 MVC 패턴이라고 한다.
  - 컨트롤러 : HTTP 요청을 받아서 파라미터를 검증하고, 비즈니스 로직을 실행한다. 그리고 뷰에 전달한 결과 데이터를 조회해서 모델에 담는다.
  - 모델 : 뷰에 출력할 데이터를 담아둔다.
  - 뷰 : 모델에 담겨있는 데이터를 사용해서 화면을 그리는 일에 집중한다.

### Front Controller 패턴
- 프론트 컨트롤러 서블릿 하나로 클라이언트 요청을 받고, 그에 맞는 컨트롤러를 찾아서 호출한다.
- 여러개의 서블릿으로 처리할 때 중복되는 코드를 하나로 묶어서 관리한다.
  - 중복되는 코드 : view로 포워드, view path의 prefix와 suffix
  - 간혹 사용하지 않는 request, response 객체도 존재한다.

### 어댑터 패턴
- 프론트 컨트롤러가 다양한 방식의 컨트롤러를 처리할 수 있게 만든다.
- 프론트 컨트롤러는 어댑터만 있다면 어떤 것이든 처리할 수 있기 때문에 컨트롤러 대신 핸들러라는 명칭을 사용한다.

### 동작 순서
![image](https://user-images.githubusercontent.com/87891581/168423149-d198ea93-908f-4c09-85b2-8b43e527f13c.png)
1. 핸들러 조회 
   - 클라이언트가 요청을 보내면, Dispatcher Servlet에서 요청 URL에 매핑된 핸들러(컨트롤러)를 조회한다.
2. 핸들러 어댑터 조회
   - 핸들러를 실행할 수 있는 핸들러 어댑터를 조회한다.
3. 핸들러 실행
   - 핸들러 어댑터를 실행하면 파라미터로 넘겨진 핸들러(컨트롤러)가 실행된다. 
4. ModelAndView 반환
   - 핸들러 어댑터는 핸들러가 반환하는 정보를 ModelAndView로 변환해서 반환한다. 
   - RestController라면 컨버터가 반환값을 HTTP 메시지 바디에 넣은 후 클라이언트에게 응답한다.
5. viewResolver 호출
   - 뷰 리졸버를 찾아 실행한다. 
6. View 반환
   - 뷰 리졸버는 뷰의 논리 이름을 물리 이름으로 바꾸고, 렌더링 역할을 담당하는 뷰 객체를 반환한다. 
7. 뷰 렌더링
   - 뷰에 Model을 보내 렌더링한 후 클라이언트에게 응답한다. 

## HTTP 요청 데이터 조회 방법
### 1. 쿼리 파라미터, HTML Form 데이터의 경우
**1) `@RequestParam`**
  - 요청 파라미터 조회에 사용된다.
  - 쿼리 파라미터, HTML Form 방식 둘다 파라미터 형식이 같으므로 구분없이 사용한다.
  - 파라미터 이름이 변수 이름과 같으면 name 속성은 생략해도 된다.
  - defaultValue 속성은 빈 문자의 경우에도 설정한 기본값이 적용된다.
  - 여러 파라미터를 조회할 수도 있다.
    - Map : 파라미터 값이 1개가 확실하다면 사용
    - MultiValueMap : 확실하지0 않을 경우 사용

**2) `@ModelAttribute`**
  - 객체 생성 후 요청 파라미터를 받아서 넣어주는 작업까지 해준다.
    - setter로 값을 넣는다.
  - 추가로 Model에 `@ModelAttribute`로 지정한 객체를 자동으로 넣어준다.
    - 이름은 `@ModelAttribute`의 name 속성을 사용한다.
    - name을 생략하면, 클래스 첫글자만 소문자로 변경해서 사용한다.

### 2. HTTP message body 데이터의 경우
- 주로 JSON 형식이며, HTML Form은 포함되지 않는다.
- 스프링 MVC 내부에서 HTTP 메시지 바디를 읽어서 문자나 객체로 변환해서 전달해준다.
  - `HttpMessageConverter` 사용

**1) `@RequestBody`**
- HTTP 메시지 바디 정보를 편리하게 조회할 수 있다.
- JSON 요청 -> HTTP 메시지 컨버터 -> 객체
  - `@ModelAttribute`와 유사한 방식으로 사용하면 된다.
- 헤더 정보가 필요하다면 `RequestEntity`, `HttpEntity`, `@RequestHeader` 중에서 하나를 사용한다.
- 생략 불가능하다.
  - 생략 시 `@ModelAttribute`가 적용된다.

## HTTP 응답 데이터를 만드는 방법
### 1. 정적 리소스
- 파일 변경 없이 그대로 제공한다.
- HTML, css, js 등이 해당된다.
- 스프링 부트는 클래스패스의 다음 디렉토리에 있는 정적 리소스를 제공한다.
  - `/static`, `/public`, `/resources`, `/META-INF/resources`
  - `src/main/resources/static/basic/hello.html`의 경우 `localhost:8080/basic/hello.html`로 요청한다.

### 2. 뷰 템플릿 사용
- 뷰 템플릿을 거쳐 HTML이 생성되고, 뷰가 응답을 만들어서 전달한다.
- 주로 HTML를 동적으로 생성하는 용도로 사용되며, 다른 것들도 가능하다.
- String을 반환하는 경우 `@ResponseBody`가 없다면, 뷰 리졸버가 실행되어서 뷰를 찾고 렌더링 한다.
- Void를 사용하는 경우 `@Controller`를 사용하고 HTTP 메시지 바디를 처리하는 파라미터가 없으면, 요청 URL을 참고해서 논리 뷰 이름으로 사용한다.
  - 권장하지 않는다.

### 3. HTTP 메시지 사용
> - HTML이나 뷰 템플릿을 사용해도 HTTP 응답 메시지 바디에 HTML 데이터가 담겨서 전달된다. 

- HTTP API를 제공하는 경우에는 데이터를 전달해야 한다.
  - HTTP 메시지 바디에 JSON과 같은 형식으로 데이터를 실어 보낸다.

**1) `@Responsebody`**
- `viewResolver` 대신, `HttpMessageConverter`가 동작하게 되어 HTTP message body에 직접 데이터가 입력된다.
- HTTP 응답 코드를 설정하려면, `ResponseEntity`를 사용하거나 `@ResponseStatus`를 붙여준다.
  - 조건에 따라 동적으로 변경하려면, `ResponseEntity`를 사용한다.
- 객체 -> HTTP 메시지 컨버터 -> JSON 요청

## @Controller vs @RestController
- `@Controller`는 반환 값이 String이면 뷰 이름으로 인식된다. 그래서 뷰를 찾고 뷰가 렌더링된다.
- `@RestController`는 `@ResponseBody`와 `@Controller`가 적용된 애노테이션이다.
- `@RestController`는 반환값으로 뷰를 찾는 것이 아니라, HTTP 메시지 바디에 바로 입력한다.

## HTTP 메시지 컨버터
- 문자나 객체 등의 데이터를 JSON으로 변환하는 작업을 한다.
  - `StringHttpMessageConver` : String 문자를 처리한다. 
  - `MappingJackson2HttpMessageConverter` : 객체나 HashMap을 처리한다. 요청 응답 둘 다 application/json
- 스프링 MVC는 다음의 경우에 HTTP 메시지 컨버터를 적용한다.
  - HTTP 요청 : `@RequestBody`, `HttpEntity(or RequestEntity)`
  - HTTP 응답 : `@ResponseBody`, `HttpEntity(or ResponseEntity)`

### HTTP 요청 데이터를 읽는 과정
1. `@RequestBody`나 `HttpEntity`를 사용하는 컨트롤러로 HTTP 요청이 들어온다.
2. 메시지 컨버터가 대상 클래스 타입과 `Content-Type`을 확인한다.
3. 조건을 만족하면, 데이터를 자바 코드로 변환한다.

### HTTP 응답 데이터를 생성하는 과정
1. 컨트롤러가 `@ResponseBody`나 `HttpEntity`를 사용한다.
2. 메시지 컨버터가 대상 클래스 타입과 HTTP 요청의 Accept 미디어 타입을 확인한다.
3. 조건을 만족하면, HTTP 응답 메시지 바디에 데이터를 생성한다.

### HTTP 메시지 컨버터 위치
![image](https://user-images.githubusercontent.com/87891581/168459636-bcea8712-e789-48db-917f-8c954d2ca610.png)
- 요청의 경우 : `@RequestBody`나 `HttpEntity`를 처리하는 `ArgumentResolver`가 HTTP 메시지 컨버터를 호출해서 필요한 객체를 생성한다.
- 응답의 경우 : `@ResponseBody`나 `HttpEntity`를 처리하는 `ReturnValueHandler`가 HTTP 메시지 컨버터를 호출해서 응답 결과를 만든다. 
#### ArgumentResolver
  - 애노테이션 기반의 컨트롤러는 매우 다양한 파라미터를 사용할 수 있다.
  - `ArgumentResolver`가 컨트롤러(핸들러)가 필요로 하는 다양한 파라미터의 값(객체)를 생성하고, 호출할 때 넘겨준다.
  - 직접 구현한 argumentResolver를, `WebMvcConfigurer`가 제공하는 `addArgumentResolvers()`로 등록할 수 있다.

#### ReturnValueHandler
  - `ArgumentResolver`와 반대로, 응답 값을 변환하고 처리한다.

## Thymeleaf
- 타임리프는 백엔드 서버에서 HTML을 동적으로 렌더링 하는 용도로 사용하는 뷰 템플릿이다.
- 타임리프는 스프링과 자연스럽게 통합되고, 스프링의 다양한 기능을 편리하게 사용할 수 있게 지원한다.
  - 스프링 빈 호출 지원
  - 편리한 폼 관리를 위한 추가 속성(`th:object`, `th:field`, `th:errors`, `th:errorclass`)
  - checkbox, radio button 등을 편리하게 사용할 수 있는 기능 지원
  - SpringEL 문법 통합
  - 스프링의 메시지, 국제화 기능의 편리한 통합
  - 스프링의 검증, 오류 처리 통합
  - 스프링의 변환 서비스 통합
- 타임리프는 순수 HTML을 그대로 유지하면서 뷰 템플릿도 사용할 수 있다.
  - 이를 네츄럴 템플릿이라고 부른다.
  - JSP를 포함함 다른 뷰 템플릿은 웹 브라우저에서 파일을 열면 정상적인 HTML 결과를 확인할 수 없다.
  - 타임리프로 작성된 파일을 웹 브라우저에서 열면정상적인 HTML 결과를 확인할 수 있다. 

## 메시지, 국제화
### 메시지 
- 화면을 구성하는 문자들을 하드코딩하지 않고, 한 곳에서 관리하도록 하는 기능을 메시지 기능이라고 한다.
  - 하드코딩 : 상수나 변수에 들어가는 값을 소스코드에 직접 쓰는 방식
- 메시지 관리 기능을 사용하려면, 스프링이 제공하는 `MessageSource`를 스프링 빈으로 등록해야 한다.
  - 스프링 부트는 자동으로 등록해준다.
  - 스프링 부트는 `messages.properties`가 기본 메시지 파일이다. 
### 국제화 
- 메시지 파일을 각 나라별로 별도로 관리하면 서비스를 국제화 할 수 있다.
  - `messages_ko.properties`와 같이 언어에 맞는 메시지 파일을 생성하면 된다.
- 어떤 나라에서 접근했는지 인식하는 방법은 `Accept-Language` 헤더 값을 사용하거나, 사용자가 직접 언어를 선택하도록 하고 쿠키 등을 사용해서 처리하면 된다.
  - 스프링 부트는 `Accept-Language`로 인식하는 방법을 기본으로 지원한다.
  - 스프링은 `Locale` 선택 방식을 변경할 수 있도록 `LocaleResolver`라는 인터페이스를 제공한다.

## BindingResult
- 스프링이 제공하는 검증 오류를 보관하는 객체이다.
- 검증 오류가 발생하면 `BindingResult`에 보관하면 된다.
- 타임리프는 스프링의 `BindingResult`를 활용해서 편리하게 검증 오류를 표현하는 기능을 제공한다.
- `reject()`, `rejectValue()`, `Bean Validation`은 `MessageCodesResolver`로 메시지 코드를 생성하고, 매칭되는 오류 메시지를 찾는다.
  - 없으면 기본값을 사용한다.

### MessageCodesResolver
- 검증 오류 코드로 메시지 코드들을 생성한다.
  - 구체적인 것이 더 우선시된다.
  - 덜 구체적인 것은 범용적으로 사용할 수 있다.
- `MessageCodesResolver`는 인터페이스이고 `DefaultMessageCodesResolver`는 기본 구현체이다.

### DefaultMessageCodesResolver의 기본 메시지 생성 규칙
1. 객체 오류
  1) code + "." + object name
    - ex) `required.item`
  2) code
    - ex) `required`

2. 필드 오류
  1) code + "." + object name + "." + field
    - ex) `typeMismatch.user.age`
  2) code + "." + field
  3) code + "." + field type
    - ex) `typeMismatch.int`
  4) code

## 검증
- HTTP 요청을 처리하기 전에, 요구사항에 맞는 요청인지 검증하는 작업이 필요하다.
  - 스프링은 검증을 위해 `BindingResult` 객체를 지원한다.
- 클라이언트 검증과 서버 검증을 둘 다 사용하되, 최종적으로 서버 검증은 필수이다.
  - 클라이언트 검증은 조작할 수 있으므로 보안에 취약하다.
  - 서버만으로 검증하면, 즉각적인 고객 사용성이 부족해진다.

### 유의점
- 폼 데이터는 `BindingResult`로 검증하고, API 데이터는 예외를 직접 던져서 `@ExceptionHandler`로 처리한다.
  - `@ModelAttribute`는 특정 필드가 바인딩 되지 않아도 나머지 필드는 정상 바인딩 되고, Validator를 사용한 검증도 적용할 수 있다.
  - `@RequestBody`는 `HttpMessageConverter` 단게에서 JSON 데이터를 객체로 변경하지 못하면 예외가 발생하기 때문에, 컨트롤러가 호출되지 않고 Validator도 적용할 수 없다.
- `BindingResult`는 검증할 대상 바로 다음에 와야한다.
- `BindingResult`는 Model에 자동으로 포함된다.
- 폼 데이터 전달을 위한 별도의 객체를 사용한다.
  - ex) `Item` 대신 `ItemSaveForm` 사용
  - 대부분의 경우 폼에서 전달하는 데이터와 도메인 객체가 딱 맞지 않기 때문에, Bean Validation의 `groups` 기능은 사용하지 않는다.
  - 대신 변환 작업이 추가된다.
 
### 검증 방법
- 오브젝트 관련 오류는 `BindingResult`가 제공하는 `reject()`를 사용한다.
  - Bean Validation의 `@ScriptAssert()`는 제약이 많고 복잡하다.
- 필드는 `Bean Validation`으로 검증한다.
  - Bean Validation은 검증 로직을 모든 프로젝트에 적용할 수 있도록 공통화하고, 표준화한 기술이다.
  - 스프링 부트가 자동으로 Bean Validator를 글로벌 Validator로 등록해준다.

## 필터 & 인터셉터
- 애플리케이션 여러 로직에서 공통으로 관심이 있는 것을 공통 관심사라고 한다.
  - ex) 여러 컨트롤러에서 로그인 여부 확인 필요
- 공통 관심사는 스프링의 AOP로 해결할 수 있지만, 웹과 관련된 공통 관심사는 서블릿 필터 또는 스프링 인터셉터를 사용하는 것이 좋다.
  - 웹과 관련된 공통 관심사를 처리할 때는 HTTP의 헤더나 URL의 정보들이 필요하다.
  - 인터셉터는 스프링 MVC 구조에 특화된 필터 기능을 제공하므로, 일반적으로는 인터셉터를 사용하는 것이 더 편리하다.

### 1. 필터
- 서블릿에 요청이 전달되기 전/후에 url 패턴에 맞는 모든 요청에 대해 부가 작업을 처리할 수 있는 기능을 제공한다.
  - 스프링의 경우 서블릿은 디스패쳐 서블릿이 해당된다.
- 스프링 부트를 사용한다면, `FilterRegistrationBean`로 필터를 등록할 수 있다.
  - `ServletComponentScan`, `@WebFilter`는 필터 순서 조절이 안된다.
  - 서블릿 컨테이너가 필터를 싱글톤 객체로 생성하고, 관리한다.
- 다음 필터나 서블릿을 호출할 때 `request`, `response`를 다른 객체로 만들어 넘길 수 있다.

#### 필터 흐름
- 필터 흐름 : `HTTP 요청 -> WAS -> 필터 -> 서블릿 -> 인터셉터 -> 컨트롤러`
  1. 서블릿 컨테이너가 생성될 때 `init()`가 호출된다.
  2. 고객의 요청이 올 때마다 `doFilter()`메서드가 호출된다.
  3. 필터는 체인처럼 여러개로 추가할 수 있으며, 다음 필터가 없다면 서블릿을 호출한다.
    - 적절하지 않는 요청이라고 판단되면, 서블릿이 호출되지 않는다.
  4. 이후 서블릿 컨테이너가 종료될 때 `destroy()`가 호출된다.

### 2. 인터셉터
- 스프링 MVC가 제공하는 기능으로, 디스패쳐 서블릿이 컨트롤러를 호출하기 전/후와 요청 완료 후에 추가적인 작업을 할 수 있도록 기능을 제공한다.
- 인터셉터는 `request`, `response` 뿐만 아니라, 어떤 컨트롤러가 호출되는지와 어떤 `modelAndView`가 반환되는지 알 수 있다. 
- `WebMvcConfigurer`가 제공하는 `addInterceptors()`로 인터셉터를 등록할 수 있다.
  - 싱글톤처럼 사용되기 때문에 멤버변수를 사용하면 위험하다.
- [URL 경로 공식 문서](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/util/pattern/PathPattern.html)

#### 인터셉터 흐름
![image](https://user-images.githubusercontent.com/87891581/168583864-9db2087c-cf50-4516-b766-9dd181573cb0.png)
1. HTTP 요청이 들어오면, 디스패쳐 서블릿을 거쳐 `preHandle()`이 호출된다.
   - `preHandle()`의 응답값이 true면 다음으로 진행하고, false면 더이상 진행되지 않는다.
2. 컨트롤러를 거쳐 내부 로직 수행 후 `postHandle()`이 호출된다.
   - 컨트롤러에서 예외가 발생하면 `postHandle()`은 호출되지 않는다.
3. 뷰가 렌더링 된 후 `afterCompletion()`이 호출된다.
   - `afterCompletion()`은 예외가 발생하더라도 항상 호출된다.

## 예외 처리와 오류 페이지
- 스프링 부트를 사용한다면 오류 페이지를 적절한 경로에 추가만 하면 된다.
### 서블릿 예외처리
- 서블릿은 다음 2가지 방식으로 예외 처리를 지원한다.
  1. `Exception`
     - `WAS(여기까지 전파) <- 필터 <- 서블릿 <- 인터셉터 <- 컨트롤러(예외 발생)`
     - 애플리케이션에서 발생한 예외를 잡지 못해서 WAS까지 예외가 올라온다면, WAS가 기본으로 제공하는 오류 페이지를 볼 수 있다.
  2. `response.sendError(http 상태 코드, 오류 메시지)`
     - HTTP 상태 코드와 오류 메시지를 추가할 수 있다.
     - `WAS(sendError 호출 기록 확인) <- 필터 <- 서블릿 <- 인터셉터 <- 컨트롤러(sendError() 호출)`
     - 당장 예외가 발생하지는 않지만, 서블릿 컨테이너에게 오류가 발생했다는 점을 전달한다.
- 기본 오류 페이지 대신, 다른 오류 페이지를 등록해서 사용할 수 있다.
  - `WebServerFactoryCustomizer`의 `customize()`를 오버라이딩해서, 예외 종류에 따라 `ErrorPage` 등록
  - 예외 처리용 컨트롤러 필요

#### 예외 발생과 오류 페이지 요청 흐름
> 클라이언트는 서버 내부에서 이런 일이 일어나는지 전혀 알지 못한다. 오직 서버 내부에서 오류 페이지를 찾기 위해 추가적인 호출을 한다.

```
1. WAS(클라이언트 요청, dispatcherType = REQUEST) -> 필터 -> 서블릿 -> 인터셉터 -> 컨트롤러
2. WAS <- 필터 <- 서블릿 <- 인터셉터 <- 컨트롤러(예외 발생 or sendError 호출)
2. WAS(에러 페이지 요청, dispatcherType = ERROR) -> 필터(X) -> 서블릿 -> 인터셉터(X) -> 컨트롤러 -> View(에러 페이지)
```
- 예외가 WAS까지 전달되면, WAS는 오류 페이지 경로를 찾아서 내부에서 오류 페이지를 호출한다. 
   - WAS는 오류 정보를 `request`의 `attribute`에 추가해서 넘겨준다.
- 오류 페이지 경로로 필터, 서블릿, 인터셉터, 컨트롤러가 모두 다시 호출된다.
  - `DispatcherType(forward, include, request, async, error)`에 따라 필터 적용 여부를 설정할 수 있다.
  - 인터셉터는 서블릿이 아니라 스프링이 제공하는 기능이기 때문에, 적용 여부를 `excludePathPatterns`로 설정하면 된다.

### 스프링 부트와 오류 페이지
- 서블릿에서 예외 처리 페이지를 등록하기 위해서는 복잡한 과정을 거쳐야한다. 
- 스프링 부트는 이런 과정을 기본으로 제공하기 때문에, 개발자는 오류 페이지 파일을 추가만 하면 된다.
  - `/error` 경로에 에러 페이지를 추가하면, 자동으로 등록된다.
  - `BasicController`라는 예외 처리 컨트롤러가 자동으로 등록된다.
    - `BasicController`는 예외 정보를 model에 담아서 뷰로 전달한다.
    - `BasicController`는 `text/html` 이외의 요청의 경우 응답을 JSON으로 반환한다.

#### BasicController의 뷰 선택 우선순위
1. 뷰 템플릿
   - `resources/templates/error/500.html` : 구체적인 것이 우선순위가 더 높다.
   - `resources/templates/error/5xx.html`
2. 정적 리소스(static, public)
   - `resources/static/error/404.html`
   - `resources/static/error/4xx.html`
3. 적용 대상이 없을 때 뷰 이름(error)
   - `resources/template/error.html`

## API 예외 처리
- HTMl 페이지의 경우 4xx, 5xx와 같은 오류 페이지만 있으면, 대부분의 문제를 해결할 수 있다. 
- API는 각 오류 상황에 맞는 오류 응답 스펙을 정하고, JSON으로 데이터를 내려주어야 한다.
  - `BasicErrorController`를 확장해서 JSON 오류 메시지를 변경할 수 있다.
  - 하지만 `@ExceptionHandler`와 `@ControllerAdvice`를 사용하면 예외를 훨씬 깔끔하게 처리할 수 있다.

### 스프링 MVC와 API 예외처리
![image](https://user-images.githubusercontent.com/87891581/168731890-ab3c4b86-8dd9-4141-bc90-b24dd40c3068.png)
- 스프링 MVC는 컨트롤러(핸들러) 밖으로 던저진 예외를 해결하고, 동작 방식을 변경할 수 있도록 `ExceptionResolver`를 제공한다.
  - 컨트롤러에서 예외가 발생하면 `postHandle()`이 호출되지 않고, `ExceptionResolver`가 호출된다.
- 예외가 발생해도 서블릿 컨테이너까지 예외가 전달되지 않고, 스프링 MVC에서 예외 처리는 끝이난다.
  - 결과적으로 WAS 입장에서는 정상 처리가 되었다.

#### `ExceptionResolver` 종류
1. `ExceptionHandlerExceptionResolver`
   - 예외가 발생하면 `@ExceptionHandler`가 달린 메서드가 호출된다.  
   - `@ExceptionHandler`에 지정한 클래스부터 자식 클래스까지 처리할 수 있다.
     - `부모예외처리()`와 `자식예외처리()`가 공존하는 경우 더 자세한 `자식예외처리()`가 우선권을 가진다.
     - 클래스 지정을 생략하면, 메서드 파라미터의 예외가 지정된다.
   - html, api 응답 둘 다 가능하다.
   - `@ControllerAdvice` 또는 `@RestController`를 사용하여 예외 처리 로직을 분리할 수 있다.
     - 예외 처리할 컨트롤러를 다양한 방법으로 지정할 수 있다.
     - 지정하지 않으면 모든 컨트롤러에 적용된다.
2. `ResponseStatusExceptionResolver`
   - `@ResponseStatus`가 달려있는 예외나 `ResponseStatusException` 예외를 처리한다.
     - 상태코드와 메시지를 변경할 수 있다.
   - 코드를 수정할 수 없는 라이브러리나 동적인 처리에 `ResponseStatusException`를 사용한다.
3. `DefaultHandlerExceptionResolver`
   - 스프링 내부에서 발생하는 스프링 예외를 해결한다.
   - ex) `TypeMismatchException` 예외가 발생하면, HTTP 상태코드 400 오류 발생
   - 상속해서 예외 메시지를 변경할 수 있지만, `@ExceptionHandler`를 사용하자

## 컨버터 & 포맷터
### 1. 컨버터
- 문자를 숫자로 변환하거나, 객체를 문자로 변환하는 등 타입을 변환하는 기능을 제공한다.
- 스프링의 타입 변환 적용 예
  - 스프링 MVC 요청 파라미터(`@RequestParam`, `@ModelAttribute`, `@PathVariable`)
  - `@Value` 등으로 YML 정보 읽기
  - XML에 넣은 스프링 빈 정보를 변환
  - 뷰를 렌더링 할 때
- 스프링은 개발 컨버터를 모아두고 그것들을 묶어서 편하게 사용할 수 있도록 하는 `ConversionService`를 제공한다.
- 스프링에 추가적인 타입 변환이 필요하다면, `Converter` 인터페이스를 구현한 다음에 `WebMvcConfigurer`가 제공하는 `addFormatters()`로 등록하면 된다.
  - 스프링 내부에서 사용하는 `ConversionService`에 컨버터가 추가된다.
  - `org.springframework.core.convert.converter.Converter`
  - `Converter` 외에도 다양한 방식의 컨버터를 제공한다.
  - 추가한 컨버터가 기본 컨버터보다 높은 우선순위를 가진다.
- 타임리프의 경우 `${{...}}`를 사용하면, 자동으로 컨버전 서비스를 사용해서 변환된 결과를 출력해준다.
  - `th:field`도 자동으로 컨버전 서비스를 적용해준다.

### 2. 포맷터
- 포맷터는 객체를 문자로 변경하고, 문자를 객체로 변경하는 기능을 수행한다.
- 컨버터와 동일한 방식으로 포맷터를 등록할 수 있다.
  - 포맷터는 문자에 특화된 컨버터일 뿐이다.
  - `${{...}}`도 사용할 수 있다.
  - 우선순위는 컨버터가 더 높다.
- 스프링은 날짜와 숫자를 애노테이션 기반으로 원하는 형식을 지정해서 사용할 수 있는 포맷터를 제공한다.  
  - `@NumberFormat` : 숫자 관련 형식 지정 포맷터 사용
  - `@DateTimeFormat` : 날짜 관련 형식 지정 포맷터 사용
- `HttpMessageConverter`에는 컨버전 서비스가 적용되지 않는다.
  - `HttpMessageConverter`의 역할은 HTTP 메시지 바디의 내용을 객체로 변환하거나 객체를 HTTP 메시지 바디에 입력하는 것이다.
  - `HttpMessageConverter` 내부에서 사용되는 라이브러리가 변환 작업을 진행한다. 이는 컨버전 서비스와 관계 없다. 
  - `ArgumentResolver`는 컨버전 서비스를 사용해서 타입을 변환한다.

### 3. 차이점
- `Converter`는 입력과 출력 타입에 제한이 없는, 범용 타입 변환 기능을 제공한다.
- `Formatter`는 문자를 다른 객체로 변환하거나 객체를 문자로 변환하는 기능을 제공한다.
  - 즉, 문자에 특화된 컨버터이다.
  - `Locale` 현지화 정보가 사용될 수 있다.

## 파일 업로드
- `multipart/form-data`방식은 다른 종류의 여러 파일과 폼의 내용을 함께 전송할 수 있다.
  - 일반적인 폼 데이터는 문자 형식, 파일은 바이너리 형식이다.
- 스프링이 지원하는 `MultipartFile`로 `multipart/form-data` 방식의 폼 데이터를 효과적으로 처리할 수 있다. 
  - 업로드하는 HTML Form의 name에 맞추어 `@RequestParam`을 적용하거나, `@ModelAttribute`를 사용해도 된다. 
  - 서블릿이 제공하는 `Part`는 `HttpServletRequest`를 사용해야 하고, 추가로 파일 부분만 구분하려면 여러가지 코드를 넣어야 한다.

### 유의점
- 큰 파일을 무제한 업로드하게 둘 수 없으므로 업로드 사이즈를 제한할 수 있다.
  - `max-file-size` : 파일 하나의 최대 사이즈, 기본 1MB
  - `max-request-size` : 전체 파일 용량의 최대 사이즈, 기본 10MB
- 고객이 업로드한 파일명으로 서버 내부에 파일을 저장하면 안된다.
  - 서버에서는 저장할 파일명이 겹치지 않도록 내부에서 관리하는 별도의 파일명이 필요하다.