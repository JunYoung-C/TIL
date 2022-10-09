# Spring



Spring batch
MSA vs Monolithic(모놀리식)
DDD 구조

---

<details>
   <summary>Entity, VO, DTO, DAO</summary>

<br/>

- Entity
    - 핵심 비즈니스 도메인이고, JPA에서는 데이터베이스 테이블과 ORM 매핑되어 있는 객체이다.
    - 로직을 가질 수 있다.
- VO(Value Object)
    - 실제 데이터만을 저장하는 객체이다.
    - 로직을 포함할 수 있으며, 객체의 불변성을 보장한다.
- DTO(Data Transfer Object)
    - 계층간 데이터 교환을 위해 사용하는 객체이다.
    - 주요 로직 없이, 단순 getter, setter만 존재한다.
- DAO(Data Access Object)
    - DB에 접근하여 실제 데이터를 조회하거나 조작하는 기능을 가진 객체이다.
    - DAO는 데이터베이스에 더 가깝고, Repository는 도메인 객체에 더 가까운 개념이다.
    - Repository는 DAO를 사용해서 구현할 수 있다.

</details>

<details>
   <summary>프레임워크와 라이브러리</summary>

<br/>

- 프레임워크 : 원하는 기능 구현에 집중하여 개발할 수 있도록, 일정한 형태와 필요한 기능을 갖추고 있는 골격, 뼈대를 의미한다.
- 라이브러리 : 자주 사용되는 로직을, 재사용이 편리하도록 잘 정리한 코드의 집합을 말한다.
- 프레임워크는 사용자가 작성한 코드를 프레임워크가 직접 제어하고, 대신 실행한다. 하지만 라이브러리는 사용자가 작성한 코드가 직접 제어의 흐름을 담당한다.

---

</details>


<details>
   <summary>EJB</summary>

<br/>

- Enterprise JavaBeans
- 기업 환경의 시스템을 구현하기 위한 서버측 컴포넌트 모델이다.
- 복잡하고 객체지향적이지 않다는 단점 등으로 인해 스프링이 등장하였다.

---

</details>

<details>
   <summary>POJO</summary>

<br/>

- Plain Old Java Object
- 특정 기술 규약과 환경에 종속되지 않은 순수한 자바 오브젝트를 말한다.
- 코드가 간결하고 테스트가 용이하다는 장점이 있다.

---

</details>


<details>
   <summary>Spring이란</summary>

<br/>

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

<br/>

- 스프링을 복잡한 설정 없이 쉽고 빠르게 만들어주는 도구이다.
  - 자주 사용하는 모듈간의 의존성과 버전 조합 제공
  - 자동 설정
  - 내장 WAS

---

</details>

<details>
   <summary>IoC</summary>

<br/>

- Inversion Of Control, 제어의 역전
- 객체의 생성에서부터 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀐 것을 말한다.
- 개발자가 프레임워크에 필요한 부분을 개발하고 조립하면, 코드의 최종 호출은 프레임워크에 의해 이뤄진다. 
- 객체 지향 원칙을 잘 지키기 위해 사용한다.
  - 내부에서 직접 객체를 생성하는 방법보다 외부에서 주입받는게 변경에 더 유연한다.
  - 객체 생성을 위해 구체 클래스 의존을 피할 수 없다. DIP 위반이다.
---

</details>

<details>
   <summary>DI (Dependency Injection)</summary>

<br/>

- Dependency Injection, 의존관계 주입 or 의존성 주입
- Spring 프레임워크에서 지원하는 IoC의 형태로, 클래스 사이의 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 연결해 주는 것을 말한다.

---

</details>

<details>
   <summary>DI 주입 방식</summary>

<br/>

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

---

</details>

<details>
   <summary>스프링 컨테이너</summary>

<br/>

- BeanFactory와 ApplicationContext를 스프링 컨테이너라고 한다.
  - BeanFactory는 빈을 관리하고 조회하는 역할을 한다.
  - BeanFactory를 상속한 ApplicationContext는 빈 관리 기능뿐만 아니라, 국제화 등의 추가적인 기능을 제공한다.

