# Spring

빈 후처리기
AOP
디자인 패턴
로깅 라이브러리


- AOP(Aspect Oriented Programming)
- Filter vs Interceptor
- AOP vs Interceptor
- 레이어드 아키텍처
- OSIV
- 커넥션 풀
- DataSource
- 트랜잭션을 추상화하는 이유
- 트랜잭션 동기화 매니저
- 선언적 트랜잭션 vs 프로그래밍 방식 트랜잭션
- @Transactional
Propagation 전파단계
ORM
영속성 컨텍스트
N+1 문제
fetch join 한계
OneToMany fetch join 페이징 쿼리 성능 이슈
MultipleBagFetchException
OneToOne 양방향 관계 Lazy 로딩 주의
상속관계 매핑
QueryDsl을 사용하는 이유
Spring batch
MSA vs Monolithic(모놀리식)
DDD 구조

---

<details>
   <summary>프레임워크와 라이브러리</summary>

- 프레임워크 : 원하는 기능 구현에 집중하여 개발할 수 있도록, 일정한 형태와 필요한 기능을 갖추고 있는 골격, 뼈대를 의미한다.
- 라이브러리 : 자주 사용되는 로직을, 재사용이 편리하도록 잘 정리한 코드의 집합을 말한다.
- 프레임워크는 사용자가 작성한 코드를 프레임워크가 직접 제어하고, 대신 실행한다. 하지만 라이브러리는 사용자가 작성한 코드가 직접 제어의 흐름을 담당한다.

---

</details>


<details>
   <summary>EJB</summary>

- Enterprise JavaBeans
- 기업 환경의 시스템을 구현하기 위한 서버측 컴포넌트 모델이다.
- 복잡하고 객체지향적이지 않다는 단점 등으로 인해 스프링이 등장하였다.

---

</details>

<details>
   <summary>POJO</summary>

- Plain Old Java Object
- 특정 기술 규약과 환경에 종속되지 않은 순수한 자바 오브젝트를 말한다.
- 코드가 간결하고 테스트가 용이하다는 장점이 있다.

---

</details>


<details>
   <summary>Spring이란</summary>

- 자바 엔터프라이즈 개발을 편하게 해주는 경량급 오픈소스 애플리케이션 프레임워크이다.
- 특징
  - POJO 기반으로 구성되어 코드가 간결하고 테스트가 용이하다.
  - DI를 통해 객체 관계를 구성한다.
  - AOP를 지원하여 개발자가 핵심 비즈니스 로직에 집중할 수 있도록 한다.
  - MVC 구조를 웹을 개발할 수 있도록 지원한다.

---

</details>

<details>
   <summary>스프링 부트란</summary>

- 스프링을 복잡한 설정 없이 쉽고 빠르게 만들어주는 프레임워크이다.

---

</details>

<details>
   <summary>IoC</summary>

- Inversion Of Control, 제어의 역전
- 객체의 생성에서부터 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀐 것을 말한다.
- 개발자가 프레임워크에 필요한 부분을 개발하고 조립하면, 코드의 최종 호출은 프레임워크에 의해 이뤄진다. 

---

</details>

<details>
   <summary>DI (Dependency Injection)</summary>

- Dependency Injection, 의존관계 주입 or 의존성 주입
- Spring 프레임워크에서 지원하는 IoC의 형태로, 클래스 사이의 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 연결해 주는 것을 말한다.

---

</details>

<details>
   <summary>DI 주입 방식</summary>

1. 생성자 주입
   - 생성자를 통해서 의존관계를 주입받는 방법
   - 생성사 호출 시점에 딱 1번만 호출되는 것을 보장 
   - final 키워드로 불변하게 설계할 수 있고, 초기화 누락 시 컴파일 시점에 오류가 발생하기 떄문에 가장 권장되는 방법이다.
2. 수정자 주입
   - setter 메서드를 통해서 의존관계를 주입 받는 방법
   - setter를 public으로 열어야 하므로, 누군가 실수로 호출할 수 있다.
   - 보통 한번 주입한 의존관계를 변경할 일이 거의 없지만, 필요한 경우 선택적으로 사용
3. 필드 주입
   - 필드에 의존관계를 바로 주입받는 방법
   - DI 프레임워크가 없으면 의존관계를 주입받을 수 없다.
   - 외부에서 변경이 불가능하기 때문에 테스트하기 어려우므로, 권장하지 않는 방법이다.
