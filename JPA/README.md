# JPA

## 목차

- [JPA & MyBatis](#jpa--mybatis)
- [엔티티](#엔티티)
- [영속성 컨텍스트](#영속성-컨텍스트)
- [엔티티 매핑](#엔티티-매핑)
- [데이터베이스 스키마 자동 생성](#데이터베이스-스키마-자동-생성)
- [프록시 객체](#프록시-객체)
- [즉시 로딩과 지연 로딩](#즉시-로딩과-지연-로딩)
- [영속성 전이와 고아 객체](#영속성-전이와-고아-객체)
- [값 타입](#값-타입)
- [JPA에서 쿼리를 작성하는 다양한 방법](#jpa에서-쿼리를-작성하는-다양한-방법)
- [JPQL](#jpql)
- [도메인 모델 패턴 & 트랜잭션 스크립트 패턴](#도메인-모델-패턴--트랜잭션-스크립트-패턴)
- [OSIV](#osiv)
- [Spring Data JPA](#spring-data-jpa)

---

## JPA & MyBatis
### 1. JPA
- Java Persistence API
- 자바 진영의 ORM 기술 표준으로, SQL 중심의 개발에서 객체 중심의 개발을 할 수 있도록 기능을 제공한다.
- 특징
  - JPA는 인터페이스 모음이다.
    - 구현체 : 하이버네이트, Eclipse, DataNucleus
    - 하이버네이트가 많이 사용된다.
  - 애플리케이션과 JDBC 사이에서 동작한다.
  - 특정 데이터베이스에 종속되지 않는다.

![image](https://user-images.githubusercontent.com/87891581/168938724-db0f7919-323f-4f60-ab7c-bd069c534ff7.png)

#### ORM
- Object Relational Mapping
- 객체와 관계형 데이터베이스의 테이블을 매핑하여 데이터를 객체화하는 기술이다.
  - 특정 데이터베이스에 의존적이지 않다.
- 객체는 객체대로 설계하고 관계형 데이터베이스는 관계형 데이터베이스대로 설계하더라도, ORM 프레임워크가 자바 객체와 관계형 DB를 매핑해준다.

#### 장점
- SQL 중심적인 개발에서 객체 중심으로 개발
- 생산성
  - 반복적인 CRUD 작업을 하지 않아도 된다.
- 유지보수
  - 필드를 수정하면 SQL은 JPA가 처리해준다.
- 패러다임의 불일치 해결
  - 객체는 추상화, 상속, 다형성이라는 개념이 있고, 연관관계를 참조로 맺는다.
  - 관게형 데이터베이스에는 추상화, 상속, 다형성이라는 개념이 없고, 연관관계를 외래키로 맺는다.
  - 이런 패러다임의 불일치 사이에서 데이터를 주고 받으려면 번거로운 변환 작업이 필요하다. 이를 JPA가 해결해준다.
- 성능
  - JPA는 캐시와 버퍼 기능을 지원하기 때문에 잘 활용하면 성능 향상이 가능하다.

### 2. MyBatis
- 반복적인 JDBC 프로그래밍을 단순화하고, SQL, 저장 프로시저 및 고급 매핑을 지원하는 퍼시스턴스 프레임워크이다.
  - Persistence Framework : 데이터베이스와 연동되는 시스템을 빠르게 개발하고 안정적인 구동을 보장해주는 프레임워크. ex) SQL Mapper, ORM
  - 저장 프로시저 : 일련의 쿼리를 마치 하나의 함수처럼 실행하기 위한 쿼리의 집합이다.

#### SQL Mapper
- 객체와 SQL의 필드를 매핑하여 데이터를 객체화하는 기술이다.
  - SQL을 직접 작성하기 떄문에 특정 데이터베이스에 의존적이다.

#### 실무에서 MyBatis를 사용하는 이유
- JPA는 쿼리를 직접 만들어준다는 장점이 있지만, 영속성 컨텍스트 등 복잡한 개념 때문에 러닝 커브가 MyBatis에 비해 높다.
- 따라서 국내에서는 순수 쿼리만 어느정도 다룰 줄 알면 사용하기가 상대적으로 편리한 MyBatis가 아직 많이 사용되고 있다.
  - 물론 JPA 수요가 높아지고 있다.

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

#### 준영속 엔티티를 수정하는 2가지 방법
**1. 변경 감지 기능 사용**
- 영속성 컨텍스트에서 엔티티를 다시 조회한 후에 데이터를 수정하는 방법
- 동작 방식
  1. 트랜잭션 안에서 다시 조회한 엔티티의 값을 변경
  2. 트랜잭션 커밋 서점에 변경 감지(Dirty Checking) 기능이 동작
  3. 데이터베이스에 update SQL 실행

**2. 병합 사용**
![image](https://user-images.githubusercontent.com/87891581/169645596-e958a5dc-d9cd-4f40-85a9-65ca6112bb84.png)
- 준영속 상태의 엔티티를 영속 상태로 변경할 때 사용하는 기능
- 동작 방식
  1. `merge()` 실행
  2. 파라미터로 넘어온 준영속 엔티티의 식별자 값으로 1차 캐시에서 엔티티 조회
     - 1차 캐시에 엔티티가 없으면, 데이터베이스에서 엔티티를 조회하고 1차 캐시에 저장
  3. 조회한 영속 엔티티의 값을 준영속 엔티티의 값으로 모두 교체
  4. 트랜잭션 커밋 시점에 변경 감지 기능이 동작해서 데이터베이스에 update SQL 실행
- 모든 필드를 변경해버리고, 데이터가 없으면 null로 업데이트를 해버린다.
  - 변경 폼 화면에서 모든 데이터를 항상 유지해야 하기 때문에 오히려 번거로워진다.

## 영속성 컨텍스트
- 엔티티를 영구 저장하는 환경이라는 뜻이다.
- 엔티티 매니저로 엔티티를 저장하거나 조회하면, 엔티티 매니저는 영속성 컨텍스트에 엔티티를 보관하고 관리한다.

### 이점
#### 1. 1차 캐시
- `save()`나 `find()`를 호출하면 엔티티가 1차 캐시에 등록된다. 
- 1차 캐시에 등록된 엔티티를 조회한다면, 조회 쿼리 없이 1차 캐시에서 바로 조회할 수 있다.
#### 2. 동일성(identity) 보장
- 영속 엔티티는 1차 캐시에서 조회하므로 동일한 참조값의 엔티티를 보장한다.
#### 3. 트랜잭션을 지원하는 쓰기 지연(transactional write-behind)
- 엔티티 매니저로 CRUD 작업을 하면, 곧바로 쿼리를 보내지 않고 sql문을 모아두었다가 커밋하면 한번에 전송한다.
#### 4. 변경 감지(dirty checking)
- 영속 엔티티의 데이터를 수정하고 플러시하면, 자동으로 데이터베이스에 반영된다.
- 과정
  1. 영속 엔티티의 데이터 수정 후 플러시 발생
  2. 영속성 컨텍스트가 스냅샷과 엔티티를 비교하여 변경을 감지
  3. 쓰기 지연 SQL 저장소에 UPDATE 쿼리 등록
  4. 쓰기 지연 SQL 저장소의 쿼리를 데이터베이스에 전송
#### 5. 지연 로딩(lazy loading)

### 플러시
- 영속성 컨텍스트의 변경 내용을 데이터베이스에 반영
  - 영속성 컨텍스트를 비우지 않는다.
- 플러시하는 방법
  - `em.flush()` - 직접 호출
  - 트랜잭션 커밋 - 플러시 자동 호출
  - JPQL 쿼리 실행 - 플러시 자동 호출

## 엔티티 매핑
### 객체와 테이블 매핑
- `@Entity` : 해당 애노테이션이 붙은 클래스는 JPA가 관리하며, 엔티티라 한다.
  - name 속성은 JPA에서 사용할 이름을 지정하는 것이다.(쿼리에서 사용) 
  - 기본 생성자가 필수
  - final 클래스, enum, interface, inner 클래스 사용 x
  - 저장할 필드에 final 사용 x
- `@Table` : 엔티티와 매핑할 테이블을 지정한다.
  - 생략 시 엔티티 이름과 동일한 테이블 지정

### 필드와 컬럼 매핑
- `@Column` : 컬럼 매핑
- `@Temporal` : 날짜 타입 매핑
  - 날짜 타입(`java.util.Date`, `java.util.Calendar`)를 매핑할 떄 사용
  - `LocalDate`, `LocalDateTime`을 사용할 때는 생략 가능
- `@Enumerated` : enum 타입 매핑
  - `EnumType.ORIDINAL` 대신, `EnumType.STRING`을 사용한다.
- `@Lob` : BLOB, CLOB을 매핑하는데에 사용되며, 길이 제한없이 문자열 등에 사용한다.
  - CLOB : `String`, `char[]`, `java.sql.CLOB`
  - BLOB : `byte[]`, `java.sql.BLOB`
- `Transient` : 특정 필드를 컬럼에 매핑하지 않음(무시)
  - 주로 메모리상에서만 임시로 어떤 값을 보관하고 싶을 때 사용한다.

### 기본키 매핑
- 직접 할당
  - `@Id`만 사용한다.
- 자동 생성
  - `@Id`와 `@GeneratedValue`를 같이 사용.
  - `@GeneratedValue` 전략 종류
    - IDENTITY : 기본키 생성을 데이터베이스에 위임. `persist()` 시점에 sql 실행. ex) MySql
    - SEQUENCE : 데이터베이스 시퀀스 오브젝트 사용. ex) 오라클
    - TABLE : 키 생성용 테이블 사용. 모든 DB에서 사용 가능하지만, 성능이 좋지 않다.
    - AUTO : 방언에따라 자동 지정, 기본값

#### 권장하는 식별자 전략
- Long형 + 대체키 + 키 생성전략 사용
  - 미래까지 기본 키 제약 조건을 만족하는 자연키는 찾기 어렵기 대문에 대체키를 사용한다.
  - 주민등록번호도 기본키로 적절하지 않다.

### 연관관계 매핑
- 객체의 참조와 테이블의 외래키를 매핑하는 것을 말한다.
  - 객체는 참조용 필드가 있는 쪽으로만 참조가 가능하다.(단방향)
  - 테이블은 외래키 하나로 양쪽 조인이 가능하다.(양방향)
- 객체는 참조 한번으로 단방향 관계를 맺을 수 있지만, 테이블은 외래키 하나로 양방향 관계를 맺을 수 있다.
- 이때 객체를 양방향 참조 관계로 변경 한다면, 객체의 두 관계 중 한쪽만 외래키를 관리하도록 하고, 다른 한쪽은 읽기만 가능하도록 설정해야 한다.
  - 외래키를 관리하는 참조를 연관관계 주인이라고 말한다.
  - 연관관계 주인에는 `@JoinColumn`을 붙여 외래키를 매핑해주고, 반대편에는 `mappedBy` 속성으로 주인을 지정해준다.

#### 연관관계 종류
**1. 다대일(N:1)** - `@ManyToOne`
- 외래키가 있는 테이블에 매핑된 엔티티가 연관관계 주인을 가지고 있다.  
  - 테이블은 항상 다쪽에 외래키가 있기 때문에, 다쪽의 엔티티가 연관관계 주인을 보유한다.
- 가장 많이 사용되는 연관관계이다.

**2. 일대다(1:N)** - `@OneToMany`
- 외래키가 없는 테이블에 매핑된 엔티티가 연관관계 주인을 가지고 있다.
  - 테이블은 항상 다쪽에 외래키가 있기 때문에, 일쪽의 엔티티가 연관관계 주인을 보유한다.
- `@JoinColumn`을 사용해야 한다. 그렇지 않으면, 중간에 테이블을 추가하는 조인 테이블 방식을 사용한다.
- 엔티티가 관리하는 외래키가 다른 테이블에 있기 때문에 Update SQL이 추가로 실행된다.
  - Team 엔티티가 Member 엔티티를 필드로 가지고 있는 경우, `1. team_id가 null인 멤버 insert` -> `2. 팀 insert` -> `3. 멤버의 team_id update 쿼리 발생`
- 이런 이유로 일대다 매핑보다는 다대일 양방향 매핑 권장

**3. 일대일(1:1)** - `@OneToOne`
- 주 테이블과 대상 테이블 중에 외래키를 선택할 수 있다.
- 주 테이블에 외래키
  - 장점 : 주 테이블만 조회해도 대상 테이블에 데이터가 있는지 확인 가능하다.
  - 단점 : 값이 없으면 외래키에 null을 허용한다는 단점이 있다.
- 대상 테이블에 외래키
  - 장점 : 주 테이믈과 대상 테이블을 일대일에서 일대다 관계로 변경할 때 테이블 구조 유지
  - 단점 : 프록시 기능의 한계로 지연 로딩으로 설정해도 항상 즉시 로딩됨
    - 외래키가 있는 테이블에 매핑된 엔티티가 연관관계 주인을 가지고 있다면, 조회 시점에 프록시를 넣을지 null을 넣을지 결정할 수 있다.
    - 외래키가 없는 테이블에 매핑된 엔티티가 연관관계 주인을 가지고 있다면, 프록시를 넣을지 null을 넣을지 모르기 때문에 이를 결정하기 위해 즉시 로딩이 발생한다.
      - 클래스는 데이터가 없음을 null로 표현하며, 프록시를 미리 넣으면 null을 넣을 수 없다.
      - 컬렉션은 데이터가 없음을 Empty로 표현할 수 있기 때문에, 동일한 상황의 일다다에서는 지연 로딩이 가능하다.
    
**4. 다대다(N:M)** - `@ManyToMany`
- 관계형 데이터베이스에서는 정규화된 테이블 2개로 다대다 관계를 표현할 수 없기 때문에, 연결 테이블을 추가해서 일대다, 다대일 관계로 풀어내야한다.
- 객체는 컬렉션을 사용해서 객체 2개로 다대다 관계가 가능하다.
- 이에 대한 해결 방안으로 두가지 방법이 있다.
  1. `@JoinTable`로 연결 테이블을 지정하는 방법이 있지만, 이 방법은 연결 데이터 추가가 불가능하다.
  2. 연결 테이블 대신, 연결 엔티티를 사용하는 방법이 더 좋은 방법이다.

### 상속관계 매핑
- 객체의 상속과 구조를 DB의 슈퍼타입 서브타입 관계와 매핑한다.
  - 관계형 데이터베이스는 상속이라는 개념이 없지만, 슈퍼타입 서브타입 모델링 기법으로 객체 상속을 유사하게 구현할 수 있다.

#### 상속관계 매핑 방법
1.조인 전략 : 부모 클래스와 자식 클래스를 각각의 테이블로 변환
   - 비즈니스적으로 복잡할 때 사용
   - 장점 :  테이블 정규화, 외래키 참조 무결성 제약조건 활용 가능, 저장공간 효율화
   - 단점 : 조회시 조인을 많이 사용(성능 저하), 조회 쿼리가 복잡합, 데이터 저장시 insert sql 2번 호출
2.단일 테이블 전략 : 통합 테이블로 변환
   - 비즈니스적으로 단순할 때 사용
   - 장점 : 조인이 필요 없으므로 일반적으로 조회 성능이 빠름, 조회 쿼리가 단순함
   - 단점 : 자식 엔티티가 매핑한 컬럼은 모두 null 허용, 테이블이 커질 수 있고 상황에 따라서 조회 성능이 오히려 느려질 수 있다.
3.구현 클래스마다 테이블 전략 : 슈퍼타입 테이블 없이 서브타입 테이블로 변환
   - 권장하지 않는다.
   - 장점 : 서브 타입을 명확하게 구분해서 처리할 때 효과적, not null 제약조건 활용 가능
   - 단점 : 여러 자식 테이블을 함께 조회할 때 성능이 느림(union 필요), 자식 테이블을 통합해서 쿼리하기 어려움

#### @MappedSuperclass
- 엔티티가 아니기 때문에 테이블과 매핑되지 않고, 자식 클래스에 매핑 정보만 제공한다.
- 테이블과 관계 없이, 단순히 엔티티가 공통으로 사용하는 매핑 정보를 모으는 역할을 한다.
  - ex) 등록일, 수정일, 등록자, 수정자

## 데이터베이스 스키마 자동 생성
- DDL을 애플리케이션 실행 시점에 자동으로 생성한다.
  - 데이터베이스 방언을 활용해서 데이터베이스에 맞는 적절한 DDL 생성
  - DDL을 자동 생성할 때만 사용되고, JPA 실행 로직에는 영향을 주지 않는다.
  - db를 수정할 필요없이 편리하게 개발할 수 있다.
- 주의점
  - 운영 장비에는 절대 create, create-drop, update를 사용하면 안된다.
  - 개발 초기 단계는 create 또는 update
  - 테스트 서버는 update 또는 validate
    - 이 경우에도 update는 가급적 사용하지 말고, alter를 직접 해준다.
  - 스테이징과 운영 서버는 validate 또는 none

### 속성
|옵션|설명|
|--|--|
|create|기존 테이블 삭제 후 다시 생성(Drop + Create)
|create|create와 같으나 종료 시점에 테이블 Drop|
|update|변경분만 반영|
|validate|엔티티와 테이블이 정상 매핑되었는지만 확인|
|none|사용하지 않음(사실 아무거나 입력해도 상관없지만, 관례상 none을 입력하거나 주석처리한다.)|

## 프록시 객체
- 프록시 객체는 원래 객체를 감싸고 있는 객체이다.
- 프록시 객체는 실제 클래스를 상속받아서 만들어지며, 프록시 객체의 메소드를 호출하면 프록시 객체는 실제 객체의 메소드를 호출한다. 
  - 사용자 입장에서는 진짜 객체인지 프록시 객체인지 구분하지 않고 사용할 수 있다.
- 프록시 객체는 처음 사용할 때 한번만 초기화 되며, 실제 엔티티로 바뀌는 것이 아니라 실제 엔티티에 접근 가능하게 되는 것이다.
- 영속성 컨텍스트의 도움을 받을 수 없는 준영속 상태일 때, 프록시를 초기화하면 문제가 발생한다.
  - 초기화 후 준영속 상태가 되거나, 실제 엔티티가 반환된 경우에는 문제 없다.

### find() vs getReference()
- `em.find()` : 데이터베이스를 통해 실제 엔티티 객체를 조회한다.
- `em.getReference()` : 프록시 엔티티 객체를 조회한다.
- 영속성 컨텍스트에 찾는 엔티티가 이미 있다면, 메소드 상관없이 영속성 컨텍스트에 있는 엔티티를 조회한다.
  - 같은 트랜잭션 내에서는 동일 참조 보장!

## 즉시 로딩과 지연 로딩
- 즉시로딩 : 엔티티를 조회할 때 연관된 엔티티도 함께 조회한다. 
  - 연관된 엔티티는 실제 엔티티 객체를 참조한다.
  - JPA 구현체는 가능하면 조인을 사용해서 한번에 조회한다.
- 지연로딩 : 연관된 엔티티를 실제 사용할 때 조회한다.
  - 연관된 엔티티는 프록시 객체를 참조한다.

### 주의점
- 즉시 로딩은 N+1 문제를 일으키기 때문에 지연 로딩을 기본적으로 사용하고, 즉시 로딩 기능이 필요한 경우에는 페치 조인을 활용한다.
  - ex) 팀 엔티티를 참조하는 멤버 엔티티 N개를 즉시 로딩으로 조회하면, `1번의 멤버 조회 쿼리` + `N번의 각 멤버가 참조하는 팀 조회 쿼리`가 발생한다. 
- `@ManyToOne`과 `@OneToOne`은 기본이 즉시 로딩이므로, LAZY로 설정해야 한다.

## 영속성 전이와 고아 객체
### 1. 영속성 전이
- 특정 엔티티를 영속 상태로 만들 때 연관된 엔티티도 함께 영속 상태로 만들고 싶으면 영속성 전이 기능을 사용하면 된다.
  - ex) 부모 엔티티를 저장할 때 자식 엔티티도 함께 저장
- 영속성 전이는 연관관계 매핑과 아무 관련이 없다.

#### 옵션 종류
- ALL : 모두 적용
- PERSIST : 영속
- REMOVE : 삭제
- MERGE : 삭제
- REFRESH
- DETACH

### 2. 고아 객체
- 부모 엔티티와 연관관계가 끊어진 자식 엔티티를 고아 객체라고 하며, JPA는 고아 객체를 자동으로 삭제하는 기능을 제공한다.
  - 부모를 제거할 때 자식도 함께 제거하는 기능도 제공한다.(= `CascadeType.REMOVE`)
- 참조하는 곳이 하나일 때만 사용해야 한다.
  - ex) 게시판과 첨부파일 관계

### 3. 영속성 전이 + 고아 객체
- `CascadeType.ALL` + `orphanRemovel=true`
- 두 옵션을 모두 활성화하면 부모 엔티티를 통해서 자식의 생명 주기를 관리할 수 있다.

## 값 타입
### JPA의 데이터 타입 분류
> 식별자가 필요하고 지속해서 값을 추적하거나 변경해야 한다면, 값 타입이 아닌 엔티티이다.

- 엔티티 타입
  - `@Entity`로 정의하는 객체
  - 데이터가 변해도 식별자로 지속해서 추적 가능
- 값 타입
  - int, Integer, String처럼 단순히 값으로 사용하는 자바 기본 타입이나 객체
  - 식별자가 없고 값만 있으므로 변경시 추적 불가
  - 생명 주기를 엔티티에 의존
  - 값을 복사해서 사용하거나 불변 객체로 만들어 공유하는 것이 안전

### 값 타입 분류
**1. 기본값 타입**
- 자바 기본 타입(int, double), 래퍼 클래스(Integer, Long), String
- 생명 주기를 엔티티에 의존한다.
- 값 공유 시 기본 타입은 항상 값을 복사하고, 래퍼 클래스와 String은 변경 불가능한 객체를 공유한다.

**2. 임베디드 타입(복합 값 타입)**
- 새로운 값 타입을 직접 정의할 수 있으며, 주로 기본 값 타입을 모아서 만든다.
  - 엔티티를 모아서 만들 수도 있다.
  - 기본 생성자 필수
  - 임베디드 타입 사용 전후의 테이블은 동일하다.
- 수정할 수 없도록 생성자로만 값을 설정하여 불변 객체로 만든다.
- 객체 간에 필드 값이 같으면 동등하도록, `equals()`를 적절하게 오바라이딩 한다.
  - `hashcode()`도 같이 오버라이딩해주면 해시를 사용하는 컬렉션에서 효율적으로 사용할 수 있다. 
- 장점
  - 재사용
  - 높은 응집도
  - 해당 값 타입만 사용하는 의미 있는 메소드를 만들 수 있다.
- ex) `도시 + 번지 + 우편번호 -> 주소`

**3. 컬렉션 값 타입**
- 값 타입을 하나 이상 저장할 때 사용한다.
- 데이터베이스는 컬렉션을 같은 테이블에 저장할 수 없기 때문에 별도의 테이블이 필요하다.
  - 값 타입 컬렉션을 매핑하는 테이블은 모든 컬럼을 묶어서 기본키를 구성한다.(null x, 중복 저장 x)
- 값 타입 컬렉션에 변경 사항이 발생하면, 주인 엔티티와 관련된 모든 데이터를 삭제하고 값 타입 컬렉션에 있는 현재 값을 모두 다시 저장한다.
  - 값 타입은 엔티티와 다르게 식별자 개념이 없어서 추적이 어렵기 때문이다.
  - 한 컬럼만 변경하도록 최적화를 하는 방법이 있긴 하다.
- 실무에서는 일대다 관계나 다대일 양방향 관계를 고려하는 것이 좋다.
  - 영속성 전이 + 고아 객체 제거를 사용해서 값 타입 컬렉션처럼 사용

## JPA에서 쿼리를 작성하는 다양한 방법
### 1. [JPQL](#jpql)
- JPA를 사용하면 엔티티 객체를 중심을 개발할 수 있다. 하지만 필요한 데이터만 DB에서 불러오기 위해 SQL이 필요한 순간이 있다.
- 이를 위해 JPA는 테이블이 아닌 객체를 대상으로 하는 객체 지향 쿼리 언어를 제공하며, 이를 JPQL이라고 부른다.

### 2. Criteria
- 문자가 아닌 자바 코드로 JPQL을 작성할 수 있다.
- JPQL 빌더 역할
- JPA 공식 기능이지만, 복잡하고 실용성이 떨어진다.

### 3. QueryDSL
- 문자가 아닌 자바 코드로 JPQL을 작성할 수 있다.
- JPQL 빌더 역할
- Criteria에 비해 동적 쿼리를 편리하게 작성할 수 있기 때문에 실무에서 권장된다.

### 4. 네이티브 SQL
- JPA가 제공하는 SQL을 직접 사용하는 기능
- JPQL로 해결할 수 없는 특정 데이터베이스에 의존적인 기능을 사용할 때 사용하면 된다.
  - 특정 데이터베이스에 의존하는 SQL을 작성하므로, 데이터베이스를 변경하면 네이티브 SQL도 수정해야 한다.
  - ex) FROM절의 서브 쿼리, 오라클 CONNECT BY, 특정 DB만 사용하는 SQL 힌트

### 5. JDBC API
- JPA를 사용하면서 JDBC 커넥션을 직접 사용하거나, 스프링 JdbcTemplate, 마이바티스 등을 함께 사용할 수 있다.
- JPA를 우회해서 데이터베이스에 접근하므로, SQL을 실행하기 전에 영속성 컨텍스트를 수동으로 플러시해야 한다.

## JPQL
- JPA를 사용하면 엔티티 객체를 중심을 개발할 수 있다. 하지만 필요한 데이터만 DB에서 불러오기 위해 SQL이 필요한 순간이 있다.
- 이를 위해 JPA는 테이블이 아닌 객체를 대상으로 하는 객체 지향 쿼리 언어를 제공하며, 이를 JPQL이라고 부른다.

### 특징
- 엔티티 객체를 대상으로 쿼리한다.
- JPQL은 SQL을 추상화해서 특정 데이터베이스 SQL에 의존하지 않는다.
- JPA는 JPQL을 분석한 다음 적절한 SQL로 변환한다.
- FROM 절의 서브쿼리는 현재 JPQL에서 불가능하다.

### 프로젝션
- SELECT 절에 조회할 대상을 지정하는 것을 말한다.
- 프로젝션 대상은 엔티티, 임베디드 타입, 스칼라 타입이 있다.
  - 스칼라 타입 : 숫자, 문자 등 기본 데이터 타입을 말한다.
### 경로 표현식
- `.`을 찍어 객체 그래프를 탐색하는 것을 말한다.
  - ex) `select m.username from Member m`
- 필드 종류
  - 상태 필드 : 단순히 값을 저장하기 위한 필드. ex) m.username
  - 연관 필드 : 연관관계를 위한 필드, 임베디드 타입 포함
    - 단일 값 연관 필드 : 대상이 엔티티. ex) m.team
    - 컬렉션 값 연관 필드 : 대상이 컬렉션. ex) m.orders
- 경로 종류
  - 상태 필드 경로 : 경로 탐색의 끝이다. 더는 탐색할 수 없다.
  - 단일 값 연관 경로 : 묵시적으로 내부 조인이 일어난다. 단일 값 연관 경로는 계속 탐색할 수 있다.
  - 컬렉션 값 연관 경로 : 묵시적으로 내부 조인이 일어난다. 더는 탐색할 수 없다.
    - FROM 절에서 명시적 조인(join 키워드 직접 사용)을 통해 별칭을 얻으면 별칭으로 탐색할 수 있다.
- 묵시적 조인은 조인이 일어나는 상황을 파악하기 어렵기 때문에 가급적 명시적 조인을 사용하자.
  - 조인은 SQL 튜님에 중요 포인트

### 페치 조인
- 조인의 종류가 아니라, JPQL에서 성능 최적화를 위해 제공하는 기능이다.
  - 연관된 엔티티나 컬렉션을 한 번에 조회하는 기능이다.(즉시 로딩)
  - 글로벌 로딩 전략을 지연 로딩으로 하고, 최적화가 필요할 때 페치 조인을 적용한다.
- 여러 테이블을 조인해서 엔티티가 가진 모양이 아닌 전혀 다른 결과를 내야 하면, 일반 조인을 사용하고 필요한 데이터들만 조회해서 DTO로 변환하는 것이 효과적이다.

#### 일반 조인 vs 페치 조인
- 일반 조인은 SELECT 절에 지정한 엔티티만 조회할 뿐, 연관된 엔티티를 함께 조회하지 않는다.
  - 지연 로딩으로 설정하면 초기화하지 않는 프록시를 반환한다.
  - 즉시 로딩으로 설정하면 즉시 로딩을 위해 쿼리를 한 번 더 실행하여 실제 엔티티를 반환한다.
- 페치 조인은 SELECT 절에 지정한 엔티티와 연관된 엔티티를 함꼐 조회한다.

#### 주의점
- 일대다 관계의 컬렉션을 페치 조인 하면, `일`의 row 수가 `다`를 기준으로 row가 생성된다.
  - ex) 멤버 1과 멤버 2가 팀A 소속일 때 팀을 페치 조인하면, 기대한 1건의 팀A가 아니라 2건의 팀A가 조회된다.
  - JPQL의 `DISTINCT`로 엔티티 중복을 제거할 수 있다.
- 둘 이상의 컬렉션은 페치 조인을 할 수 없다.
- 컬렉션을 페치 조인하면, 페이징 API(setFirstResult, setMaxResults)를 사용할 수 없다.
  - 페이징을 하고 싶다면, 컬렉션은 지연 로딩으로 조회하고 N+1 문제가 발생하지 않도록 `default_betch_fetch_size` 설정을 통해 쿼리를 모아서 보내도록 설정하자.
    - 불필요한 컬럼 조회를 피하고 싶다면, dto와 In절을 활용하는 방법을 고려해도 좋다.
  - 일대일, 다대일 같은 단일 값 연관 필드는 row 수를 증가시키지 않기 때문에 페이징 API를 사용할 수 있다.

### 벌크 연산
- 많은 양의 데이터를 한번에 변경하고 싶으면, JPA의 변경 감지 기능을 사용하기보다는 여러건을 한 번에 수정하거나 삭제하는 벌크 연산을 사용하는 것이 효율적이다.
- 영속성 컨텍스트를 무시하고 직접 쿼리하기 때문에 영속성 컨텍스트와 데이터베이스 간에 값이 다를 수 있다는 점을 주의해야 한다.
  - 영속성 컨텍스트가 비어있을 때 벌크 연산을 실행하거나, 벌크 연산 수행 후 영속성 컨텍스트를 초기화해준다.

## 도메인 모델 패턴 & 트랜잭션 스크립트 패턴
### 1. 도메인 모델 매턴
- 엔티티가 비즈니스 로직을 가지고 객체 지향의 특성을 적응 활용하는 것을 도메인 모델 패턴이라고한다.
- 서비스 계층은 단순히 엔티티에 필요한 요청을 위임하는 역할을 한다.
- JPA에서 많이 사용한다.

### 2. 트랜잭션 스크립트 패턴
- 엔티티에는 비즈니스 로직이 거의 없고 서비스 계층에서 대부분의 비즈니스 로직을 처리하는 것을 트랙잭션 스크립트 패턴이라고 한다.
- MyBatis에서 많이 사용한다.

## OSIV
- Open Session In View : 현재의 엔티티매니저가 초기에는 `Session`으로 불리던 것이 관례가 되었다.
- 영속성 컨텍스트를 뷰까지 열어둔다는 뜻이다.
  - 뷰와 컨트롤러에서 지연 로딩을 가능하도록 한다.
- 영속성 컨텍스트를 유지하는 만큼 데이터베이스 커넥션 리소스를 사용하기 때문에, 실시간 트래픽이 중요한 애플리케이션에서는 커넥션이 모자를 수가 있다.
  - ADMIN처럼 커넥션을 많이 사용하지 않는 곳에서는 사용해도 좋다.

### OSIV ON
![image](https://user-images.githubusercontent.com/87891581/169645648-c8eace47-cff9-4921-b06b-c3ceafe1a35f.png)
- `Spring.jpa.open-in-view : true`, 기본값
### OSIV OFF
![image](https://user-images.githubusercontent.com/87891581/169645668-2da7ad57-5d92-46e5-a3b7-7d453636980e.png)
- `Spring.jpa.open-in-view : false`
- 트랜잭션이 끝나기 전에 지연 로딩을 강제로 호출해야 한다.

## Spring Data JPA
- JPA를 사용할 때마다 반복적으로 작성하는 코드를 자동화 해준다.
- `JPARepository`라는 인터페이스가 기본적인 CRUD를 포함한 다양한 기능을 제공해준다.
  - `save(S)` : 새로운 엔티티는 저장하고 이미 있는 엔티티는 병합한다.
  - `delete(T)` : 엔티티를 하나 삭제한다. 내부에서 `EntityManager.remove()` 호출
  - `findById(ID)` : 엔티티를 하나 조회한다. 내부에서 `EntityManager.find()` 호출
  - `getOne(ID)` : 엔티티를 프록시로 조회한다. 내부에서 `EntityManager.getReference()` 호출
  - `findAll(...)` : 모든 엔티티를 조회한다. 정렬이다 페이징 조건을 파라미터로 제공할 수 있다.
- `findByName`처럼 일반화 하기 어려운 기능도 메서드 이름으로 정확한 JPQL 쿼리를 실행한다.