---

</details>

<details>
   <summary>스프링이 싱글톤을 지원하는 이유</summary>

<br/>

- 대부분의 스프링 애플리케이션은 웹 애플리케이션이다. 웹 애플리케이션은 보통 여러 고객이 여러 요청을 한다.
- 싱글톤을 사용하지 않으면 각 요청마다 새로운 객체가 생성되고 소멸된다. 이 방식은 트래픽이 증가할수록 메모리 낭비가 심하기 때문에, 객체를 1개만 생성하고 공유하는 싱글톤 패턴을 사용한다.

---

</details>

<details>
   <summary>@Configuration과 싱글톤</summary>

<br/>

- `@Configuration`는 `@Bean`이 붙은 메서드마다 이미 스프링 빈이 존재하면 기존의 빈을 반환하고, 스프링 빈이 존재하지 않으면 스프링 빈을 새로 등록하고 반환하는 코드가 동적으로 만들어진다.
  - 참고로 `@Configuration`이 붙은 클래스도 스프링 빈으로 등록된다.
- 즉, `@Bean`만 사용해도 스프링 빈으로 등록되지만, 싱글톤을 보장하지 않는다.
---

</details>

<details>
   <summary>빈이란</summary>

<br/>

- 스프링 컨테이너가 생성하고 관리하는 자바 객체를 빈이라고 한다.
- `@Bean`나 `<bean>`로 설정 파일에 빈을 직접 등록하거나, 컴포너트 스캔을 이용하여 자동으로 등록할 수 있다.

---

</details>

<details>
   <summary>DI시 주입할 빈이 여러개인 경우</summary>

<br/>

- 스프링은 주입 대상을 타입으로 결정하지 못하면 필드 명이나 파라미터 명으로 매칭을 시도한다.
- 스프링은 이름을 직접적으로 변경하지 않고도 주입 대상을 결정할 수 있도록 `@Qulifier`과 `@Primary` 애노테이션을 제공한다.
  - `@Qualifier`를 주입 받는 곳에 적용시켜주면 동일한 `@Qualifier`가 적용된 빈이 주입된다.
  - `@Primary`가 붙은 빈이 우선적으로 적용된다. 하지만 `@Qualifier`가 `@Primary`보다 우선시된다.

---

</details>

<details>
   <summary>@Bean vs @Component</summary>

<br/>

- 둘 다 스프링 컨테이너에 빈을 등록하기 위해 사용한다.
- `@Bean` : 개발자가 작성한 method에 `@Bean`을 붙여주면, 해당 메서드가 반환하는 객체가 빈으로 등록된다.
  - `@Configuration`과 함께 사용해야 한다.
- `@Component` : 개발자가 작성한 클래스에 `@Component`를 붙여주면, 해당 클래스는 빈으로 등록된다.

---

</details>

<details>
   <summary>@Bean을 @Configuration과 함께 사용해야 하는 이유</summary>

<br/>

- `@Configuration`는 `@Bean`이 붙은 메서드마다 이미 스프링 빈이 존재하면, 존재하는 빈을 반환하도록 한다. 스프링 빈이 없으면, 새로 생성해서 빈으로 등록하는 코드가 동적으로 만들어진다.
- 즉, `@Bean`만 사용해도 스프링 빈으로 등록되지만, 싱글톤을 보장하지 않는다.

---

</details>

<details>
   <summary>@Component 종류</summary>

<br/>

- `@Controller` : 스프링 MVC 컨트롤러로 인식
- `@Repository` : 스프링 데이터 접근 계층으로 인식하고, 데이터 계층의 예외를 스프링 예외로 변환해준다.
- `@Configuration` : 스프링 설정 정보로 인식하고, 스프링 빈이 싱글톤을 유지하도록 추가 처리를 한다.
- `@Service` : `@Service` 는 특별한 처리를 하지 않는다. 대신 비즈니스 계층을 인식하는데 도움이 된다

