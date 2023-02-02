# EntityManager와 영속성 컨텍스트

### 정의

- mybatis처럼 직접 SQL을 작성하거나 JPA를 활용한 개발을 할 때는 눈에 보이는 것 이상의 차이가 있다.
- 가장 사소한 예시를 들어보자면 CRUD로 불리는 가장 기본적인 4가지 동작 중 UPDATE는 JPA에 존재하지 않는다.
- 그럼에도 JPA는 업데이트 동작을 잘 수행한다. 영속성 컨텍스트가 데이터의 변경을 감지하여 자동으로 update 쿼리를 실행하기 때문이다.
- JPA는 `EntityManager`와 `영속성 컨텍스트`를 통해 데이터의 상태 변화를 감지하고 필요한 쿼리를 자동으로 수행한다.
- Application이 시작될 때 `EntityManager`를 자동으로 bean에 등록하고 우리가 알지 못하는 사이에 가져다 사용하고 있다.

<br>

### Entity Manager 생성

```java
// name에 persistance unit name을 등록할 수 있다.
EntityManagerFactory emf = Persistance.createEntityManagerFactory("name");
EntityManager em = emf.createEntityManager();
```

- `EntityManager`를 생성할 땐 가급적 팩토리를 활용한다.
- `EntityManagerFactory`는 Thread safe한 처리가 되어 있으나, `EntityManager`는 그렇지 않기 때문에 스레드 간 공유에 주의해야 한다.

<br>

### 영속성 컨텍스트 (Persistence Context)

- 엔티티를 영구 저장하는 환경이다.
- Java 영역에서 데이터를 관리하여 DB 접근을 최적화하는 역할을 담당한다.

<br>

### 생명주기

Entity는 4가지 상태가 존재한다.

1. 비영속
   - 영속성 컨텍스트와 연관이 없는 상태
2. 영속
   - 영속성 컨텍스트에서 관리 중인 상태
3. 준영속
   - 영속성 컨텍스트에 저장되어 있었으나 분리된 상태
4. 삭제
   - 영속성 컨텍스트에서 완전히 삭제된 상태

<br>

### 비영속

- `@Entity` 어노테이션을 갖는 엔티티 인스턴스를 막 생성했을 때는 영속성 컨텍스트에서 관리하지 않는다.
- `EntityManager`의 persist 메소드를 사용하여 영속 상태로 변경할 수 있다.

```java
em.persist(someEntity);
```

<br>

### 영속

`EntityManager`를 통해 데이터를 영속성 컨텍스트에 저장했다.  
JPA는 일반적으로 id 필드가 존재하지 않으면 예외를 뱉어내는데, 영속 상태의 엔티티를 관리하기 위해서다.  
id로 데이터를 관리하기 때문에 꼭 필요한 것이다.  
이 상태가 되면 몇 가지의 장점을 갖게 된다.

1. 1차 캐시
2. 동일성 보장
3. 트랜잭션을 지원하는 쓰기 지연
4. 변경 감지
5. 지연 로딩

<br>

### 준영속

- 원래 영속 상태였으나 영속성 컨텍스트에서 분리되어 더 이상 관리하지 않는 데이터가 된 상태이다.
- 영속 상태의 엔티티를 detach 시키거나 영속성 컨텍스트 자체가 초기화 / 종료되면 컨텍스트 내부의 모든 데이터는 준영속 상태가 된다.
- 관리되지는 않는 상태이지만 JPA의 지원을 받지 못할 뿐, 정상적인 데이터를 갖는 인스턴스이다.

```java
em.detach(someEntity);
```

<br>

### 삭제

Entity를 영속성 컨텍스트와 DB 양쪽에서 모두 삭제한다.

```java
em.remove(someEntity);
```

<br>

### 플러시(flush)

- 영속성 컨텍스트의 변경 내용을 DB에 반영하는 절차이다.
- 플러시를 수행하면 아래 순서대로 동작한다.

1. 데이터의 변경을 감지한다.
2. 생성된 쿼리를 쓰기 지연 저장소에 등록한다.
3. commit되면 저장되어 있던 쿼리를 모두 수행한다.
   `em.flush()`를 활용하면 직접 플러시할 수 있다.

<br>

### 종료

영속성 컨텍스트를 종료하려면 `EntityManager`의 close 메소드를 호출한다.

```java
em.close()
```

<br>

### 병합

준영속 상태의 데이터는 병합 기능을 사용하여 다시 영속 상태로 돌릴 수 있다.

```java
SomeEntity entity = em.find(key);
em.detach(entity);
em.merge(entity);
```
