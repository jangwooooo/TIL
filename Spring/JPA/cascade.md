# Cascade

## Cascade란

영속성 정의로, 특정 엔티티를 영속 상태로 만들 때 연관된 엔티티도 함께 영속 상태로 만들고 싶은 경우에 사용합니다.

<br>

## Cascade 종류

- ALL : 모두 적용
- PERSIST : 영속
- REMOVE : 삭제
- MERGE : 병합
- REFRESH : REFRESH
- DETACH : DETACH

거의 ALL, PERSIST, REMOVE만 쓰인다.

<br>

## 영속성 전이 : 저장

CascadeType.PERSIST

```java
@Entity
public class Parent {
    ...
    @OneToMany(mappedBy = "parent", cascade = CascadeType.PERSIST)
    private List<Child> children = new ArrayList<>();
    ...
}
```

```java
    Child child1 = new Child();
    Child child2 = new Child();

    Parent parent = new Parent();
    child1.setParent(parent);
    child2.setParent(parent);
    parent.getChildren().add(child1);
    parent.getChildren().add(child2);

    em.persist(parent);  // child도 영속성 전이로 저장
```

이 처럼 부모만 영속화해도 `CascadeType.PERSIST`로 설정한 **자식 엔티티까지 함께 영속화** 하여 저장한다.

<br>

## 영송석 전이 : 삭제

CascadeType.REMOVE

```java
@Entity
public class Parent {
    ...
    @OneToMany(mappedBy = "parent", cascade = CascadeType.REMOVE)
    private List<Child> children = new ArrayList<>();
    ...
}
```

```java
    Parent findParent = em.find(Parent.class, 1L);
    em.remove(findParent);
```

이 처럼 부모만 `CascadeType.REMOVE`로 설정하고 다음처럼 부모 엔티티만 삭제해도 **연관된 자식 엔티티도 함께 삭제**된다.

<br>

## 고아 객체 (Orphan)

**OrphanRemoval**  
JPA에서는 부모와 연관관계가 끊어진 자식을 자동으로 삭제하는 기능을 제공하는데 이를 고아 객체 제거라고 한다.

```java
@Entity
public class Parent {
    ...
    @OneToMany(mappedBy = "parent", OrphanRemoval = true)
    private List<Child> children = new ArrayList<>();
    ...
}
```

```java
    Parent parent = em.find(Parent.class, 1L);
    parent.getChildren().remove(0);   // 자식 엔티티를 컬렉션에서 제거 -> 고아 객체가 되어 삭제
```

`OrphanRemoval`을 이용하면, 부모의 컬렉션에서 자식의 참조만 제거하면 **자식 엔티티가 자동으로 삭제**된다.
