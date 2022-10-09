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
  준영속 엔티티를 수정하는 2가지 방법
---

<details>
   <summary>영속성</summary>

<br/>

- 데이터를 생성한 프로그램의 실행이 종료되더라도 사라지지 않는 데이터의 특성
- 데이터를 파일이나 DB에 저장함으로써 데이터에 영속성을 부여한다.

---

</details>

<details>
   <summary>JDBC</summary>

<br/>

- 자바에서 데이터베이스에 접속할 수 있도록 하는 자바 API이다.

---

</details>

<details>
   <summary>Spring JDBC</summary>

<br/>

- JDBC의 저수준 처리를 스프링 프레임워크에 위임하여, Connection 연결 객체 생성 및 종료, Statement 준비/실행 및 종료 등의 반복되는 처리를 대신해준다.

---

</details>

<details>
   <summary>MyBatis</summary>

<br/>

- 반복적인 JDBC 프로그래밍을 단순화하고, 코드에서 SQL을 분리하는 목적을 가진 프레임워크

---

</details>

<details>
   <summary>ORM</summary>

<br/>

- Object Relational Mapping
- 객체와 관계형 데이터베이스의 테이블을 매핑하여 데이터를 객체화하는 기술이다.
- 객체는 객체대로 설계하고 관계형 데이터베이스는 관계형 데이터베이스대로 설계하더라도, ORM 프레임워크가 자바 객체와 관계형 DB를 매핑해준다.
  - 특정 데이터베이스에 의존적이지 않다.

---

</details>

<details>
   <summary>JPA</summary>

<br/>

- Java Persistence API
- 자바 진영의 ORM 기술 표준으로 사용되는 인터페이스 모음이다.
- 대표적인 구현체로 하이버네이트가 있고, SQL 중심의 개발에서 객체 중심의 개발을 할 수 있도록 기능을 제공한다.

---

</details>

<details>
   <summary>Spring Data JPA</summary>

<br/>

- JPA를 사용할 때마다 반복적으로 작성하는 코드를 추상화하여, 편리하게 사용할 수 있도록 하는 기술

---

</details>

<details>
   <summary>JPA를 사용하는 이유</summary>

<br/>

- 객체와 관계형 데이터베이스는 차이점이 있다.
  - 객체는 추상화, 상속, 다형성이라는 개념이 있고, 연관관계를 참조로 맺는다.
  - 관계형 데이터베이스에는 추상화, 상속, 다형성이라는 개념이 없고, 연관관계를 외래키로 맺는다.
- 이런 패러다임의 불일치 사이에서 데이터를 주고 받으려면 번거로운 변환 작업이 필요하다. 이를 JPA가 해결해준다.
  - ex) 조인해서 조회하는 SQL 작성 -> SQL에 의존적인 클래스 구현하여 데이터를 받아오기 -> 참조 관계를 가지도록 변환  

---

</details>

<details>
   <summary>엔티티</summary>

<br/>

## 엔티티
- 데이터베이스 테이블과 ORM 매핑되어 있는 객체이다.
- `@Entity`가 붙은 클래스는 JPA가 관리하며, 엔티티라고 부른다.

### 엔티티의 생명 주기
![image](https://user-images.githubusercontent.com/87891581/168966197-c708e0b4-ca49-4e0c-898b-7d30a478330a.png)
- 비영속(new/transient) : 영속성 컨텍스트와 전혀 관계가 없는 순수한 객체 상태
- 영속(managed) : 영속성 컨텍스트에 의해 관리되는 상태
- 준영속(detached) : 영속 상태의 엔티티가 영속성 컨텍스트에서 분리된 상태
  - 영속 상태가 된적이 있기 때문에 반드시 식별자가 있다.
  - 임의로 만들어낸 엔티티도 기존 식별자를 가지고 있으면 준영속 엔티티로 볼 수 있다.
- 삭제(removed) : 삭제된 상태

---

<details>
   <summary>영속성 컨텍스트</summary>

<br/>

- 엔티티를 영구 저장하는 환경이라는 뜻이다.
- 엔티티 매니저로 엔티티를 저장하거나 조회하면, 엔티티 매니저는 영속성 컨텍스트에 엔티티를 보관하고 관리한다.

---

</details>

</details>


<details>
   <summary>영속성 컨텍스트의 이점</summary>

<br/>

#### 1. 1차 캐시
- `save()`나 `find()`를 호출하면 엔티티가 1차 캐시에 등록된다.
- 1차 캐시에 등록된 엔티티를 조회한다면, 조회 쿼리 없이 1차 캐시에서 바로 조회할 수 있다.
#### 2. 동일성(identity) 보장
- 영속 엔티티는 1차 캐시에서 조회하므로 동일한 참조값의 엔티티를 보장한다.
#### 3. 트랜잭션을 지원하는 쓰기 지연(transactional write-behind)
- 커밋하기 전까지 SQL문을 모아두었다가 한번에 전송할 수 있다.
#### 4. 변경 감지(dirty checking)
- 영속 엔티티의 데이터를 수정하고 플러시하면, 자동으로 데이터베이스에 변경 내용이 반영된다.
- 과정
  1. 영속 엔티티의 데이터 수정 후 플러시 발생
  2. 영속성 컨텍스트가 스냅샷과 엔티티를 비교하여 변경을 감지
  3. 쓰기 지연 SQL 저장소에 UPDATE 쿼리 등록
  4. 쓰기 지연 SQL 저장소의 쿼리를 데이터베이스에 전송
#### 5. 지연 로딩(lazy loading)
- 엔티티를 실제 사용하는 시점에 SQL을 날려 데이터를 가져온다. 

---

</details>

<details>
   <summary>플러시</summary>

<br/>

- 영속성 컨텍스트의 변경 내용을 데이터베이스에 반영
  - 영속성 컨텍스트를 비우지 않는다.
- 플러시하는 방법
  - `em.flush()` - 직접 호출
  - 트랜잭션 커밋 - 플러시 자동 호출
  - JPQL 쿼리 실행 - 플러시 자동 호출

---

</details>

<details>
   <summary>OSIV</summary>

<br/>



---

</details>

<details>
   <summary>OSIV</summary>

<br/>



---

</details>

<details>
   <summary>OSIV</summary>

<br/>



---

</details>

<details>
   <summary>OSIV</summary>

<br/>



---

</details>

<details>
   <summary>OSIV</summary>

<br/>



---

</details>

<details>
   <summary>OSIV</summary>

<br/>



---

</details>

<details>
   <summary>OSIV</summary>

<br/>



---

</details>

<details>
   <summary>OSIV</summary>

<br/>



---

</details>

<details>
   <summary>OSIV</summary>

<br/>



---

</details>

<details>
   <summary>OSIV</summary>

<br/>



---

</details>