4. 일반 메서드 주입
   - 일반 메서드를 통해서 의존관계를 주입받는 방법으로, 잘 사용하지 않는다.

---

</details>

<details>
   <summary>스프링 컨테이너</summary>

- BeanFactory와 ApplicationContext를 스프링 컨테이너라고 한다.
  - BeanFactory는 빈을 관리하고 조회하는 역할을 한다.
  - BeanFactory를 상속한 ApplicationContext는 빈 관리 기능뿐만 아니라, 국제화 등의 추가적인 기능을 제공한다.

---

</details>

<details>
   <summary>스프링이 싱글톤을 지원하는 이유</summary>

- 대부분의 스프링 애플리케이션은 웹 애플리케이션이다. 웹 애플리케이션은 보통 여러 고객이 여러 요청을 한다.
- 싱글톤을 사용하지 않으면 각 요청마다 새로운 객체가 생성되고 소멸된다. 이 방식은 트래픽이 증가할수록 메모리 낭비가 심하기 때문에, 객체를 1개만 생성하고 공유하는 싱글톤 패턴을 사용한다.

---

</details>

<details>
   <summary>@Configuration과 싱글톤</summary>

- `@Configuration`는 `@Bean`이 붙은 메서드마다 이미 스프링 빈이 존재하면 기존의 빈을 반환하고, 스프링 빈이 존재하지 않으면 스프링 빈을 새로 등록하고 반환하는 코드가 동적으로 만들어진다.
  - 참고로 `@Configuration`이 붙은 클래스도 스프링 빈으로 등록된다.
- 즉, `@Bean`만 사용해도 스프링 빈으로 등록되지만, 싱글톤을 보장하지 않는다.
---

</details>

<details>
   <summary>빈이란</summary>

- 스프링 컨테이너가 생성하고 관리하는 자바 객체를 빈이라고 한다.
- `@Bean`나 `<bean>`로 설정 파일에 빈을 직접 등록하거나, 컴포너트 스캔을 이용하여 자동으로 등록할 수 있다.

---

</details>

<details>
   <summary>@Bean vs @Component</summary>

- 둘 다 스프링 컨테이너에 빈을 등록하기 위해 사용한다.
- `@Bean` : 개발자가 작성한 method에 `@Bean`을 붙여주면, 해당 메서드가 반환하는 객체가 빈으로 등록된다.
  - `@Configuration`과 함께 사용해야 한다.
- `@Component` : 개발자가 작성한 클래스에 `@Component`를 붙여주면, 해당 클래스는 빈으로 등록된다.

---

</details>

<details>
   <summary>@Bean을 @Configuration과 함께 사용해야 하는 이유</summary>

- `@Configuration`는 `@Bean`이 붙은 메서드마다 이미 스프링 빈이 존재하면, 존재하는 빈을 반환하도록 한다. 스프링 빈이 없으면, 새로 생성해서 빈으로 등록하는 코드가 동적으로 만들어진다.
- 즉, `@Bean`만 사용해도 스프링 빈으로 등록되지만, 싱글톤을 보장하지 않는다.

---

</details>

<details>
   <summary>@Component 종류</summary>

- `@Controller` : 스프링 MVC 컨트롤러로 인식
- `@Repository` : 스프링 데이터 접근 계층으로 인식하고, 데이터 계층의 예외를 스프링 예외로 변환해준다.
- `@Configuration` : 스프링 설정 정보로 인식하고, 스프링 빈이 싱글톤을 유지하도록 추가 처리를 한다.
- `@Service` : `@Service` 는 특별한 처리를 하지 않는다. 대신 비즈니스 계층을 인식하는데 도움이 된다

---

</details>

<details>
   <summary>빈의 생명주기</summary>

- 스프링 컨테이너 생성 -> 스프링 빈 생성 -> 의존관계 주입 -> 초기화 콜백 -> 사용 -> 소멸전 콜백 -> 스프링 종료
    - 초기화 콜백 : 빈 생성과 의존관계 주입이 완료된 후 호출
    - 소멸전 콜백 : 빈이 소멸되기 직전에 호출

---

</details>

<details>
   <summary>빈 생명주기 콜백 지원 방법</summary>

