# 좋은 객체 지향 설계의 5가지 원칙(SOLID)

1. SRP(Single Responsibility Principle) : 단일 책임 원칙
   - 한 클래스는 하나의 책임만 가져야 하며, 클래스를 변경하는 이유는 단 하나의 이유여야 한다.
2. OCP(Open/Closed Principle) : 개방-폐쇄 원칙  
   - 소프트웨어의 요소는 확장에는 열려있으나 변경에는 닫혀 있어야 한다.
   - 요구 사항의 변경이나 추가 사항이 발생하더라도, 기존 구성 요소에는 수정이 일어나지 않고, 기존 구성 요소를 쉽게 확장해서 재사용한다.
3. LSP(Liskov Substitution Principle) : 리스코프 치환 원칙
   - 상위 타입의 객체를 하위 타입의 객체로 치환해도 상위 타입을 사용하는 프로그램은 정상적으로 동작해야 한다.
4. ISP(Interface segregation Principle) : 인터페이스 분리 원칙
   - 인터페이스는 그 인터페이스를 사용하는 클라이언트를 기준으로 분리해야 한다.
   - SRP가 클래스의 단일 책임이라면, ISP는 인터페이스의 단일 책임이다.
5. DIP(Dependency Inversion Principle) : 의존관계 역전 원칙
   - 상위 모델은 하위 모델에 의존하면 안된다. 
   - 구체화에 의존하면 안되며, 추상화에 의존해야 한다.
