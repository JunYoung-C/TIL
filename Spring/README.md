# Spring
- 프레임워크와 라이브러리
- EJB와 POJO
- Spring 정의 및 장점
- 스프링 부트란
- IoC
- DI (Dependency Injection)
  - 주입 방식
- 스프링 컨테이너
- 스프링이 싱글톤을 지원하는 이유
- @Configuration과 싱글톤
- 빈이란
  - 생명주기
  - 생명주기 콜백 지원 방법
  - 스코프
- Entity, VO, DTO, DAO

빈 후처리기
AOP
디자인 패턴
로깅 라이브러리

- 웹 서버와 웹 애플리케이션 서버
- 서블릿
- 서블릿 컨테이너
- MVC 패턴
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

### 프레임워크와 라이브러리
<details>
   <summary>답안 보기</summary>

- 프레임워크 : 원하는 기능 구현에 집중하여 개발할 수 있도록, 일정한 형태와 필요한 기능을 갖추고 있는 골격, 뼈대를 의미한다.
- 라이브러리 : 자주 사용되는 로직을, 재사용이 편리하도록 잘 정리한 코드의 집합을 말한다.
- 프레임워크는 사용자가 작성한 코드를 프레임워크가 직접 제어하고, 대신 실행한다. 하지만 라이브러리는 사용자가 작성한 코드가 직접 제어의 흐름을 담당한다.

</details>

---

### EJB
<details>
   <summary>답안 보기</summary>

- Enterprise JavaBeans
- 기업 환경의 시스템을 구현하기 위한 서버측 컴포넌트 모델이다.
- 복잡하고 객체지향적이지 않다는 단점 등으로 인해 스프링이 등장하였다.

</details>

---

### POJO
<details>
   <summary>답안 보기</summary>

- Plain Old Java Object
- 특정 기술 규약과 환경에 종속되지 않은 순수한 자바 오브젝트를 말한다.
- 코드가 간결하고 테스트가 용이하다는 장점이 있다.

</details>

---

### Spring이란
<details>
   <summary>답안 보기</summary>

- 자바 엔터프라이즈 개발을 편하게 해주는 경량급 오픈소스 애플리케이션 프레임워크이다.
- 특징
  - POJO 기반으로 구성되어 코드가 간결하고 테스트가 용이하다.
  - DI를 통해 객체 관계를 구성한다.
  - AOP를 지원하여 개발자가 핵심 비즈니스 로직에 집중할 수 있도록 한다.
  - MVC 구조를 웹을 개발할 수 있도록 지원한다.

</details>

---

### 스프링 부트란
<details>
   <summary>답안 보기</summary>

- 스프링을 복잡한 설정 없이 쉽고 빠르게 만들어주는 프레임워크이다.

</details>

---

### IoC
<details>
   <summary>답안 보기</summary>

- Inversion Of Control, 제어의 역전
- 객체의 생성에서부터 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀐 것을 말한다.
- 개발자가 프레임워크에 필요한 부분을 개발하고 조립하면, 코드의 최종 호출은 프레임워크에 의해 이뤄진다. 

</details>

---

### DI (Dependency Injection)
<details>
   <summary>답안 보기</summary>

- Dependency Injection, 의존관계 주입 or 의존성 주입
- Spring 프레임워크에서 지원하는 IoC의 형태로, 클래스 사이의 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 연결해 주는 것을 말한다.

</details>

---

### DI 주입 방식
<details>
   <summary>답안 보기</summary>

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

</details>

---

### 스프링 컨테이너
<details>
   <summary>답안 보기</summary>

- BeanFactory와 ApplicationContext를 스프링 컨테이너라고 한다.
  - BeanFactory는 빈을 관리하고 조회하는 역할을 한다.
  - BeanFactory를 상속한 ApplicationContext는 빈 관리 기능뿐만 아니라, 국제화 등의 추가적인 기능을 제공한다.

</details>

---