- 스프링은 빈의 생성과 의존관계 주입이 완료되면 초기화 콜백이 발생한다. 또한, 싱글톤 빈은 스프링 컨테이너가 종료되기 직전에 소멸 콜백이 발생한다.
- 스프링은 인터페이스를 구현하는 방법, 설정 정보에서 빈 속성을 사용하는 방법, 애노테이션을 사용하는 방법으로 빈 생명주기 콜백을 지원한다.
  1. 인터페이스를 구현하는 방법
     - `InitializingBean`의 `afterProperties()` 메서드로 초기화를 지원한다.
     - `DisposableBean`의 `destroy()` 메서드로 소멸을 지원한다.
  2. 설정 정보에서 빈 속성을 사용하는 방법
     - 빈의 initMethod 속성에 메서드 이름 지정으로 초기화를 지원한다.
     - 빈의 destroyMethod 속성에 메서드 이름 지정으로 소멸을 지원한다.
  3. 애노테이션을 사용하는 방법
     - 메서드에 `@PostConstruct`를 붙여서 초기화를 지원한다.
     - 메서드에 `@PreDestroy`를 붙여서 소멸을 지원한다.
- 애노테이션을 사용하는 것을 권장하며, 외부 라이브러리를 초기화나 종료해야 하는 경우 설정 정보에서 빈 속성을 사용한다.

---

</details>

<details>
   <summary>빈 스코프</summary>

- 빈이 존재할 수 있는 범위를 의미하며, 스프링은 다양한 스코프를 지원한다.
1. 싱글톤
   - default 스코프다.
   - 빈이 스프링 컨테이너의 시작과 종료까지 유지된다. 
2. 프로토타입
   - 스프링 컨테이너가 빈의 생성과 의존관계 주입, 초기화까지만 관여한다.
   - 싱글톤 빈은 한번만 생성되지만, 프로토타입 빈은 요청할 때마다 생성된다.
3. 웹 스코프
   - 웹 환경에서만 동작하며, 스프링이 해당 스코프의 종료 시점까지 관리한다. 
   - request : HTTP 요청이 들어오고 나갈때까지 유지되는 스코프
   - session : HTTP 세션과 동일한 생명주기를 가지는 스코프
   - application : 서블릿 컨텍스트와 동일한 생명주기를 가지는 스코프
   - websocket : 웹 소켓과 동일한 생명주기를 가지는 스코프
     - 웹 소켓 : 클라이언트와 서버가 양방향 소통을 가능하게 하는 프로토콜

---

</details>

<details>
   <summary>웹 서버와 웹 애플리케이션 서버</summary>

![image](https://user-images.githubusercontent.com/87891581/192721935-a350c793-4754-43f8-832b-b6bcbfc76f46.png)

**1. 웹 서버(Web Server)**
- 클라이언트가 요청하는 정적 리소스를 제공한다.
    - 정적 리소스 : 정적(파일) HTML, CSS, JS, 이미지, 영상
- 예) NGINX, APACHE

**2. 웹 애플리케이션 서버(WAS, Web Application Server)**

- 프로그램 코드를 실행해서 애플리케이션 로직 수행
    - 동적 HTML, HTTP API(JSON) 제공
- 웹 서버 기능 포함
- 예) 톰캣, Jetty, Undertow

**3. 차이점**
- 웹 서버는 정적 리소스(파일)를 제공하고, WAS는 애플리케이션 로직을 수행한다.
- WAS도 웹 서버 기능을 제공할 수 있기 때문에 웹 서버 없이 WAS와 DB 만으로도 시스템 구성이 가능하다. 하지만 애플리케이션 로직이 정적 리소스 때문에 수행이 어려울 수 있고, WAS 장애 시 오류 화면 노출이 불가능하다는 단점이 있다.

---

</details>

<details>
   <summary>서블릿</summary>

- 웹 페이지를 동적으로 생성하기 위해 사용하는 서버 프로그램이다.
- HTTP 요청 메시지 파싱하는 등의 부가적인 작업을 처리하여, 개발자가 비즈니스 로직에만 신경쓰도록 한다.

---

</details>

<details>
   <summary>서블릿 생성 시점</summary>

- 서버 설정에 따라 다르다. 최초 요청 시점에 생성하게 할 수도 있고, 서블릿 컨테이너가 로딩될 때 생성하게 할 수도 있다.

---

</details>

<details>
   <summary>JSP</summary>

