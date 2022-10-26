# JAVA

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
   <summary>클래스 객체 인스턴스의 차이</summary>

<br/>

- 클래스(Class)
  - 객체를 만들어 내기 위한 설계도 혹은 틀
  - 연관되어 있는 변수와 메서드의 집합
- 객체(Object)
  - 소프트웨어 세계에 구현할 대상
  - '클래스의 인스턴스(instance)' 라고도 부른다.
  - 객체는 모든 인스턴스를 대표하는 포괄적인 의미를 갖는다.
- 인스턴스(Instance)
  - 설계도를 바탕으로 소프트웨어 세계에 구현된 구체적인 실체
  - 실체화된 인스턴스는 메모리에 할당된다.
  - 인스턴스는 객체에 포함된다고 볼 수 있다.
  - 객체는 현실 세계에 가깝고, 인스턴스는 소프트웨어 세계에 가깝다.

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
  - 부모 타입의 변수가 자식 타입의 인스턴스를 참조하는 경우, 오버로딩, 오버라이딩이 해당된다.

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
  - Native Method Stack
    - Java외의 언어로 작성된 네이티브 코드를 위한 영역이다.
    - 자바 프로그램이 컴파일 되어 생성되는 바이트 코드가 아닌 실제 실행할 수 있는 기계어로 작성된 프로그램을 실행시키는 영역이다.
  - Heap Area
    - 동적으로 생성된 객체와 배열이 저장하는 영역
    - GC의 관리 대상이다.
  - Method Area
    - 클래스 파일이 로딩되는 영역이다. 
    - 인터페이스인지 클래스인지와 같은 Type 정보와 필드 정보, 메소드 정보를 보관하고 static 변수를 초기화하여 저장한다.
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
   <summary>java9의 default GC</summary>

<br/>



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
   <summary>해시 코드</summary>

<br/>

- 임의의 길이를 가진 데이터를 고정된 크기로 변환한 후 다른 객체와 동일한 객체인지 확인하는 정수값

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
    - 변수, 메서드, 클래스가 __변경 불가능__ 하도록 만든다.
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
   <summary>try with resources</summary>

<br/>

기존에는 try 구문에서 생성한 리소스를 finally 구문에서 직접 해제해 주어야 했다. 매번 자원 해제를 위한 중복 코드가 발생하고, 실수로 자원 해제를 누락시키면 프로그램이 오작동할 우려가 있다. 

이를 해결하기 위해 자바 7 이후부터 try with resources 구문을 지원한다. try 옆 괄호 안에서 리소스를 생성해주면 따로 반납하지 않아도 리소스를 자동으로 반납한다.  

추가로, 자바 9 버전에서는 try() 문 안에 명시적으로 객체 선언을 하기보다는 try 문 바깥에서 객체 선언을 하고 생성된 인스턴스의 변수를 넣어줄 수 있도록 바뀌었다.

---

</details>

<details>
   <summary>제네릭</summary>

<br/>

+ 클래스나 메서드에서 사용할 내부 데이터 타입을 외부에서 지정하는 기법
+ 객체의 타입을 컴파일 시에 체크하기 때문에 객체의 타입 안전성을 높이고 형변환의 번거로움을 줄여준다.
  + 타입 안정성을 높인다는 것은 객체를 컬렉션에 저장하거나 꺼내올 때 의도하지 않은 타입으로 형변환 되는 것을 막는다는 말이다.

---

</details>

<details>
   <summary>직렬화와 역직렬화</summary>

<br/>

+ 직렬화
    - 자바 시스템 내부에서 사용되는 객체 또는 데이터를 외부의 자바 시스템에서도 사용할 수 있도록 바이트 형태로 데이터를 변환하는 기술
    - 조건
        - 자바 기본 타입
        - Serializable 인터페이스 상속받은 객체
    - ObjectOutputStream 객체를 이용하여 직렬화
+ 역직렬화
    - 바이트로 변환된 데이터를 다시 객체로 변환하는 기술
    - 조건
      - 직렬화 대상이 된 객체의 클래스가 클래스 패스에 존재해야 하며 import 되어 있어야 한다.
      - 자바 직렬화 대상 객체는 동일한 serialVersionUID 를 가지고 있어야 한다.
        - `private static final long serialVersionUID = 1L;`
    - ObjectInputStream 객체를 이용하여 역직렬화

