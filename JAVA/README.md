# JAVA
애노테이션에 대해서 설명해주세요.
클래스는 무엇이고 객체는 무엇인가요?
강한 결합과 느슨한 결합이 무엇인지 설명해주세요.
Mutable 객체와 Immutable 객체의 차이점에 대해 설명해주세요.
자바에서 null을 안전하게 다루는 방법에 대해 설명해주세요.



try with resources
제네릭
직렬화와 역직렬화
오버로딩, 오버라이딩
추상 클래스와 인터페이스 차이
Error, Exception
Checked Exception, Unchecked Exception
Java Collections
String, StringBuilder, StringBuffer
Blocking vs Non-Blocking
Sync vs Async
리플렉션
Stream
Fork Join Pool
람다식
Optional
자바8 추가된 내용
Java 8 -> Java 11
함수형 프로그래밍
멀티스레드 프로그래밍
Java 동기화 방식
Synchronized와 Lock & Condition 동기화
Atomic 동기화
hashcode

---

<details>
   <summary>Java 장단점</summary>

<br/>

- 장점
  - 운영체제에 독립적
      - JVM에서 동작하기 때문에 특정 운영체제에 종속적이지 않다.
  - 객체지향 언어
      - 캡슐화, 상속, 추상화, 다형성 등을 지원하여 객체 지향 프로그래밍이 가능
  - 동적 로딩을 지원
      - 애플리케이션이 실행될 때 모든 객체가 생성되지 않고, 각 객체가 필요한 시점에 클래스를 동적 로딩해서 생성된다. 또한 유지보수 시 해당 클래스만 수정하면 되기 때문에 전체 애플리케이션을 다시 컴파일할 필요가 없다. 따라서 유지보수가 쉽고 빠르다.
  - 자동으로 메모리 관리를 해준다.
- 단점
  - 비교적 느림
      - 한번의 컴파일링으로 실행 가능한 기계어가 만들어지지 않고 JVM에 의해 기계어로 번역되고 실행되는 과정을 거치기 때문에 조금 느리다.

---

</details>

<details>
   <summary>OOP(객체 지향 프로그래밍)</summary>

<br/>

- 상태와 행위를 가진 객체를 만들고, 객체 간의 상호작용을 통해 로직을 구성하는 프로그래밍 방법이다.
  - 객체란 현실세계의 실체 및 개념을 반영하는 상태(Status)와 행위(Behavior)를 정의한 데이터의 집합을 말한다. 
- 장점
  - 유지보수가 용이하다.
    - 절차 지향 프로그래밍에서는 코드를 수정해야할 때 일일이 찾아 수정해야하는 반면, 객체 지향 프로그래밍에서는 수정해야 할 부분이 클래스 내부에 멤버 변수 혹은 메서드로 존재하기 때문에 해당 부분만 수정하면 된다.
  - 코드의 재사용성이 높다.
      - 남이 만든 클래스를 가져와서 이용할 수 있고 상속을 통해 확장해서 사용할 수 있다.
  - 대형 프로젝트에 적합
    - 클래스 단위로 모듈화시켜서 개발할 수 있으므로 대형 프로젝트처럼 여러 명, 여러 회사에서 프로젝트를 개발할 때 업무 분담하기 쉽다.
- 단점
  - 처리속도가 상대적으로 느리다.
  - 설계 시 많은 시간과 노력이 필요

---

</details>

<details>
   <summary>OOP 특징</summary>

<br/>

- 캡슐화
  - 관련된 속성과 기능을 하나로 묶고, 실제로 구현되는 부분을 외부로 드러나지 않도록 하는 것을 말한다.
  - 정보 은닉 : 필요 없는 정보는 외부에서 접근하지 못하도록 제한
- 추상화 
  - 공통적인 속성이나 기능을 도출하는 것을 말한다.
- 상속
  - 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것이다.
  - 부모 클래스의 속성과 기능을 그대로 이어받아 사용하거나 기능의 일부분을 재정의하여 사용할 수 있다.
- 다형성
  - 변수나 메소드와 같은 프로그램의 요소들이 여러가지 형태를 가질 수 있는 것을 의미한다.
  - 부모 클래스 타입의 참조 변수로 자식 클래스 타입의 인스턴스를 참조하는 경우, 오버로딩, 오버라이딩이 해당된다.

---

</details>

<details>
   <summary>객체 지향 설계의 5가지 원칙(SOLID)</summary>

<br/>