### 스프링이 싱글톤을 지원하는 이유
<details>
   <summary>답안 보기</summary>

- 대부분의 스프링 애플리케이션은 웹 애플리케이션이다. 웹 애플리케이션은 보통 여러 고객이 여러 요청을 한다.
- 싱글톤을 사용하지 않으면 각 요청마다 새로운 객체가 생성되고 소멸된다. 이 방식은 트래픽이 증가할수록 메모리 낭비가 심하기 때문에, 객체를 1개만 생성하고 공유하는 싱글톤 패턴을 사용한다.

</details>

---

### @Configuration과 싱글톤
<details>
   <summary>답안 보기</summary>

- `@Configuration`는 `@Bean`이 붙은 메서드마다 이미 스프링 빈이 존재하면 존재하는 빈을 반환하고, 스프링 빈이 없으면 생성해서 스프링 빈으로 등록하고 반환하는 코드가 동적으로 만들어진다.
  - `@Bean`만 사용해도 스프링 빈으로 등록되지만, 싱글톤을 보장하지 않는다.
  - `@Configuration`이 붙은 클래스도 스프링 빈으로 등록된다.

</details>

---

### 빈이란
<details>
   <summary>답안 보기</summary>

- 스프링 컨테이너가 생성하고 관리하는 자바 객체를 빈이라고 한다.
- `@Bean`나 `<bean>`로 설정 파일에 빈을 직접 등록하거나, 컴포너트 스캔을 이용하여 자동으로 등록할 수 있다.

</details>

---

### 빈의 생명주기
<details>
   <summary>답안 보기</summary>

- 스프링 컨테이너 생성 -> 스프링 빈 생성 -> 의존관계 주입 -> 초기화 콜백 -> 사용 -> 소멸전 콜백 -> 스프링 종료
    - 초기화 콜백 : 빈 생성과 의존관계 주입이 완료된 후 호출
    - 소멸전 콜백 : 빈이 소멸되기 직전에 호출

</details>

---

### 빈 생명주기 콜백 지원 방법
<details>
   <summary>답안 보기</summary>

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

</details>

---

### 빈 스코프
<details>
   <summary>답안 보기</summary>

- 빈이 존재할 수 있는 범위를 의미하며, 스프링은 다양한 스코프를 지원한다.
1. 싱글톤
   - default 스코프다.
   - 빈이 스프링 컨테이너의 시작과 종료까지 유지된다. 
2. 프로토타입
   - 스프링 컨테이너가 빈의 생성과 의존관계 주입, 초기화끼지만 관여한다.
   - 싱글톤 빈은 한번만 생성되지만, 프로토타입 빈은 요청할 때마다 생성된다.
3. 웹 스코프
   - request : HTTP 요청이 들어오고 나갈때까지 유지되는 스코프
   - session : HTTP 세션과 동일한 생명주기를 가지는 스코프
   - application : 서블릿 컨텍스트와 동일한 생명주기를 가지는 스코프
   - websocket : 웹 소켓과 동일한 생명주기를 가지는 스코프
     - 웹 소켓 : 클라이언트와 서버가 양방향 소통을 가능하게 하는 프로토콜

</details>

---

### Entity, VO, DTO, DAO
<details>
   <summary>답안 보기</summary>



</details>

---

### 템플릿
<details>
   <summary>답안 보기</summary>



</details>

---

### 템플릿
<details>
   <summary>답안 보기</summary>



</details>

---

### 템플릿
<details>
   <summary>답안 보기</summary>



</details>

---

### 템플릿
<details>
   <summary>답안 보기</summary>



</details>

---

### 템플릿
<details>
   <summary>답안 보기</summary>



</details>

---

### 템플릿
<details>
   <summary>답안 보기</summary>



</details>

---

### 템플릿
<details>
   <summary>답안 보기</summary>



</details>

---

### 템플릿
<details>
   <summary>답안 보기</summary>



</details>

---



