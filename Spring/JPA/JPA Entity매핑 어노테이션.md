# JPA Entity매핑 어노테이션 정리/예제

## 어노테이션 종류

- @Entity
- @Table
- @Id
- @Column
- @Access
- @Enumerated
- @Temporal
- @Lob
- @Transient

<br>

## @Entity

`@Entity` 어노테이션은 JPA를 사용해 테이블과 매핑할 클래스에 붙여주는 어노테이션이다.  
이 어노테이션을 붙임으로써 JPA가 해당 클래스를 관리하게 된다.

- 속성
  - name
    - JPA에서 사용할 엔티티 이름 지정.
    - 생략시 클래스이름을 엔티티 이름으로 지정

```java
@Entity(name = "user2")
public class User {}
```

**주의 사항**

- 기본 생성자가 꼭 필요함
- final, enum, interface, inner class에서는 사용 불가
- 필드(변수)를 final로 선언 불가

<br>

## @Table

`@Table` 어노테이션은 엔티티와 매핑할 테이블을 지정하는 어노테이션이다.

- 속성
  - name
    - 매핑할 테이블 이름
    - 생략시 엔티티 이름(@Entity(name="~") 사용
  - catalog
    - catalog 기능이 있는 DB에서 catalog 매핑
  - schema
    - schema기능이 있는 DB에서 schema 매핑
  - uniqueContraints
    - DDL 생성시 유니크 제약조건 생성
    - 스키마 자동 생성 기능을 사용해 DDL을 만들 때만 사용

```java
@Entity
@Table(name = "user2")
public class User {}
```

<br>

## @Id

`@Id` 어노테이션은 특정 속성을 기본키로 설정하는 어노테이션이다.

```java
@Entity
@Table(name = "User")
public class User {
    @Id
    private Long id;
    private String name;
}
```

`@Id` 어노테이션만 적게될 경우 기본키값을 직접 부여해줘야 한다.  
하지만 보통 DB를 설계할 때는 기본키는 직접 부여하지 않고 Mysql `AUTO_INCREMENT`처럼 자동 부여되게끔 한다.

```java
@Entity
@Table(name = "User")
public class User {
    @Id
    @GeneratedValue
    private Long id;
    private String name;
}
```

`@GeneratedValue` 어노테이션을 사용하면 기본값을 DB에서 자동으로 생성하는 전략을 사용 할 수 있다.

- 속성
  - startegy = GenerationType.IDENTITY
    - 기본 키 생성을 DB에 위임 (Mysql)
  - startegy = GenerationType.SEQUENCE
    - DB시퀀스를 사용해서 기본 키 할당 (Oracle)
  - startegy = GenerationType.TABLE
    - 키 생성 테이블 사용 (모든 DB 사용 가능)
  - startegy = GenerationType.AUTO
    - 선택된 DB에 따라 자동으로 전략 선택

위 처럼 다양한 전략이 있는 이유는 DB마다 지원하는 방식이 다르기 때문이다.  
`AUTO` 같은 경우DB에 따라 전략을 JPA가 자동으로 선택한다.  
이로 인해 DB를 변경해도 코드를 수정할 필요 없다는 장점이 있다.

<br>

## @Column

`@Column` 어노테이션은 객체 필드를 테이블 컬럼과 매핑한다.

```java
@Column
private String name;
```

- 속성
  - name
    - 필드와 매핑할 테이블의 컬럼 이름 지정
    - name을 쓰지 않을 경우 (default)는 필드이름으로 대체
  - insertable
    - true : 엔티티 저장시 필드값 저장
    - false : 필드값이 저장되지 않음
  - updatable
    - true : 엔티티 수정시 값이 수정
    - false : 엔티티 수정시 값이 수정 되지 않음
  - table
    - 하나의 엔티티를 두 개 이상의 테이블에 매핑할 때 사용
  - nullable
    - true : null 대입 가능
    - false : not null 제약 조건
  - unique
    - 컬럼에 유니크 제약조건 부여
  - columnDefinition
    - 데이터베이스 컬럼 정보를 직접 부여
  - length
    - 문자 길이 제약조건
    - String 타입일 때 사용
  - precision, scale
    - BigDecimal 타입에서 사용
    - precision : 소수점을 포함한 전체 자릿수 설정
    - scale : 소수의 자릿수

**insertable**

```java
@Column(insertable = false)
private String name;
```

name 컬럼에 값을 입력해도 DB에는 값이 들어가지 않는다.

**updatable**

```java
@Column(updatable = false)
private String name;
```

name 컬럼의 값을 변경해도 변경값이 적용되지 않는다.

**nullable**

```java
@Column(nullable = false)
private String name;
```

name 컬럼에는 not null이 적용된다.

**unique**

```java
@Column(unique = true)
private String name;
```

name 컬럼에는 unique가 적용된다.

**columnDefinition**

```java
@Column(columnDefinition = "VARCHAR(255) NOT NULL")
private String name;
```

name 컬럼의 Datatype은 VARCHAR(255)가 되고 not null이 적용된다.

**length**

```java
@Column(length = 11)
private String name;
```

name 컬럼의 DataType은 VARCHAR(11)이 된다.

<br>

## @Access

`@Access` 어노테이션은 접근 방식을 설정한다.

- 속성
  - AccessType.FILED
    - 필드에 직접 접근
    - 필드 접근 권한이 `private`이여도 접근 가능
  - AccessType.PROPERTY
    - `getter`를 통해 접근

```java
public class User {
    @Id
    @GeneratedValue
    private Long id;
}

@Access(AccessType.FIELD)
public class User {
    @Id
    @GeneratedValue
    private Long id;
}
```

두 코드는 설정이 같다.

```java
@Access(AccessType.PROPERTY)
public class User {

    @GeneratedValue
    private Long id;

    @Id
    public Long getId() {
        return id;
    }
}
```

getter에 @id를 설정함으로 써 프로퍼티 접근으로 할 수 있다.

<br>

## @Enumerated

`@Enumrated` 어노테이션은 자바 enum 타입을 매핑할 때 사용한다.

- 속성
  - EnumType.ORDINAL
    - enum 순서를 DB에 저장
  - EnumType.STRING
    - enum이름을 DB에 저장

```java
@Enumerated(value = EnumType.ORDINAL)
private RoleType ordinal;
@Enumerated(value = EnumType.STRING)
private RoleType string;
```

EnumType.ORDINAL은 enum추가시 문제가 발생할 수 있으므로 사용을 지양하도록 하자..

<br>

## @Temporal

`@Temporal` 어노테이션은 날짜 타입을 매핑할 때 사용한다.

- 속성
  - TemporalType.DATE
    - 날짜, DB date 타입과 매핑(예 : 2022-02-04)
  - TemporalType.TIME
    - 시간, DB time 타입과 매핑(예: 14:56:27)
  - TemporalType.TIMESTAMP
    - 날짜와 시간 DB timestamp 타입과 매핑(예 : 2022-02-04 14:56:27)

```java
@Temporal(value = TemporalType.DATE)
private Date date;
@Temporal(value = TemporalType.TIME)
private Date time;
@Temporal(value = TemporalType.TIMESTAMP)
private Date timeStamp;
```

<br>

## @Lob

`@Lob` 어노테이션은 DB BLOB, CLOB 타입과 매핑할 때 사용한다.  
정의할 속성이 없다. 대신 필드 타입이 문자열이면 `CLOB`, 나머지는 `BLOB`을 매핑한다.

```java
@Lob
private String stringLob;
@Lob
private Integer integerLob;
```

stringLob은 LONGTEXT, integerLob은 LONGBLOB으로 매핑된다.

<br>

## @Transient

`@Transient` 어노테이션을 붙인 필드는 DB에 저장하지도 조회하지도 않는다.  
객체에 임시로 값을 보관하고 싶을 때 사용한다.

```java
@Transient
private String trans;
```

trans필드는 DB컬럼에 추가되지 않는다.