1. SRP(Single Responsibility Principle) : 단일 책임 원칙
    - “한 클래스는 하나의 책임만 가져야 한다.”
    - 클래스를 변경하는 이유는 단 하나의 이유여야 한다.
    - ex) 객체의 생성과 사용을 분리
2. OCP(Open/Closed Principle) : 개방-폐쇄 원칙
    - “소프트웨어의 요소는 확장에는 열려있으나 변경에는 닫혀 있어야 한다.”
    - 요구 사항의 변경이나 추가 사항이 발생하더라도, 기존 구성 요소에는 수정이 일어나지 않고, 기존 구성 요소를 쉽게 확장해서 재사용한다.
3. LSP(Liskov Substitution Principle) : 리스코프 치환 원칙
    - “프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.”
    - ex) 자동차 인터페이스의 엑셀이 앞으로 가라는 기능인 경우, 뒤로 가게 구현하면 LSP 위반이다. 느리더라도 앞으로 가야한다.
4. ISP(Interface segregation Principle) : 인터페이스 분리 원칙
    - “특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.”
    - 인터페이스는 그 인터페이스를 사용하는 클라이언트를 기준으로 분리해야 한다.
    - SRP가 클래스의 단일 책임이라면, ISP는 인터페이스의 단일 책임이다.
    - ex) 자동차 인터페이스를 운전 인터페이스와 정비 인터페이스로 분리한다. 또한, 사용자 클라이언트도 운전자 클라이언트와 정비사 클라이언트로 분리한다.
5. DIP(Dependency Inversion Principle) : 의존관계 역전 원칙
    - “구체화에 의존하면 안되며, 추상화에 의존해야 한다.”
    - 상위 모델은 하위 모델에 의존하면 안된다.
    - 쉽게 말해 구현 클래스에 의존하지 말고, 인터페이스에 의존하라는 뜻이다.

---

</details>

<details>
   <summary>객체 지향 프로그래밍 vs 절차 지향 프로그래밍</summary>

<br/>

+ 절차 지향 프로그래밍
    - 실행하고자 하는 절차를 정하고, 절차대로 프로그래밍 하는 방식이다.
    - 실행 속도가 빠르지만, 유지보수와 디버깅이 어렵다는 단점이 있다.
+ 객체 지향 프로그래밍
    - 상태와 행위를 가진 객체를 만들고, 객체 간의 상호작용을 통해 로직을 구성하는 프로그래밍 방법이다.
    - 코드의 재사용성이 높고 유지보수가 용이하지만, 처리 속도가 상대적으로 느리다는 단점이 있다.

---

</details>

<details>
   <summary>JVM</summary>

<br/>

- 자바 프로그램을 실행하는 역할을 가진 자바 가상 머신
- 컴파일러를 통해 바이트 코드로 변환된 파일을 JVM에 로딩하여 실행

---

</details>

<details>
   <summary>JVM의 구성 요소</summary>

<br/>

JVM은 크게 Class Loader, Execution engine, Runtime Data Area 세가지로 구성된다.

#### 1. 클래스 로더
- Runtim시에 JVM내로 클래스(.class 파일)를 로드하고 링크를 통해 배치하는 작업을 수행한다. (Runtime : 클래스를 처음으로 참조할 때.)
- 동적 로드를 담당한다.
#### 2. 실행 엔진
- 메모리(Runtime Data Area)에 적재된 클래스들을 기계어로 해석해 실행
- 구성
  - 인터프리터: 바이트 코드 명령어를 하나씩 읽어서 해석하고 실행한다.
  - JIT 컴파일러: 인터프리터 효율을 높이기 위한 컴파일러이다. 기본적으로 인터프리터를 사용하지만, 반복적인 코드는 JIT 컴파일러가 처리한다.
  - GC(Garbage Collector): 힙 메모리에서 참조되지 않는 개체들 제거
#### 3. Runtime Data Area
- 프로그램 실행 중에 사용되는 메모리 영역이다.
- 힙과 Method Area는 모든 쓰레드가 공유하는 영역이다.
- 구성
  - PC Register
    - Thread가 시작될 때 각각의 Thread 별로 생성되는 공간으로, 현재 수행 중인 JVM 명령어 주소를 가진다.
  - Stack Area
    - 메서드 실행과 관련된 정보를 저장하는 영역
    - 메서드 매개 변수, 지역 변수 등을 저장한다.
  - Natvie Method Stack
    - Java외의 언어로 작성된 네이티브 코드를 위한 영역이다.
    - 자바 프로그램이 컴파일 되어 생성되는 바이트 코드가 아닌 실제 실행할 수 있는 기계어로 작성된 프로그램을 실행시키는 영역이다.
  - Heap Area
    - 동적으로 생성된 객체와 배열이 저장하는 영역
    - GC의 관리 대상이다.
  - Method Area
    - 클래스 정보를 처음 메모리 공간에 올릴 때 초기화되는 대상을 저장하기 위한 메모리 공간.
    - 필드 정보, 메소드 정보, Type 정보를 보관한다.
    - Runtime Constant Pool이라는 것이 존재하며, 상수 자료형을 저장하여 참조하고 중복을 막는 역할을 수행한다.

