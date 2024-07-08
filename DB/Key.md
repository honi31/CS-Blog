## 0. 관계형 데이터베이스

### 0.1 relation

relation 개념을 알기 전 수학에서의 set이라는 개념을 먼저 알아보자.

- **set**
  **set**은 서로 다른 elements를 가지는 collection이다. 따라서, 중복X. 그리고, 하나의 set에서 elements의 순서는 중요하지않다.
  {1,3,11,4,7} = {11,3,4,7,1}

![](https://velog.velcdn.com/images/honi31/post/c48574b0-25cb-4bc9-884c-c501f03e2561/image.png)

- **Cartesian Product**
  두 set의 원소들에 대해 pair를 만들어주면 모든 조합을 카티전 곱을 활용해 만들 수 있다.
  -> (1,p) (1,q) (1,r) (2,p) (2,q) (2,r)
  이때, 이 모든 조합의 부분집합을 relation이라고 한다.(=튜플들의 집합)
  -> {(1,p) (1,q) (2,r)}
  각각의 리스트를 튜플이라고 한다.
  -> (1,p)
  ![](https://velog.velcdn.com/images/honi31/post/cd890cc3-8558-4922-8372-77e4c48290f9/image.png)

### 0.2 relational data model

주로 테이블로 표현을 한다.
![](https://velog.velcdn.com/images/honi31/post/722543ac-c8e0-4d39-a95e-9a9f57fb160a/image.png)

- **domain **: atomic한 값들의 set, 이름을 붙일 수 있음
- **attribute**(field) : domain이 relation에서 맡은 역할 이름, 테이블에서 각각의 열에 대해 유일한 이름
- **tuple**(record) : 각 attribute의 값으로 이루어진 리스트, 테이블에서 하나의 행을 의미한다. 일부 값은 **NULL**일 수 있음.
- **relation** : table, 튜플들의 집합
- **relation name** : relatio의 이름

### 0.3 관계형 데이터베이스 (relational database)

관계형 데이터베이스란 relational data model에 기반하여 구조화된 database이다. relational database는 여러개의 relations로 구성된다. 따라서, 데이터들을 테이블 형태로 저장하여 관리한다.

---

## 1. Key

데이터베이스에서 **키(key)**란, 데이터베이스 내에서 각각의 행을 구분하기 위한 값 또는 속성(열)을 의미한다. 즉, Key는 튜플 간 구분을 위한 식별자 역할을 한다.
데이터베이스에서 Key는 **데이터의 일관성과 무결성을 보장**하기 위한 중요한 역할을 수행하며, 데이터베이스를 설계하고 구현할 때 매우 중요한 개념이다.

데이터베이스에서 Key는 다음과 같이 종류가 있다.

- SuperKey(슈퍼키)
- CandidateKey(후보키)
- PrimaryKey(기본키)
- UniqueKey
- AlternateKey(대체키)
- Foreign Key(외래키)
  ![](https://velog.velcdn.com/images/honi31/post/12f235f7-154b-48f4-bb42-36807390640b/image.png)

- 유일성
  하나의 키값으로 튜플을 유일하게 식별할 수 있는 성질을 말한다.
  각각의 튜플을 유일해야한다.
- 최소성 - 키를 구성하는 속성들 중 가장 최소로 필요한 속성들로만 키를 구성하는 성질을 말한다. 쉽게 말해, 키를 구성하고 있는 속성들이 진짜 각 튜플을 구분하는 데 꼭 필요한 속성들로만 구성되어 있는지를 의미한다.

### 1.1 슈퍼키(Super Key)

릴레이션에서 튜플을 유일하게 식별할 수 있는 키. 슈퍼키는 릴레이션 내 attribute set으로 구성된다.

릴레이션을 구성하는 모든 튜플 중 슈퍼키로 구성된 속성의 집합과 동일한 값은 없다.
슈퍼키는 릴레이션을 구성하는 모든 튜플에 대해 **유일성은 만족**하지만 **최소성은 만족하지 못한다.**

- 예시
  PLAYER(id, name, team_id, back_number, birth_date)의 슈퍼키는
  {id, name, team_id, back_number, birth_date}, {id, name}, {name, team_id, back_number} ... etc

### 1.2 후보키(Candidate Key)

어느 한 attribute라도 제거하면 유일하게 튜플을 식별할 수 없는 슈퍼키. 기본키가 될 수 있는 후보들을 의미한다. 키 or minimal superkey

후보키는 릴레이션을 구성하는 모든 튜플에 대해 **유일성과 최소성 모두 만족**한다. 따라서, NULL 값을 허용하지 않는다.

- 예시
  PLAYER(id, name, team_id, back_number, birth_date)의 후보키는
  {id}, {team_id, back_number}

### 1.3 기본키(Primary Key)

릴레이션에서 튜플을 유일하게 식별하기 위해 선택된 후보키.
테이블에서 특정 행(row)을 고유하게 식별할 수 있는 하나의 속성(열) 또는 속성의 집합이다.
즉, 기본키는 테이블의 모든 행을 고유하게 식별할 수 있는 유일한 식별자(identifier)이다.

기본키는 테이블에서 반드시 하나만 존재해야 하며, 해당 테이블의 모든 행에 대해 유일하고 NULL 값을 포함하지 않아야 한다.
기본키로 지정된 속성은 반드시 유일성 제약 조건(unique constraint)을 가져야한다.

주로 기본키는 보통 테이블에서 자동으로 생성되는 일련번호(serial number), GUID(Globally Unique Identifier), 또는 유일성이 보장되는 다른 속성을 사용하여 정의된다.

- 예시
  PLAYER(id, name, team_id, back_number, birth_date)의 후보키는
  {id} or {team_id, back_number} -> 주로 {id}

### 1.4 대체키(Alternate Key)

기본키로 사용되지 않는 후보키
후보키와 차이점은 NULL 값을 가질 수 있다는 점이다.

- 예시
  PLAYER(id, name, team_id, back_number, birth_date)의 유니크키
  {team_id, back_number}

### 1.5 외래키(Foreign Key)

두 개 이상의 테이블을 연결하는데 사용한다. 하나의 테이블에서 다른 테이블의 기본키를 참
다른 릴레이션의 pk를 참조하는 attribute set.

- 예시
  PLAYER(id, name, team_id, back_number, birth_date)와 TEAM(id, name, manager)가 있을 때
  foreign key는 PLAYER의 {team_id}

---

## 2. 제약조건 (constraints)

relational database의 relations들이 언제나 항상 지켜줘야 하는 제약 사항

### 2.1 implicit constraints

relational data model 자체가 가지는 constraints이다.

- relation은 중복되는 tuple을 가질 수 없다.
- relation 내에서는 같은 이름의 attribute를 가질 수 없다.

### 2.2 explicit constraints (schema-based)

주로 DDL을 통해 schema에 직접 명시할 수 있는 constraints

#### 2.2.1 도메인 무결성 제약조건

attribute의 value는 해당 attribute에 속한 value 여야 한다.
![](https://velog.velcdn.com/images/honi31/post/34a1da89-f01b-4d4d-a452-435cc117e91b/image.png)

#### 2.2.2 키 무결성 제약조건

서로 다른 tuple은 같은 value의 key를 가질 수 없다.
![](https://velog.velcdn.com/images/honi31/post/20204ce1-23be-4651-9eb5-85cdb145cb90/image.png)

#### 2.2.3 NULL 무결성 제약조건

attribute가 NOT NULL로 명시됐다면 NULL을 값으로 가질 수 없다.
![](https://velog.velcdn.com/images/honi31/post/065b9871-f8dc-4a50-a5cc-ae2ae5f48bd8/image.png)

#### 2.2.4 개체 무결성 제약조건

기본키 제약이라고도 하는데, 테이블은 기본키를 지정하고 그에 따른 무결성 원칙 즉, 기본키는 value에 NULL 값을 가질 수 없고 테이블 내에 오직 하나의 값만 존재해야 한다는 조건이다.
![](https://velog.velcdn.com/images/honi31/post/311514fd-7cf4-4dc2-96ff-71c40e8bd57c/image.png)

#### 2.2.5 참조 무결성 제약조건

참조 무결성 제약조건은 Foreign key와 Primary key의 도메인이 같아야 하고 primary key에 없는 value를 foreign key가 값으로 가질 수 없다.
![](https://velog.velcdn.com/images/honi31/post/1a06c6c5-4322-4584-9424-30ca4e544ccd/image.png)

#### 2.2.6 unique 제약조건(유일성 제약조건)

실제 DBMS에서는 위에서 설명한 제약조건과 함께 UNIQUE 제약조건도 사용한다. UNIQUE 제약조건은 속성의 모든 값들에 서로 같은 값이 없어야 한다는 조건이다.
