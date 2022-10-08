# JPA

- 
- N+1 문제 
- fetch join 한계 
- OneToMany fetch join 페이징 쿼리 성능 이슈 
- MultipleBagFetchException 
- OneToOne 양방향 관계 Lazy 로딩 주의 
- 상속관계 매핑 
- QueryDsl을 사용하는 이유 
- OSIV

---

<details>
   <summary>영속성</summary>

<br/>

- 데이터를 생성한 프로그램의 실행이 종료되더라도 사라지지 않는 데이터의 특성
- 데이터를 파일이나 DB에 저장함으로써 데이터에 영속성을 부여한다.

</details>

<details>
   <summary>JDBC</summary>

<br/>

- 자바에서 데이터베이스에 접속할 수 있도록 하는 자바 API이다.

</details>

<details>
   <summary>Spring JDBC</summary>

<br/>

- JDBC의 저수준 처리를 스프링 프레임워크에 위임하여, Connection 연결 객체 생성 및 종료, Statement 준비/실행 및 종료 등의 반복되는 처리를 대신해준다.

</details>

<details>
   <summary>MyBatis</summary>

<br/>

- 반복적인 JDBC 프로그래밍을 단순화하고, 코드에서 SQL을 분리하는 목적을 가진 프레임워크

</details>

<details>
   <summary>ORM</summary>

<br/>

- Object Relational Mapping
- 객체와 관계형 데이터베이스의 테이블을 매핑하여 데이터를 객체화하는 기술이다.
- 객체는 객체대로 설계하고 관계형 데이터베이스는 관계형 데이터베이스대로 설계하더라도, ORM 프레임워크가 자바 객체와 관계형 DB를 매핑해준다.
  - 특정 데이터베이스에 의존적이지 않다.

</details>

<details>
   <summary>JPA</summary>

<br/>

- Java Persistence API
- 자바 진영의 ORM 기술 표준으로 사용되는 인터페이스 모음이다.
- 대표적인 구현체로 하이버네이트가 있고, SQL 중심의 개발에서 객체 중심의 개발을 할 수 있도록 기능을 제공한다.

</details>


<details>
   <summary>Spring Data JPA</summary>

<br/>

- JPA를 사용할 때마다 반복적으로 작성하는 코드를 추상화하여, 편리하게 사용할 수 있도록 하는 기술

</details>

<details>
   <summary>JPA를 사용하는 이유</summary>

<br/>

- 객체와 관계형 데이터베이스는 차이점이 있다.
  - 객체는 추상화, 상속, 다형성이라는 개념이 있고, 연관관계를 참조로 맺는다.
  - 관계형 데이터베이스에는 추상화, 상속, 다형성이라는 개념이 없고, 연관관계를 외래키로 맺는다.
- 이런 패러다임의 불일치 사이에서 데이터를 주고 받으려면 번거로운 변환 작업이 필요하다. 이를 JPA가 해결해준다.
  - ex) 조인해서 조회하는 SQL 작성 -> SQL에 의존적인 클래스 구현하여 데이터를 받아오기 -> 참조 관계를 가지도록 변환  

</details>

<details>
   <summary>영속성 컨텍스트</summary>

<br/>

- 엔티티를 영구 저장하는 환경이라는 뜻이다.
- 엔티티 매니저로 엔티티를 저장하거나 조회하면, 엔티티 매니저는 영속성 컨텍스트에 엔티티를 보관하고 관리한다.

</details>


<details>
   <summary>OSIV</summary>

<br/>



</details>


<details>
   <summary>OSIV</summary>

<br/>



</details>


<details>
   <summary>OSIV</summary>

<br/>



</details>


<details>
   <summary>OSIV</summary>

<br/>



</details>


<details>
   <summary>OSIV</summary>

<br/>



</details>


<details>
   <summary>OSIV</summary>

<br/>



</details>


<details>
   <summary>OSIV</summary>

<br/>



</details>


<details>
   <summary>OSIV</summary>

<br/>



</details>


<details>
   <summary>OSIV</summary>

<br/>



</details>


<details>
   <summary>OSIV</summary>

<br/>



</details>


<details>
   <summary>OSIV</summary>

<br/>



</details>


<details>
   <summary>OSIV</summary>

<br/>



</details>


<details>
   <summary>OSIV</summary>

<br/>



</details>

