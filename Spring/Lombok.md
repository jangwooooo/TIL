# Lombok

### Lombok이란?

Lombok이란 어노테이션 기반으로 코드를 자동완성 해주는 라이브러리이다.

<br>

### Lombok 장점

- 어노테이션 기반의 코드 자동 생성을 통한 생산성 향상
- 반복되는 코드 다이어트를 통한 가독성 및 유지보수성 향상
- Getter, Setter 외에 빌더 패턴이나 로그 생성 등 다양한 방면으로 활용 가능

<br>

### @Getter @Setter

Lombok에서 가장 자주 활용하는 어노테이션이다.  
@Getter와 @Setter를 클래스 이름 위에 적용시키면 모든 변수들에 적용이 가능하고, 변수 이름 위에 적용시키면 해당 변수들만 적용 가능하다.

<br>

### @AllArgsConstructor

모든 변수를 사용하는 생성자를 자동완성 시켜주는 어노테이션이다.

<br>

### @NoArgsConstructor

어떠한 변수도 사용하지 않는 기본 생성자를 자동완성 시켜주는 어노테이션이다.

<br>

### @RequiredArgsConstructor

특정 변수만을 활용하는 생성자를 자동완성 시켜주는 어노테이션이다.  
생성자의 인자로 추가할 변수에 @NonNull 어노테이션을 붙여서 해당 변수를 생성자의 인자로 추가할 수 있다.  
아니면 해당 변수를 final로 선언해도 의존성을 주입받을 수 있다.

<br>

### @EqualsAndHashCode

클래스에 대한 equals 함수와 hashCode 함수를 자동으로 생성해준다.

<br>

### @ToString

클래스의 변수들을 기반으로 ToString 메소드를 자동으로 완성시켜 준다.  
출력을 원하지 않는 변수에 @ToString.Exclude 어노테이션을 붙여주면 출력을 제외할 수 있다.  
또한 상위 클래스에 대해도 toString을 적용시키고자 한다면 상위 클래스에 @ToString(callSuper = true) 를 적용시키면 된다.

<br>

### @Data

@ToString, @EqualsAndHashCode, @Getter, @Setter, @RequiredArgsConstructor를 자동완성 시켜준다.  
실무에서는 너무 무겁고 객체의 안정성을 지키기 때문에 @Data의 활용을 지양한다.

<br>

### @Builder

해당 클래스의 객체의 생성에 Builder패턴을 적용시켜준다.  
모든 변수들에 대해 build하기를 원한다면 클래스 위에 @Builder를 붙이면 되지만, 특정 변수만을 build하기 원한다면 생성자를 작성하고 그 위에 @Builder 어노테이션을 붙여주면 된다.