---

</details>

<details>
   <summary>자바 실행 과정</summary>

<br/>

- 자바 컴파일러(javac)가 자바 소스코드(.java)을 클래스 파일(.class)로 변환시킨다.
- 클래스 로더는 클래스 파일을 런타임 데이터 영역에 로드한다.
- 실행 엔진이 로딩된 클래스 파일을 해석하고 실행한다.

---

</details>

<details>
   <summary>가비지 컬렉터</summary>

<br/>

- 동적으로 할당된 영역에서 참조되지 않는 객체를 제거한다.
- GC는 크게 Young generation에서 일어나는 Minor GC와 Old generation에서 발생하는 Major GC로 구분된다.
- 기본적으로 Mark And Sweep 방식으로 GC를 진행한다.
  - 변수가 참조하는 객체를 시작으로 그래프 순회를 통해 접근 가능한 객체를 판별한다. 접근하지 못하는 객체는 제거한다.
  - 단순히 참조되고 있는 횟수로 판단하는 방식은 순환 참조 되는 객체를 제거할 수 없다.

**동작 과정**
1. 새로운 객체 생성은 Heap의 Eden 영역에 저장 
2. Eden 영역이 꽉차면 Minor GC가 수행되고, Reachable 객체는 Survival 0 영역으로 이동과 동시에 age-bit 1 상승 
3. 2번 과정이 반복되면서 Survival 1 -> 0 -> 1 이동이 반복 
4. age-bit가 일정 값 이상이 되면 해당 객체에 대해 promotion 과정이 진행되어 Old Generation 영역으로 이동 
5. Old Generation 영역이 꽉차면 Major GC가 발생
---

</details>

<details>
   <summary>접근 제어자</summary>

<br/>

- 멤버나 클래스에 사용되며, 외부에 보여주고 싶은 정보를 선택적으로 제공하기 위해 사용한다.
- 종류
  - private : 같은 클래스 내에서만 접근이 가능하다.
  - default : 같은 패키지 내에서만 접근이 가능하다.
      - 멤버나 클래스에 접근 제어자가 지정되어 있지 않다면, 접근 제어자가 default임을 뜻한다.
  - protected : 같은 패키지 내에서, 그리고 다른 패키지의 자손 클래스에서 접근이 가능하다.
  - public : 접근 제한이 전혀 없다.

---

</details>

<details>
   <summary>String vs char</summary>

<br/>

- char는 문자 하나를 저장하는 기본 타입이다.
- String은 문자열을 저장하는 참조 타입이다.
- char는 ==을 사용하여 값을 비교할 수 있지만, String은 값이 같더라도 주소값이 다를 수 있기 때문에 equals()로 비교해야 한다.

---

</details>

<details>
   <summary>동일성과 동등성</summary>

<br/>

- 동일성은 객체의 주소값를 비교하는 것이고, 동등성은 객체 내부의 값을 비교하는 것이다.
- ==을 사용하여 주소값을 비교할 수 있고, equals()를 사용하여 값을 비교할 수 있다.

---

</details>

<details>
   <summary>기본 타입과 참조 타입</summary>

<br/>

+ 기본 타입
    - 논리형, 문자형, 정수형, 실수형으로 구성되며, 실제 값을 저장하는 타입이다.
      - 정수형 : byte(1), short(2), int(4), long(8)
      - 실수형 : float(4), double(8)
      - 논리형 : boolean(1)
      - 문자형 : char(unsigned 2)
    - 변수 선언부는 Stack 영역에 저장되고, 변수에 저장된 상수는 Runtime Constant Pool에 저장된다.
+ 참조 타입(Reference Type)
    - 기본형을 제외한 나머지 타입을 말한다.
    - Heap 영역에서 생성된 데이터의 주소값을 변수가 참조하는 방식이다. 
      - 변수 : Stack의 로컬 변수, Method Area의 Static 변수
    - String과 배열은 일반적인 참조 타입과 달리 new 없이 생성 가능하지만 참조타입이다.
    - 더이상 참조하는 변수가 없을 때 GC에 의해 삭제된다.

