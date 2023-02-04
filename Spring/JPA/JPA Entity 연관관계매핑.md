# JPA Entity 연관관계 매핑 정리/예제

<br>

## 다대일(M:1) 단방향 관계

Member : Team 관계(M:1)를 단방향 관계 매핑을 해보자

```java
@Entity
public class Member {
    @Id
    @GeneratedValue
    private Long id;
    private String MemberName;
    @ManyToOne
    @JoinColumn(name="TEAM_ID")
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

먼저 위 결과를 통해 나온 테이블을 보자.

**Member 테이블**  
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FOEE0a%2FbtqYE6ICbDo%2FZEIalLqnt93u07kKQ0xoY1%2Fimg.png">

**Team 테이블**  
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUrEyF%2FbtqYAucxvBT%2FlgUe55RG1k2zKNjKkkoskK%2Fimg.png">

테이블을 보면 Member 테이블에 외래킹린 TEAM_ID가 생성된 것을 볼 수 있다.  
이것은 `@ManyToOne`, `@JoinColumn` 어노테이션으로 생성된 것이다.  
단방향이기때문에 Team엔티티에서는 Member를 알 수 없다.

- @ManyToOne
  - M : 1 관계를 표현하는 어노테이션이다.
  - @ManyToOne이 붙은 엔티티가 M이고 반대 엔티티가 1일 때 붙인다.
- @JoinColumn
  - 외래키를 정의하는 어노테이션이다.

**@JoinColumn 속성**

- name
  - 매핑할 외래키 이름
  - default는 필드명 + "\_" + 참조하는 테이블 기본키 컬럼명
- referencedColumnName
  - 외래키가 참조하는 대상 테이블의 컬럼명
  - 참조하는 테이블의 기본키 컬럼명
- foreignKey(DDL)
  - 외래 키 제약조건 지정
  - unique, nullable, insertable, updatable, columnDefinition, table

**@ManyToOne 속성**

- optional
  - false : 연관된 엔티티가 항상 있어야한다
- fetch
  - 글로벌 패치 전략 설정
  - @ManyToOne = FetchType.EAGER
  - @OneToMany=FetchType.LAZY
- cascade
  - 영속성 전이 기능 사용
- targetEntity
  - 연관된 엔티티 타입 정보 설정

이제 위에서 매핑한 Entity로 Member, Team을 저장하는 코드를 보자.

```java
public class TestService {
    private final EntityManager em;
    @Transactional
    public void test() {
        Team team = new Team();
        team.setTeamName("test");
        em.persist(team);

        Member member = new Member();
        member.setMemberName("memberTest");
        //member객체에 team객체를 넣어 관계를 맺는다
        member.setTeam(team);
        em.persist(member);
    }
}
```

**Member 테이블**  
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdLXY8A%2FbtqYDleXS9S%2FK9gkZSLXmj0CBiv45tL49K%2Fimg.png">

**Team 테이블**  
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTxkTk%2FbtqYLyErWNj%2FVGdixqoHfxVQGbfYGSwWTk%2Fimg.png">

위 결과를 보면 member.TEAM_ID에 team.id가 값이 매핑되어 있는것을 확인할 수 있다.  
아래는 데이터를 가져오는 코드이다.

```java
public void findTest() {
    Member member = em.find(Member.class, 2L);
    log.info(member.getMemberName());
    log.info(member.getTeam().getTeamName());
}
```

**결과 log**  
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdALJD8%2FbtqYN0UU9xS%2Fcfq3CLnlKZyxACTwUrH7I0%2Fimg.png">

지금은 Member 객체를 찾아 Member가 속한 Team까지 연관관계로 인해 데이터를 가져온다.  
하지만 Team을 find했을 때는 단방향 관계로 인해 Member를 찾을 수가 없다.

<br>

## 다대일(M:1) 양방향 관계

이제 양방향 관계는 어떻게 하는지 보자. 양방향 매핑 코드는 다음과 같다.

```java
@Entity
public class Team {
    @Id
    @GeneratedValue
    private Long id;
    private String teamName;
    //양방향 매핑을 위해 추가
    @OneToMany(mappedBy = "team")
    private List<Member> members = new ArrayList<>();
}

@Entity
public class Member {
    @Id
    @GeneratedValue
    private Long id;
    private String MemberName;
    @ManyToOne
    @JoinColumn(name="TEAM_ID")
    private Team team;
}
```

위의 코드를 보면 Team에 Member를 저장할 필드가 생성된 것을 볼 수 있고, @OneToMany 어노테이션이 사용됐다.  
그리고 속성으로 mappedBy가 사용되었는데 mapppedBy는 양방향 매핑일 때 사용한다.

mappedBy 속성에는 반대쪽 매핑의 필드 이름값을 넣는다.  
위 코드상에서는 Member의 Team객체의 team을 입력한다.

그렇다면 mappedBy는 왜 필요할까?  
이것은 양방향이 서로 다른 단방향 2개로 이루어져있는것과 연관이 있다.

단방향 한개로만 이루어졌을 때 보면 연관관계를 TEAM_ID를 통해 관리한다.  
그렇다면 서로 다른 단방향 2개면 어떻겠는가?  
2개의 연관관계 ID가 필요하게 된다.  
즉, 외래키 2개를 관리하게 될텐데 관계형 데이터베이스는 외래키 1개를 가지고 관리한다.

그래서 JPA는 두개의 연관관계중 하나를 고르게 하기 위해 mappedBy를 설정한다.  
여기서 관리되는 연관관계를 연관관계의 주인이라 한다.  
다시 말해 mappedBy가 없는 엔티티가 연관관계의 주인이다.

위의 코드에서도 mappedBy가 없는 Member 엔티티에 외래키가 생성된다.

그럼 이제 양방향 관계에 데이터를 넣는 코드를 보자.

```java
public class TestService {
    private final EntityManager em;
    @Transactional
    public void test() {
        Team team = new Team();
        team.setTeamName("test");
        em.persist(team);

        Member member = new Member();
        member.setMemberName("memberTest");
        member.setTeam(team);
        em.persist(member);
    }
}
```

위에서 봤던 단방향일때 데이터를 저장하는 코드와 같다.  
이유는 연관관계주인 방향에서 데이터를 입력하면 연관관계 주인이 아닌(Team)에 Member 데이터를 넣지 않아도 데이터베이스에는 정상적으로 들어가기 때문이다.

다음과 같이 연관관계 주인이아닌 곳에만 데이터를 넣었을 경우에는 정상적으로 데이터가 삽입되지 않는다.

```java
public class TestService {
    private final EntityManager em;
    @Transactional
    public void test() {
        Team team = new Team();
        team.setTeamName("test");
        em.persist(team);

        Member member = new Member();
        member.setMemberName("memberTest");
        //관계주인인 member에는 team을 설정하지 않음
        //member.setTeam(team);

        //관계주인이 아닌 team에 member를 추가
        team.getMembers().add(member);
        em.persist(member);
    }
}
```

**Member 테이블**  
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb8a22k%2FbtqYE7gwB9t%2F9nsQufbMXhNxXKVU1Cbuj0%2Fimg.png">

결과를 보면 Member 테이블에 외래키값이 들어가지 않는다.  
이러한 오류를 방지하기 위해서는 양쪽 객체 둘다에게 데이터를 저장해야한다.