---

</details>

<details>
   <summary>빈의 생명주기</summary>

<br/>

- 스프링 컨테이너 생성 -> 스프링 빈 생성 -> 의존관계 주입 -> 초기화 콜백 -> 사용 -> 소멸전 콜백 -> 스프링 종료
    - 초기화 콜백 : 빈 생성과 의존관계 주입이 완료된 후 호출
    - 소멸전 콜백 : 빈이 소멸되기 직전에 호출

---

</details>

<details>
   <summary>빈 생명주기 콜백 지원 방법</summary>

<br/>

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

<br/>

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

<br/>

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

<br/>

- 웹 페이지를 동적으로 생성하기 위해 사용하는 서버 프로그램이다.
- HTTP 요청 메시지 파싱하는 등의 부가적인 작업을 처리하여, 개발자가 비즈니스 로직에만 신경쓰도록 한다.

---

</details>

<details>
   <summary>서블릿 생성 시점</summary>

<br/>

- 서버 설정에 따라 다르다. 최초 요청 시점에 생성하게 할 수도 있고, 서블릿 컨테이너가 로딩될 때 생성하게 할 수도 있다.

---

</details>

<details>
   <summary>JSP와 Thymeleaf</summary>

<br/>

#### JSP
- HTML 코드에 자바 코드를 삽입하여, 동적으로 웹 페이지를 생성하는 서버 사이드 스크립트 언어이다.
- 서블릿으로 화면과 관련된 작업을 하면 상당히 복잡하기 때문에 등장하였다.
- 실행 시 서블릿으로 변환된다.

#### Thymeleaf
- 서버에서 HTML을 동적으로 렌더링 하는 용도로 사용하는 뷰 템플릿이다.
- 검증 오류 통합 기능과 폼 관리를 위한 추가 속성(`th:object`, `th:field`, `th:errors`, `th:errorclass`) 등 스프링과 통합된 다양한 기능을 제공한다.
  - 검증 오류 통합 기능
    - 스프링의 `BindingResult`를 활용해서 편리하게 검증 오류를 표현하는 기능을 제공한다.
    - `#fields` : `BindingResult`가 제공하는 검증 오류에 접근 가능
    - `th:errors` : 해당 필드에 오류가 있는 경우에 태그를 출력
    - `th:errorclass` : `th:field`에서 지정한 필드에 오류가 있으면 `class`정보를 추가
  - `th:object` : form에서 사용할 객체를 지정한다. 모델에 들어있는 데이터를 편하게 사용할 수 있다.
  - `th:field` : id, name, value 속성을 자동으로 만들어준다.

---

</details>

<details>
   <summary>서블릿 컨테이너</summary>

<br/>

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

<br/>

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

<br/>

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

<br/>

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

<br/>

- 리다이렉트
  - 클라이언트로 요청에 대한 응답이 나갔다가, redirect 경로로 새로 요청하는 것이다.
  - 클라이언트가 인지할 수 있고, URL 경로도 실제로 변경된다.
- 포워드
  - 서블릿이나 JSP가 요청을 받은 후 다른 서블릿이나 JSP로 처리를 위임하는 것이다.
  - 서버 내부에서 일어나는 호출이기 때문에 클라이언트가 전혀 인지하지 못한다.

---

</details>

<details>
   <summary>MVC 패턴</summary>

<br/>

- 모델, 뷰, 컨트롤러로 이루어진 디자인 패턴이다. 비즈니즈 로직은 Controller로, 화면을 그리는 일은 View로 분리한 다음에 뷰가 필요한 데이터는 Model에 담아서 넘긴다.
  - 모델 : 뷰에 출력할 데이터를 담아둔다.
  - 뷰 : 모델에 담겨있는 데이터를 기반으로 사용자가 볼 수 있는 화면을 말한다.
  - 컨트롤러 : 모델과 뷰를 잇는 다리 역할을 하며, 메인 로직을 담당한다.
