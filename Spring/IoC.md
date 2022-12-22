# IoC란 무엇인가

### IoC

Inversion of Control(IoC) 말 그대로 `제어의 역전`이다.  
원래 프로그램을 제어하는건 프로그래밍을 하는 개발자이다. 그러나 개발자가 모든 것들을 관리해야한다면 얼마나 힘들겠는가.  
이러한 점을 타파하기 위해 제어권을 제 3자에게 위임하는 것이다.

<br>

### IoC의 분류

#### DL(Dependency Lookup) 과 DI (Dependency Injection)

- DL : 저장소에 저장되어 있는 Bean에 접근하기 위해 컨테이너가 제공하는 API를 이용하여 Bean을 Lockup하는 것
- DI : 각 클래스간의 의존관계를 빈 설정(Bean Definition) 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것
  - Setter Injection (수정자 주입)
  - Constructor Injection (생성자 주입)
  - Method Injection (필드 주입)

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fx4WUU%2Fbtq9gXndYek%2FCwB8xqIdfQh1ox2P9H6bV1%2Fimg.png)

**DL사용시 컨테이너 종속이 증가하기 때문에 주로 DI를 사용한다.**

<br>

### 컨테이너

컨테이너는 보통 객체의 생명주기를 관리, 생성된 인스턴스들에게 추가적인 기능을 제공하도록 하는 것이다.  
즉, 개발자가 작성한 처리과정을 위임받은 존재이다.

<br>

### 스프링 컨테이너의 종류

스프링 컨테이너가 관리하는 객체를 `빈(Bean)`이라고 하고,  
이 빈들을 관리한다는 의미로 컨테이너를 `빈 팩토리(BeanFactory)`라고 부른다.

### BeanFactory

- Bean을 등록,생성,조회,반환 관리를 한다.
- Bean을 조회할 수 있는 getBean()메서드가 정의되어 있다.
- 보통은 BeanFactiory를 바로 사용하지 않고, 이를 확장한 ApplicationContext를 사용한다.

### ApplicationContext

- Bean을 등록,생성,조회,반환 관리하는 기능은 BeanFactory와 같다.
- 스프링의 각종 부가 기능을 추가로 제공한다.
- BeanFactory보다 추가적으로 제공하는 기능
  - 국제화가 지원되는 텍스트 메시지를 관리 해준다.
  - 이미지같은 파일 자원을 로드할 수 있는 포괄적인 방법을 제공해준다.
  - 리스너로 등록된 빈에게 이벤트 발생을 알려준다.

**따라서 대부분의 어플리케이션에서는 BeanFactory 보다는 ApplicationContext를 사용하는 것이 더 좋다.**
