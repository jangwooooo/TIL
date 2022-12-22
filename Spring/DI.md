# 의존성 주입

**Spring은 @Autowired 어노테이션을 이용한 다양한 의존성 주입(DI; Dependency Injection) 방법을 제공합니다.**
의존성 주입은 필요한 객체를 직접 생성하는 것이 아닌 외부로부터 객체를 받아 사용하는 것입니다.  
이를 통해 객체간의 결합도를 줄이고 코드의 재활용성을 높일 수 있습니다.  
@Autowired 는 Spring에게 의존성을 주입하는 지시자 역할로 쓰입니다.

<br>

### 의존성 주입을 해야 하는 이유

- Test가 용이해진다.
- 코드의 재사용성을 높여준다.
- 객체 간의 의존성(종송석)을 줄이거나 없앨 수 있다.
- 객체 간의 결함도를 낮추면서 유연한 코드를 작성할 수 있다.

<br>

### 의존성 주입의 3가지 방법

1. 생성자 주입(Construction Injection)
2. 필드 주입(Field Injection)
3. 수정자 주입(Setter Injection)

의존성 주입은 위의 3가지 방법이 있다. 그렇다면 어떤 주입 방법을 사용하는게 가장 좋을까?  
우선, 의존성 주입 방법을 하나씩 알아보자.

## 1. 생성자 주입(Constructor Injection)

```java
@Controller
public class CocoController {
  //final을 붙일 수 있음
    private final CocoService cocoService;
  //---------------------------------------------------------
  //@Autowired
    public CocoController(CocoService cocoService) {
        this.cocoService = cocoService;
    }
}
```

클래스의 생성자가 하나이고, 그 생성자로 주입받을 객체가 빈으로 등록되어 있다면 @Autowired를 생략할 수 있다.

### 2. 필드 주입(Field Injection)

```java
@Controller
public class CocoController {

    @Autowired
    private CocoService cocoService;
}
```

필드에 @Autowired 어노테이션만 붙여주면 자동으로 의존성 주입된다.

**단점**

- 외부에서 변경하기 힘들다.
- 프레임워크에 의존적이고, 객체지향적으로 좋지 않다.

### 3. 수정자 주입(Setter Injection)

```java
@Controller
public class CocoController {
    private CocoService cocoService;

    @Autowired
    public void setCocoService(CocoService cocoService) {
    	this.cocoService = cocoService;
    }
}
```

Setter 메소드에 @Autowired 어노테이션을 붙이는 방법이다.

**단점**

- 수정자 주입을 사용하면 setXXX 메서드를 public으로 열어두어야 하기 때문에 언제 어디서든 변경이 가능하다.

<br>

## 어떤 주입 방식을 사용하는게 좋을까?

Spring Framwork reference에서 권장하는 방법은 `생성자를 통한 주입`이다.  
@Autowired 어노테이션만으로 간단하게 의존성을 주입할 수 있는데 왜 생성자 주입 방법을 권장하는걸까?  
필드 주입이나 수정자 주입과 다르게 생성자 주입 방법이 주는 장점에 대해 알아보자.

### 생성자 주입을 권장하는 이유

### 1. 순환참조를 방지할 수 있다.

개발을 하다 보면 여러 컴포넌트 간에 의존성이 생긴다.  
예를 들어, 서로 참조하여 순환 참조되는 코드가 있다고 가정해 보자.  
필드 주입과 수정자 주입은 빈이 생성된 후에 참조를 하기 때문에 어플리케이션이 아무런 오류 그리고 경고 없이 구동된다.  
그리고 그것은 실제 코드가 호출될 때까지 문제를 알 수 없다.  
반면, 생성자를 통해 주입하고 실행하면 BeanCurrentlyInCreationException이 발생하게 된다.  
순환 참조 뿐만아니라 더 나아가서 의존 관계에 내용을 외부로 노출 시킴으로써 어플리케이션을 실행하는 시점에서 오류를 체크할 수 있다.

### 2. 불변성

생성자로 의존성을 주입할 때 final로 선언할 수 있고, 이로인해 런타임에서 의존성을 주입받는 객체가 변할 일이 없어진다.  
하지만 수정자 주입이나 일반 메소드 주입을 이용하게되면 불필요하게 수정의 가능성을 열어두게 되고,  
이는 OCP(Open-Closed Principal, 개방-폐쇄의 원칙)를 위반하게 된다.  
그러므로 생성자 주입을 통해 변경의 가능성을 배제하고 불변성을 보장하는 것이 좋다.  
또한, 필드 주입 방식은 null이 만들어질 가능성이 있는데, final로 선언한 생성자 주입 방식은 null이 불가능하다.

### 3. 테스트에 용이하다

생성자 주입을 사용하게 되면 테스트 코드를 좀 더 편리하게 작성할 수 있다.  
DI의 핵심은 관리되는 클래스가 DI 컨테이너에 의존성이 없어야 한다는 것이다.  
즉, 독립적으로 인스턴스화가 가능한 POJO(Plain Old Java Object)여야 한다는 것이다.

### 결론

위와 같은 이유로 필드 주입이나 수정자 주입 보다는 생성자 주입의 사용을 권장한다.