---

</details>

<details>
   <summary>오버로딩, 오버라이딩</summary>

<br/>

+ 오버로딩
    - 한 클래스 내에 같은 이름의 메서드를 여러 개 정의하는 것을 오버로딩이라고 한다.
    - 이름이 같은 메서드들은 서로 매개변수의 개수나 타입이 달라야 한다.
      - 반환타입만 다른 경우는 오버로딩이 아니다.
+ 오버라이딩
    - 상위 클래스 혹은 인터페이스에 존재하는 메소드를 하위 클래스에서 필요에 맞게 재정의하는 것을 의미한다.
  - 오버라이딩하는 메서드는 상위 클래스의 메소드의 이름, 매개변수, 반환타입이 같아야 한다.

---

</details>

<details>
   <summary>추상 클래스와 인터페이스 차이</summary>

<br/>

+ 추상 메서드
    - abstract 키워드와 선언부만 작성하고 구현부는 작성하지 않은 메서드
      - 선언부는 리턴 타입, 메서드 이름, 매개 변수로 구성된다.
+ 추상 클래스
    - abstract 키워드로 선언된 클래스로, 추상 메서드뿐만 아니라 생성자, 멤버 변수, 메서드를 가질 수 있다.
      - 추상 메서드가 없어도 상관없지만, 어떤 경우든 추상 클래스로 인스턴스를 생성할 수 없다.
    - 목적
        - 관련성이 높은 클래스 간의 공통적인 부분을 추상화하여, 상속하는 클래스에게 구현을 강제하고 기능을 확장하는 용도로 사용하기 위함.
+ 인터페이스
  - 일종의 추상 클래스로, class 키워드 대신 interface 키워드로 선언한다.
    - 모든 멤버 변수는 `public static final`이어야 하며, 이를 생략할 수 있다.
    - 모든 메서드는 추상메서드이며, `abstract public`를 생략할 수 있다. 단, JDK 1.8부터 static 메서드와 default 메서드가 추가되었다.
    - 다중 상속이 가능하다.
  - 목적
    - 관련성이 낮은 클래스들이 논리적으로 같은 기능을 가지는 경우 구현을 강제하기 위함.

---

</details>

<details>
   <summary>애노테이션</summary>

<br/>

- 애노테이션은 인터페이스를 기반으로 한 문법으로, 주석처럼 코드에 달아 클래스에 특별한 의미를 부여하거나 기능을 주입할 수 있다.
  - 리플렉션 기술을 활용하여, 특정 애노테이션이 붙은 멤버에 의존성을 주입하는 등의 작업을 할 수 있다.
- `@Target`과 같이 애너테이션을 정의할 때 사용하는 메타 애너테이션이 있다.

---

</details>

<details>
   <summary>Error, Exception</summary>

<br/>