- 장점
  - 앱의 구성 요소를 세 가지 역할로 구분하여 개발 프로세스에서 각각의 구성요소에만 집중해서 개발할 수 있다.
  - 재사용성과 확장성이 용이하다.
- 단점
  - 뷰와 모델 사이에 의존성이 높아서 애플리케이션이 복잡해질수록 모델과 뷰의 관계가 복잡해진다.

---

</details>

<details>
   <summary>프론트 컨트롤러 패턴</summary>

<br/>

- 서블릿 하나로 클라이언트 요청을 받고, 그에 맞는 컨트롤러를 찾아서 호출한다.
- 여러 개의 서블릿으로 처리할 때 중복되는 코드를 하나로 묶어서 관리한다.
    - 중복되는 코드 : view로 포워드, prefix, suffix
    - 간혹 사용하지 않는 request, response 객체도 존재한다.

---

</details>

<details>
   <summary>스프링 MVC의 요청 처리 과정</summary>

<br/>

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

---

</details>

<details>
   <summary>@Controller vs @RestController</summary>

<br/>

- `@Controller`는 뷰를 반환하기 위해 사용한다.
- `@RestController`는 `@Controller`와 `@ResponseBody`가 적용된 애노테이션으로, 데이터를 반환하기 위해 사용한다.

---
</details>

<details>
   <summary>메시지, 국제화</summary>

<br/>

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

---

</details>

<details>
   <summary>필터 & 인터셉터</summary>

<br/>

### 1. 필터
- 서블릿에 요청이 전달되기 전/후에 url 패턴에 맞는 모든 요청에 대해 부가 작업을 처리할 수 있는 기능을 제공한다.
    - 스프링의 경우 서블릿은 디스패쳐 서블릿이 해당된다.
- 필터에서 예외가 발생하면 `@ControllerAdvice`로 처리할 수 없다.
- 스프링 부트를 사용한다면, `FilterRegistrationBean`로 필터를 등록할 수 있다.
    - `ServletComponentScan`, `@WebFilter`는 필터 순서 조절이 안된다.
    - 서블릿 컨테이너가 필터를 싱글톤 객체로 생성하고, 관리한다.
- 다음 필터나 서블릿을 호출할 때 `request`, `response`를 다른 객체로 만들어 넘길 수 있다.

#### 필터 흐름
> HTTP 요청 -> WAS -> 필터 -> 서블릿 -> 인터셉터 -> 컨트롤러

1. 서블릿 컨테이너가 생성될 때 `init()`가 호출된다.
2. 고객의 요청이 올 때마다 `doFilter()`메서드가 호출된다.
3. 필터는 체인처럼 여러개로 추가할 수 있으며, 다음 필터가 없다면 서블릿을 호출한다.
   - 적절하지 않는 요청이라고 판단되면, 서블릿이 호출되지 않는다.
4. 이후 서블릿 컨테이너가 종료될 때 `destroy()`가 호출된다.

### 2. 인터셉터
- 스프링 MVC가 제공하는 기능으로, 디스패쳐 서블릿이 컨트롤러를 호출하기 전/후와 요청 완료 후에 추가적인 작업을 할 수 있도록 기능을 제공한다.
- 인터셉터에서 예외가 발생하면 `@ControllerAdvice`로 처리할 수 있다.
- 인터셉터는 `request`, `response` 뿐만 아니라, 어떤 컨트롤러가 호출되는지와 어떤 `modelAndView`가 반환되는지 알 수 있다.
- `WebMvcConfigurer`가 제공하는 `addInterceptors()`로 인터셉터를 등록할 수 있다.
    - 싱글톤처럼 사용되기 때문에 멤버변수를 사용하면 위험하다.
- [URL 경로 공식 문서](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/util/pattern/PathPattern.html)