- HTML 코드에 자바 코드를 삽입하여, 동적으로 웹 페이지를 생성하는 서버 사이드 스크립트 언어이다.
- 서블릿으로 화면과 관련된 작업을 하면 상당히 복잡하기 때문에 등장하였다.
- 실행 시 서블릿으로 변환된다.

---

</details>

<details>
   <summary>서블릿 컨테이너</summary>

- 톰캣처럼 서블릿을 지원하는 WAS를 서블릿 컨테이너라고 한다.
- 서블릿 컨테이너는 서블릿 객체의 생명주기(생성, 초기화, 호출, 종료)를 관리한다.
  - 서블릿 컨테이너 종료시 함께 종료
- 서블릿 객체는 싱글톤으로 관리된다.
  - 요청마다 객체를 생성하는 것은 비효율적이다. 
  - 모든 요청은 동일한 서블릿 객체 인스턴스에 접근
- 동시 요청을 위한 멀티 쓰레드 처리 지원

---

</details>

<details>
   <summary>요청 시 서블릿 컨테이너 동작 과정</summary>

![image](https://user-images.githubusercontent.com/87891581/192733332-c6be7272-2edd-4d1c-aca0-bd2f9b7af870.png)

1. 사용자가 URL을 입력
2. Servlet Container는 쓰레드 풀에서 쓰레드를 꺼내 할당해주고, HttpServletRequest 객체와 HttpServletResponse 객체를 생성한다.
3. 사용자가 요청한 URL로 어떤 서블릿에 대한 요청인지 찾는다.
4. 해당 서블릿의 service()를 실행한다.
5. 실행이 끝나면 HttpServletResponse 객체 정보를 바탕으로, 클라이언트에게 응답을 보낸다.
6. HttpServletRequest 객체와 HttpServletResponse 객체는 소멸되고, 쓰레드 풀로 쓰레드를 반환한다. 

---

</details>

<details>
   <summary>동시 처리 해결 방안</summary>

**1. 요청마다 쓰레드 생성**
- 쓰레드의 생성 비용이 소모되고 생성에 제한이 없다는 단점이 있다.

**2. 쓰레드 풀**
- 쓰레드가 미리 생성되어 있으므로, 쓰레드를 생성하고 종료하는 비용이 절약되고, 응답 시간이 빠르다.
- 생성 가능한 최대치가 존재하므로, 너무 많은 요청이 들어와도 기존 요청은 안전하다.
- 최대 쓰레드 수를 적절하게 설정하는 것이 중요하다.
  - 너무 낮게 설정하면, 동시 요청이 많을 때 서버 리소스는 여유롭지만 응답이 지연된다.
  - 너무 높게 설정하면, 동시 요청이 많을 때 CPU, 메모리 리소스 임계점 초과로 서버가 다운된다.

---

</details>

<details>
   <summary>SSR & CSR</summary>

### SSR
- 서버 사이드 렌더링
- HTML 최종 결과를 서버에서 만들어서 웹 브라우저에 전달
- 주로 정적인 화면에 사용
- SSR을 사용하더라도, 자바스크립트를 사용해서 화면 일부를 동적으로 변경 가능
- 관련 기술 : JSP, 타임리프

### CSR
- 클라이언트 사이드 렌더링
- HTML 결과를 자바스크립트를 사용해 웹 브라우저에서 동적으로 생성해서 적용
- 주로 동적인 화면에 사용, 웹 환경을 마치 앱처럼 필요한 부분을 변경할 수 있음
- 관련 기술 : React, Vue.js

### 참고
- CSR, SSR을 동시에 지원하는 웹 프레임워크도 있다.

---

</details>

<details>
   <summary>redirect vs forward</summary>

- 리다이렉트
  - 클라이언트로 요청에 대한 응답이 나갔다가, redirect 경로로 새로 요청하는 것이다.
  - 클라이언트가 인지할 수 있고, URL 경로도 실제로 변경된다.
- 포워드
  - 서블릿이나 JSP가 요청을 받은 후 다른 서블릿이나 JSP로 처리를 위임하는 것이다.
  - 서버 내부에서 일어나는 호출이기 때문에 클라이언트가 전혀 인지하지 못한다.

---

</details>

<details>
   <summary>프론트 컨트롤러 패턴</summary>


---

</details>

<details>
   <summary>MVC 패턴</summary>


---

</details>

<details>
   <summary>스프링 MVC의 요청 처리 과정</summary>


---

</details>


<details>
   <summary>Entity, VO, DTO, DAO</summary>



</details>