![그림3](https://backtony.github.io/assets/img/post/interview/java-3.PNG)

- 에러
  - 스택 오버 플로우나 메모리 부족과 같이 복구할 수 없는 심각한 오류이다.
  - 런타임에 발생한다.
- 예외
  - 프로그래머가 try catch로 수습할 수 있는 오류이다.
  - 컴파일 시점에 발생하는 Checked Exception과 런타임 시점에 발생하는 Unchecked Exception으로 나뉜다.

---

</details>

<details>
   <summary>Checked Exception, Unchecked Exception</summary>

<br/>

- Checked Exception
  - IOException, SQLException 등 컴파일 시점에 발생하는 예외이다.
  - 사용하는 모든 곳에 throws를 명시해야하는데, 이는 의존성 문제를 야기한다.
- Unchecked Exception
  - NullPointException과 같이 런타임 시점에 발생하는 예외이다.
  - Exception 클래스 하위 RuntimeException 클래스를 상속받는다.

---

</details>

<details>
   <summary>Java Collections</summary>

<br/>

![그림1](https://backtony.github.io/assets/img/post/interview/java-1.PNG)  
- 다량의 데이터를 효율적으로 관리할 수 있도록 표준화한 클래스들을 말한다.
- 크게 List와 Set이 상속한 Collection 인터페이스와 Map 인터페이스로 나뉜다. 
+ Map
    - Key와 Value의 쌍으로 이루어진 데이터 집합
    - 순서를 유지하지 않는다.
    - Key는 중복이 허용되지 않고, Value는 중복을 허용한다.
+ Collection
    + Collection은 Iterator 인터페이스를 상속한다.
    - List
      - 순서가 있는 데이터 집합
      - 데이터 중복을 허용한다.
    - Set
        - 순서를 유지하지 않는 데이터 집합
        - 데이터 중복을 허용하지 않는다.

<br>

---

</details>

<details>
   <summary>Map 구현체 종류</summary>

<br/>

+ HashMap
  + key와 value를 묶은 entry의 배열로 저장되며, 배열의 인덱스는 내부 해쉬 함수를 통해 계산된다.
  - key와 value에 null값을 허용 한다.
  - 비동기 처리
+ LinkedHashMap
    - HashMap에 저장 순서 유지 기능을 추가하였다.
    - 비동기 처리
+ TreeMap
  + 이진 검색 트리의 형태로 키와 값의 쌍으로 이루어진 데이터를 저장한다.
      - 내부적으로 __레드-블랙 트리(균형 이진 탐색 트리)__ 로 저장된다.
  - 범위 검색이나 정렬이 필요한 경우 HashMap 대신 TreeMap을 사용한다.
  - 키값에 대한 Compartor 구현으로 정렬 방법을 지정할 수 있다.
+ ConCurrentHashMap
    - key,value에 null값 비허용
    - __쓰기작업에서만 동기 처리__
+ HashTable
    - key,value에 null값 비허용
    - __모든 작업에 동기 처리__

---

</details>

<details>
   <summary>Set 구현체 종류</summary>

<br/>

+ HashSet
    - 저장 순서를 유지하지 않고 중복을 허용하지 않는 데이터의 집합
    - 해시 알고리즘을 사용하여 검색 속도가 매우 빠르다.
    - 내부적으로 HashMap 인스턴스를 이용하여 요소를 저장한다.
+ LinkedHashSet
    - HashSet에 저장 순서 유지 기능 추가
+ TreeSet
    - 데이터가 정렬된 상태로 저장되는 이진 탐색 트리의 형태로 요소를 저장한다.
      - 이진 탐색 트리의 성능을 향상시킨 레드-블랙 트리(Red-Black tree)로 구현되어 있다.
    - Compartor 구현으로 정렬 방법을 지정할 수 있다.

---

</details>

<details>
   <summary>List 구현체 종류</summary>

<br/>

+ ArrayList
    - 내부적으로 배열을 이용해서 데이터를 순차적으로 저장한다.
    - 배열에 저장할 공간이 없으면 더 큰 배열을 생성해서 기존 배열의 값을 복사하여 사용한다.
      - 재할당 시 크기가 두 배로 증가한다.
    - 데이터 삽입, 삭제 시 해당 데이터 이후 모든 데이터가 복사되므로, 삽입과 삭제가 빈번히 일어나는 경우에는 부적합하다.
    - 검색의 경우는 인덱스의 데이터를 가져오면 되므로 빠르다.
+ LinkedList
    - 불연속적으로 존재하는 데이터를 서로 연결한 형태로 되어있다.
    - 데이터의 삽입이나 삭제 시 데이터 이동 없이 주소지만 변경하면 되므로 삽입, 삭제가 빈번한 데이터에 적합하다.
    - 데이터의 검색 시 처음부터 노드를 순회하므로 검색에는 부적합하다.
    - 큐, 양방향 큐를 만들기 위한 용도로 사용한다.
+ Vector
    - 내부에서 자동으로 동기처리가 일어난다.
    - 성능이 좋지 않아 잘 사용하지 않는다.
    - 재할당 시 크기가 두 배로 증가한다.
+ Stack
  + 후입선출 구조로 데이터를 저장한다.
  - new 키워드로 직접 사용 가능
  - Vector를 상속받아 동기 처리

---

</details>

<details>
   <summary>String, StringBuilder, StringBuffer</summary>

<br/>

+ String
    - String은 문자열을 저장하는 참조 타입이다.
    - String에 저장되는 문자열은 private final 배열 형태이므로 값을 변경할 수 없다.
      - char[]을 byte[]로 변환하여 저장한다.
    - 문자열 연산 시 새로 객체를 만드는 Overhead가 발생한다.
+ StringBuilder, StringBuilder
  + 공통점
    + new 연산으로 객체를 한번만 생성한다.
    + 문자열 연산 시 내부적으로 사용되는 배열에 값을 추가하고, 배열이 꽉차면 더 큰 배열을 생성한 후 기존 값을 복사하여 사용한다.
    + StringBuilder와 StringBuffer 클래스의 메서드는 동일하다.
  + 차이점
    + StringBuilder는 비동기 처리, StringBuffer는 동기 처리 

- 결론
  - String은 문자열 연산이 적으면 사용한다.
  - StringBuilder는 문자열 연산이 많은 Single-Thread 환경에서 사용한다.
  - StringBuffer는 문자열 연산이 많은 Multi-Thread 환경에서 사용한다.

---

</details>

<details>
   <summary>String new와 리터럴("") 차이</summary>

<br/>

- String은 new 연산자나 리터럴("")를 사용하여 새로운 객체를 생성할 수 있다.
- new 연산자로 생성하면, 값이 같더라도 매번 새로운 객체를 생성한다.
  - `intern()` 메서드를 사용하면 String Constant Pool로 이동시키거나, 이미 존재한다면 해당 문자열을 반환한다.
- 리터럴("")은 처음에만 새로운 객체를 생성하고, 이미 존재하는 String 값이라면 재사용한다.
  - Heap 영역 내의 String Constant Pool에서 관리된다.

---

</details>

<details>
   <summary>Blocking vs Non-Blocking</summary>

<br/>

- 자신의 작업이 막히는지 막히지 않는지로 보면 쉽다.

### Blocking
- 함수 A가 실행되다가 함수 B를 호출하면 제어권을 함수 A는 함수 B에게 제어권을 넘긴다.
- 따라서 함수 B가 실행을 완료하고 제어권을 돌려줄 때까지 아무 작업도 할 수 없다.

### Non-Blocking
- 함수 A가 함수 B를 호출하더라도 제어권을 넘기지 않는다.
- 따라서 함수 B를 호출한 뒤에도 함수 A는 계속 실행된다.

---

</details>

<details>
   <summary>Synchronous vs Asynchronous</summary>

<br/>

+ Synchronous(동기)
    - 함수 A가 함수 B를 호출하면, 함수 A는 B가 결과를 반환할 때까지 대기한다. 
+ Asynchronous(비동기)
    -  함수 A가 함수 B를 호출더라도, 함수 A는 함수 B의 작업 완료 여부를 신경쓰지 않는다.
       - 함수 A가 함수 B를 호출할 때 콜백 함수를 함께 전달해서, 함수 B의 작업이 끝나면 콜백 함수가 실행된다.


---

</details>

<details>
   <summary>리플렉션</summary>

<br/>

- 접근 제어자와 상관 없이 런타임에 메모리에 올라간 클래스의 생성자, 메소드, 변수 등에 접근할 수 있는 기술
  - 자바는 정적 언어이기 때문에 컴파일 시점에 객체 타입을 결정한다.
- 주로 프레임워크나 라이브러리에서 사용된다.
  - 컴파일 시점에는 사용자가 작성한 클래스가 어떤 타입을 가지는지 알 수 없기 때문이다.
  - ex) 스프링에서 필드 주입 시 필드가 private 이더라도 의존관계 주입이 가능한 이유가 리플렉션 덕분이다. 
+ 주의점
    - 컴파일 타임에 확인되지 않고 런타임 시에만 발생하는 문제를 만들 수 있다.
    - 접근 제어자를 무시할 수 있다.
    - 성능이 떨어지므로, 꼭 필요한 경우에만 사용한다.

---

</details>

<details>
   <summary>리플렉션과 기본 생성자</summary>

<br/>

- 리플렉션을 사용하는 스프링이나 JPA 등에서 기본 생성자를 요구한다.
- 리플렉션은 생성자의 인자 정보를 가져오지 못한다. 따라서 파라미터 생성자만 있는 경우 리플렉션이 객체를 생성하지 못한다.
- 기본 생성자로 객체를 생성한다면, 필드 값 등은 리플렉션으로 넣어줄 수 있다.

---

</details>

<details>
   <summary>Stream</summary>

<br/>

+ java8에서 추가된 API
+ 컬렉션, 배열 등에 저장되어있는 요소들을 하나씩 참조하여 반복 처리를 가능하게 한다.
+ 불필요한 코드를 줄일 수 있고, 가독성을 향상시킨다.
+ 특징
  + 원본 데이터를 변경하지 않는다.
    + 원본 데이터를 읽어서 사용한다.
  + 한번 사용하면 닫혀서 다시 사용할 수 없다.
  + 작업을 내부 반복으로 사용한다.
    + 내부 반복이란 반복문을 메서드의 내부로 숨겨서 처리한다는 것을 말한다. `forEach()`의 경우 메서드 안에 for문을 넣은 것이다.
+ 구조
    - Stream 생성
    - 중간 연산
        - 데이터를 가공하는 단계에 해당되며, 스트림을 반환하므로 다른 연산과 연결해서 사용할 수 있다.
        - 필터링 : filter, distinct
        - 변환 : map, flatMap
        - 제한 : limit, skip
        - 정렬 : sorted
        - 연산결과확인 : peek
    - 최종 연산
        - 지연된 모든 중간 연산들을 수행하여 최종 결과를 출력한다. 이후 stream이 닫히므로 재사용할 수 없다.
        - 출력 : foreach
        - 소모 : reduce
        - 검색 : findFirst, findAny
        - 검사 : anyMatch, allMatch, noneMatch
        - 통계 : count, min, max
        - 연산 : sum, savage
        - 수집 : collect

---

</details>

<details>
   <summary>lambda</summary>

<br/>

+ 자바 8에서 등장
+ __메서드를 하나의 식으로 표현하는 익명 함수__
  + 메서드와 함수는 같은 의미이지만, 메서드는 클래스에 반드시 속해야 한다는 제약이 있기 때문에 함수라는 용어 사용
+ 인터페이스 내에 한 개의 추상 메서드만 정의되어있는 함수형(Function) 인터페이스를 통해 사용 가능
+ ex) Comparator, Runnable
+ 장점
    - 기존에 익명함수로 작성하던 코드를 줄일 수 있음
    - 가독성 증가
    - 병렬 프로그래밍이 용이하다.