---

</details>

<details>
   <summary>Call By Value와 Call By Reference</summary>

<br/>

+ Call By Value(값에 의한 호출)
    - 함수 호출시 인자로 전달되는 변수의 값을 복사하여 함수의 파라미터로 전달한다.
    - 따라서 함수 안에서 파라미터 값이 변경되더라도, 인자로 전달된 변수의 값은 변하지 않는다.
+ Call by Reference(참조에 의한 호출)
    - 함수 호출 시 인자로 전달되는 변수의 레퍼런스를 전달한다.
    - 따라서 함수 안에서 파라미터 값이 변경되면, 인자로 전달된 변수의 값도 함께 변경된다.

자바는 Call By Value이다. 참조 타입의 경우에도 주소값을 복사해서 넘기는 것이다.

---

</details>

<details>
   <summary>Wrapper class</summary>

<br/>

- 8개의 기본 타입에 해당되는 데이터를 객체로 포장해주는 클래스를 말한다.
- 산술 연산을 위해 정의된 클래스가 아니므로, 인스턴스에 저장된 값을 변경할 수 없다.
- DB로부터 기본타입에 null값이 들어올 수 있는 경우에 사용하면 유용하다.

---

</details>

<details>
   <summary>박싱과 언박싱</summary>

<br/>

- 기본 타입의 데이터를 래퍼 클래스의 인스턴스로 변환하는 과정을 박싱이라고 한다.
- 래퍼 클래스의 인스턴스에 저장된 값을 다시 기본 타입의 데이터로 꺼내는 과정을 언박싱이라고 한다.
- JDK 1.5부터 박싱과 언박싱이 필요한 상황에서 자바 컴파일러가 자동으로 처리해준다.
  - 단, 래퍼 클래스 간에 값 비교로 ==을 사용하면 안된다.

---

</details>

<details>
   <summary>non-static vs static</summary>

<br/>

+ non-static
    - 공간적 특성
        - 객체마다 별도로 존재하고 인스턴스 변수라고 부른다.
    - 시간적 특성
        - 객체와 생명주기가 동일하다.
+ static
    - 공간적 특성
        - 클래스당 하나만 생성되며, 클래스 변수라고 부른다.
        - 동일한 클래스의 모든 객체들에 의해 공유된다.
    - 시간적 특성
        - 클래스 로딩 시 생성되므로 객체를 생성하지 않고 사용할 수 있다.
        - 프로그램 종료시에 사라진다.

---

</details>

<details>
   <summary>main이 static인 이유</summary>

<br/>

- static 멤버는 프로그램 시작 시(클래스 로딩) 메모리에 로드되어 인스턴스를 생성하지 않아도 호출이 가능하다. JVM은 인스턴스가 없는 클래스의 `main()`을 호출해야 하기 때문에 static이어야 한다.
+ 실행 과정
    - 코드를 실행하면 컴파일러가 자바 소스코드를 클래스 파일로 변환
    - 클래스 로더가 클래스 파일을 메모리 영역에 로드
    - Runetime Data Area 중 Method Area(=Class area, Static area)라고 불리는 영역에 Class Variable이 저장되는데, static 변수도 여기에 포함
    - JVM은 Method Area에 로드된 main()을 실행

---

</details>

<details>
   <summary>final vs finally vs finalize</summary>

<br/>

+ final 키워드
    - 변수, 메서드 클래스가 __변경 불가능__ 하도록 만든다.
    - 기본 타입 변수에 적용 시
        - 해당 변수의 값 변경 불가능하다.
    - 참조 변수에 적용 시
        - 참조 변수가 다른 객체를 가리키도록 변경할 수 없다.
    - 메서드에 적용 시
        - 해당 메서드를 오버라이드할 수 없다.(오버로딩은 가능)
    - 클래스에 적용 시
        - 해당 클래스를 상속 받아서 사용할 수 없다.
+ finally 키워드
    - try catch 블록이 종료될 때 항상 실행될 코드 블록을 정의하기 위해 사용한다.
+ finalize 메서드
    - 가비지 컬렉터가 참조되지 않는 객체를 메모리에서 제거하겠다고 결정하는 순간 호출된다.
    - Object 클래스에 존재한다.

---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>

<details>
   <summary></summary>

<br/>



---

</details>
