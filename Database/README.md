# Database
- DB
- DB(or DBMS)를 사용하는 이유
- DBMS
- SQL
- View
- 릴레이션
- 엔티티
- 속성
- 도메인
- 레코드

### DB
<details>
   <summary>답안 보기</summary>

- 일정한 규칙, 혹은 규약을 통해 구조화되어 저장되는 데이터의 모음이다.

</details>

---

### DB(or DBMS)를 사용하는 이유
<details>
   <summary>답안 보기</summary>

- 파일 시스템의 데이터 종속과 중복, 비일관성, 데이터 무결성 등의 문제를 해결하기 위해 사용한다.
  - 데이터 종속 : 파일 시스템에서는 데이터 정의를 응용 프로그램에서 한다. 이러한 의존관계로 인해 데이터 구조를 변경하려면 프로그램을 수정해야 한다.
  - 데이터 중복 : 응용 프로그램별로 독립적인 파일 관리로 인해 데이터의 중복 저장이 발생할 수 있다.
  - 데이터의 비일관성 : 중복 저장된 데이터 중 하나의 데이터만 변경되어 불일치성이 발생할 수 있다.

</details>

---

### DBMS
<details>
   <summary>답안 보기</summary>

- DataBase Management System. 
- 데이터베이스 관리 시스템으로, 다수의 사용자가 데이터베이스에 접근할 수 있도록 설계된 시스템이다.

</details>

---

### SQL
<details>
   <summary>답안 보기</summary>

- 데이터 베이스 시스템에서 사용하는 전용 언어이다.
- 데이터 정의어, 데이터 조작어, 데이터 제어어로 구성된다.
  - 데이터 정의어(DDL, Data Definition Language)
    - `CREATE, ALTER, DROP`문과 같이 테이블의 구조를 정의한다.
  - 데이터 조작어(DML, Data Manipulation Language)
    - `SELECT, INSERT, UPDATE, DELETE`문과 같이 데이터 검색, 삽입, 수정, 삭제하는 데 사용한다.
  - 데이터 제어어(DCL, Data Control Language)
    - `GRANT, REVOKE`문과 같이 데이터의 사용 권한을 관리한다.

</details>

---

### View
<details>
   <summary>답안 보기</summary>

- 하나 이상의 테이블에서 유도된 가상의 테이블이다.
  - 실제 데이터를 디스크에 저장하지 않고, 원본 테이블에서 가져온다.
- 매번 조인할 필요없이 편리하게 사용할 수 있고, 보안이 필요한 속성을 제외하여 정의할 수 있다는 장점이 있다.

</details>

---

### 릴레이션
<details>
   <summary>답안 보기</summary>

- 관계형 데이터베이스에서 정보를 구분하여 저장하는 기본 단위이다. 테이블이라고도 부른다.
  - NoSQL 데이터베이스에서는 컬렉션이라고 한다.

</details>

---

### 엔티티
<details>
   <summary>답안 보기</summary>

- 사람, 장소, 물건, 사건, 개념 등 여러 개의 속성을 지닌 명사를 의미한다.
  - 자동차라는 엔티티는 차 번호, 바퀴 수, 색깔, 차종 등 다양한 속성을 가진다.

</details>

---

### 속성
<details>
   <summary>답안 보기</summary>

- 릴레이션에서 관리하는 구체적이며 고유한 이름을 갖는 정보이다.
  - 필드나 열이라고도 부른다.
- 가령 자동차라는 엔티티는 차 번호, 바퀴 수, 색깔, 차종 등 다양한 속성을 가진다. 이때 서비스에서 필요로 하는 엔티티의 속성을 말한다. 
- 한 릴레이션 안에 있는 애트리뷰트 수를 차수(degree)라고 한다.

</details>

---

### 도메인
<details>
   <summary>답안 보기</summary>

- 릴레이션에 포함된 각각의 속성들이 가질 수 있는 값의 집합을 말한다.
  - 성별이라는 속성의 경우 남자와 여자라는 도메인을 가진다.

</details>

---

### 레코드
<details>
   <summary>답안 보기</summary>

- 테이블에 쌓이는 행단위의 데이터를 레코드라고 한다.
  - 튜플이라고도 한다.
- 릴레이션 튜플의 개수를 카디날리티라고 한다.

</details>

---

### 키
<details>
   <summary>답안 보기</summary>



</details>

---

### 템플릿
<details>
   <summary>답안 보기</summary>



</details>

---