#### 인터셉터 흐름
![image](https://user-images.githubusercontent.com/87891581/168583864-9db2087c-cf50-4516-b766-9dd181573cb0.png)
1. HTTP 요청이 들어오면, 디스패쳐 서블릿을 거쳐 `preHandle()`이 호출된다.
    - `preHandle()`의 응답값이 true면 다음으로 진행하고, false면 더이상 진행되지 않는다.
2. 컨트롤러를 거쳐 내부 로직 수행 후 `postHandle()`이 호출된다.
    - 컨트롤러에서 예외가 발생하면 `postHandle()`가 호출되지 않고 `ExceptionResolver`가 호출되어 예외 처리를 한다.
3. 뷰가 렌더링 된 후 `afterCompletion()`이 호출된다.
    - `afterCompletion()`은 예외가 발생하더라도 항상 호출된다.

---

</details>

<details>
   <summary>예외처리 방법 (feat. 내 프로젝트)</summary>

<br/>

- `@ModelAttribute`
  - 필드 관련 예외는 `Bean Validation`과 `BindingResult`가 제공하는 `rejectValue()`로 잡을 수 있다. 
  - 오브젝트 관련 예외는 `BindingResult`가 제공하는 `reject()`를 사용한다.
  - 예외를 모두 잡지 못한 경우를 위해 스프링 부트의 경우 `/errer` 경로에 에러 페이지를 만들어 놓으면, `BasicErrorController`가 에러 페이지를 자동으로 등록해준다.
- `@ResponseBody`
  - 간단한 필드 예외는 `Bean Validation`과 `@ExceptionHandler`의 조합으로 처리할 수 있다.
  - 이외에는 예외를 던지고 `@ExceptionHandler`로 처리한다.

---

</details>

<details>
   <summary>ExceptionResolver</summary>

<br/>

![image](https://user-images.githubusercontent.com/87891581/168731890-ab3c4b86-8dd9-4141-bc90-b24dd40c3068.png)
- 스프링 MVC는 컨트롤러(핸들러) 밖으로 던저진 예외를 해결하고, 동작 방식을 변경할 수 있도록 `ExceptionResolver`를 제공한다.
    - 컨트롤러에서 예외가 발생하면 `postHandle()`이 호출되지 않고, `ExceptionResolver`가 호출된다.
    - 일반적으로 `@ExceptionHandler`와 `@ControllerAdvice`를 사용하여 처리한다.
- 예외가 발생해도 서블릿 컨테이너까지 예외가 전달되지 않고, 스프링 MVC에서 예외 처리는 끝이난다.
    - 결과적으로 WAS 입장에서는 정상 처리가 되었다.

---

</details>

<details>
   <summary>컨버터 vs 포맷터</summary>

<br/>

- `Converter`는 타입에 제한이 없는, 범용 타입 변환 기능을 제공한다.
- `Formatter`는 문자에 특화된 컨버터로, 문자를 다른 객체로 변환하거나 객체를 문자로 변환하는 기능을 제공한다.

---

</details>

<details>
   <summary>파일 업로드</summary>

<br/>

- `multipart/form-data`방식은 다른 종류의 여러 파일과 폼의 내용을 함께 전송할 수 있다.
    - 일반적인 폼 데이터는 문자 형식, 파일은 바이너리 형식이다.
- 스프링이 지원하는 `MultipartFile`로 `multipart/form-data` 방식의 폼 데이터를 효과적으로 처리할 수 있다.
    - 업로드하는 HTML Form의 name에 맞추어 `@RequestParam`을 적용하거나, `@ModelAttribute`를 사용해도 된다.
    - 서블릿이 제공하는 `Part`는 `HttpServletRequest`를 사용해야 하고, 추가로 파일 부분만 구분하려면 여러가지 코드를 넣어야 한다.

---

</details>

<details>
   <summary>빈 후처리기</summary>

<br/>

- 빈 저장소에 등록할 목적으로 생성한 객체를 빈 저장소에 등록하기 직전에 조작하기 위해 사용한다.

---

</details>

<details>
   <summary>AOP</summary>

<br/>

- Aspect Oriented Programming, 관점 지향 프로그래밍
- 애플리케이션 로직은 핵심 기능과 부가 기능으로 나눌 수 있다.
    - 핵심 기능 : 해당 객체가 제공하는 고유의 기능. 핵심 비즈니스 로직.
    - 부가 기능 : 핵심 기능을 보조하기 위해 제공되는 기능. ex) 로그 추적 로직, 트랜잭션 로직
- 보통 부가 기능은 여러 클래스에 걸쳐서 사용되며, 이런 부가 기능을 횡단 관심사라고 한다.
- AOP는 횡단 관심사를 애스펙트로 모듈화하여 핵심 로직에서 분리하는 프로그래밍 방식을 말한다.
    - 애스펙트 : 부가 기능과, 부가 기능을 어디에 적용할지 정의한 것이다.

---

</details>

<details>
   <summary>AOP 적용 방식</summary>

<br/>

1. 컴파일 시점에 적용
   - 자바 파일이 `.class` 바이트 코드 파일로 컴파일되는 시점에 실제 대상 코드에 애스펙트를 통한 부가 기능 코드가 포함된다.
   - `AspectJ`가 사용하는 방법

2. 클래스 로딩 시점에 적용
   - `.class` 바이트 코드 파일을 JVM에 저장하기 전에 실제 대상 코드에 애스펙트를 통한 부가 기능 코드가 포함된다.
   - `AspectJ`가 사용하는 방법

3. 런타임 시점에 적용
   - `Spring AOP`가 사용하는 방법
   - 자바의 메인 메서드가 실행된 후 프록시를 통해 스프링 빈에 부가 기능을 적용한다.
       - 실제 대상 코드는 그대로 유지한다.
       - 프록시는 메서드 오버라이딩 개념으로 동작하기 때문에 메서드 실행 지점에만 AOP를 적용할 수 있다.

---

</details>

<details>
   <summary>AOP vs Interceptor vs filter</summary>

<br/>

- AOP vs Interceptor, Filter
  - 웹과 관련된 공통 관심사를 처리할 때는 Request와 Response 객체를 제공해주는 서블릿 필터와 스프링 인터셉터를 사용하는 것이 편리하다.
- Interceptor vs Filter
  - 문자 인코딩과 같이 전체적인 Request 단에서 어떤 처리가 필요하다면 Filter를 사용한다. 
  - 그렇지 않다면 스프링 MVC 구조에 특화된 필터 기능을 제공하는 인터셉터를 사용하는 것이 편리하다.

---

</details>

<details>
   <summary>JUnit5 vs JUnit4</summary>

<br/>

1. 단일 Jar에서 Platform, Jupiter, Vintage 세가지 모듈로 구성되도록 변경되었다.
   - Platform : 테스트를 실행해주는 런쳐 제공. TestEngine API 제공
   - Jupiter : JUnit5를 지원하는 TestEngine API 구현체
   - Vintage : JUnit 4와 3을 지원하는 TestEngine 구현체
2. JDK 요구사항이 Java5 이상에서 Java8 이상으로 변경
3. `@Before` -> `@BeforeEach` 등 애노테이션 명이 변경되고, `@Nested`와 같이 새로운 애노테이션이 추가되어 편리해졌다.

---

</details>

- 커넥션 풀
- DataSource
- 트랜잭션을 추상화하는 이유
- 트랜잭션 동기화 매니저
- 선언적 트랜잭션 vs 프로그래밍 방식 트랜잭션
- 
  Propagation 전파단계

<details>
   <summary>@Transactional</summary>

<br/>

1. 단일 Jar에서 Platform, Jupiter, Vintage 세가지 모듈로 구성되도록 변경되었다.
    - Platform : 테스트를 실행해주는 런쳐 제공. TestEngine API 제공
    - Jupiter : JUnit5를 지원하는 TestEngine API 구현체
    - Vintage : JUnit 4와 3을 지원하는 TestEngine 구현체
2. JDK 요구사항이 Java5 이상에서 Java8 이상으로 변경
3. `@Before` -> `@BeforeEach` 등 애노테이션 명이 변경되고, `@Nested`와 같이 새로운 애노테이션이 추가되어 편리해졌다.

</details>