---

</details>

<details>
   <summary>Optional</summary>

<br/>

- 모든 타입의 참조 변수를 담을 수 있는 제네릭 클래스이다.
- 반환 값 null 체크를 편리하게 할 수 있도록 기능을 제공한다.
  - Objects의 `isNull()`, `nonNull()`등도 널 체크를 편리하게 하기 위해서 존재한다.

---

</details>

<details>
   <summary>자바8 추가된 내용</summary>

<br/>

+ optional
+ stream
+ lambda
+ 새로운 날짜 API
  + LocalDateTime, LocalDate 등
+ 인터페이스에 default 메서드와 static 메서드를 포함할 수 있게 되었다.

**기존 날짜 API의 문제점**
+ 불변 객체가 아님
+ 헷갈리는 월 지정(1월을 0으로 표현)
+ 일관성 없는 요일 상수 (Calendar는 일요일이 1부터, Date는 0부터 시작)
+ 상수 필드 남용 등

---

</details>

<details>
   <summary>Java 8 -> Java 11</summary>

<br/>

+ __default GC가 Parallel GC에서 G1GC로 변경__
+ strip(), stripLeading(), stripTrailing(), isBlank(), repeat(n) 과 같은 새로운 문자열 메서드 추가
+ writeString, readString, isSameFile 과 같은 __File관련 새로운 메서드 추가__
+ Predicate 인터페이스에 부정을 나타내는 not() 메서드 추가
+ 람다에서 로컬 변수 Var 사용
  + var는 변수를 선언할 때 타입을 생략할 수 있으며, 컴파일러가 타입을 추론한다.
+ Javac를 통해 컴파일하지 않고도 바로 java 파일을 실행할 수 있게 되었다.

---

</details>
