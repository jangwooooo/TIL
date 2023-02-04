# JPA Entity 연관관계 매핑 정리/예제

관계형 데이터베이스는 테이블 간 **foreign key**로 연관관계를 맺고 JOIN을 통해 테이블을 조회한다.

예를 들어 Member 테이블과 Team 테이블의 연관관계를 M:1 관계라 하자.

그렇다면 기본적으로 외래 키는 M 쪽인 Member 테이블에 존재하고,  
Member JOIN Team, Team JOIN Member 양쪽 모두에서 조회가 가능하다.

<hr>

객체의 경우, Member에 Team 멤버 변수를 두어 관계를 맺는다.  
Member -> Team 조회는 가능하지만, Team -> Member 조회할 수 없다. 이러한 관계를 단방향 관계라 부른다.

그렇다면 JPA를 통해 연관관계가 어떻게 매핑되는지 자세히 알아보자.

<hr>

### 다대일 (M : 1) 단방향 관계

```java
@Entity
public class Member {

    @Id
    @GeneratedValue
    private Long id;
    private String memberName;

    @ManyToOne
    @JoinColumn(name="team_id")
    private Team team;
}


@Entity
public class Team {

    @Id
    @GeneratedValue
    private Long id;
    private String teamName;
}
```

위 코드는 Member 테이블에 외래 키인 team_id가 생성되고, 단방향이기 때문에 Team 엔티티에서는 Member를 알 수 없다.

- @ManyToOne
  - M:1 관계를 표현하는 어노테이션
  - @ManyToOne이 붙은 엔티티가 M이고 반대 엔티티가 1일 때 붙인다.
- @JoinColumn
  - 외래 키를 정의하는 어노테이션

<hr>

### 다대일 (M : 1) 양방향 관계

양방향 매핑 코드를 봐보자

```java
@Entity
public class Member {

    @Id
    @GeneratedValue
    private Long id;
    private String memberName;

    @ManyToOne
    @JoinColumn(name="team_id")
    private Team team;
}


@Entity
public class Team {

    @Id
    @GeneratedValue
    private Long id;
    private String teamName;

    //양방향 매핑을 위한 추가
    @OneToMany(mappedBy = "team")
    private List<Team> team = new ArrayList<>();
}
```

Team에 Member를 저장할 필드가 생성된 것을 볼 수 있고,  
@OneToMany 어노테이션이 사용됐다.  
속성 mapppedBy는 양방향 매핑일 때 사용한다.

- JPA는 두 개의 연관관계 중 하나를 고르게 하기 위해 mappedBy를 설정
- mappedBy가 없는 엔티티가 연관관계의 주인
  - mappedBy가 없는 Member 엔티티에 외래 키가 생성

<hr>

### 일대다 (1 : M) 단방향 관계

일반적으로 일대다 단방향 관계 매핑은 권장되지 않고, 다대일 단방향으로 관계를 맺는 것이 좋다.

<hr>

### 일대다 (1 : M) 양방향 관계

일대다 양방향 관계는 존재하지 않는다.

- 일대다 양방향 == 다대일 양방향

<hr>

### 일대일 (1 : 1) 단방향 관계

- 양쪽이 서로 하나의 관계만 가진다.
- 외래 키가 어디에 있든 상관이 없다.

```java
@Entity
public class Member {

    @Id
    @GeneratedValue
    private Long id;
    private String memberName;
}


@Entity
public class Team {

    @Id
    @GeneratedValue
    private Long id;
    private String teamName;

    @OneToOne
    @JoinColumn(name = "member_id")
    private Member member;
}
```

<hr>

### 일대일 (1 : 1) 양방향 관계

```java
@Entity
public class Member {

    @Id
    @GeneratedValue
    private Long id;
    private String memberName;

    @OneToOne(mappedBy = "member")
    private Team team;
}


@Entity
public class Team {

    @Id
    @GeneratedValue
    private Long id;
    private String teamName;

    @OneToOne
    @JoinColumn(name = "member_id")
    private Member member;
}
```

<hr>

### 다대다 (M : M) 관계

두 테이블 사이에 중간 테이블을 두어 관계를 풀어줘야 하는데 실무에서 한계가 존재하기 때문에 지양하자.

**이유**

- 중간 테이블을 묵시적으로 생성해 주기 때문에 복잡한 조인 쿼리가 발생
- 중간 테이블에 필요한 추가 컬럼을 사용할 수 없다.
  - 추가된 컬럼에 대해 매핑이 되지 않기 때문이다.
