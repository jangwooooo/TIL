# SOLID

클린코드로 유명한 로버트 마틴의 좋은 객체 지향 설계의 5가지 원칙을 정리

- SRP : 단일 책임 원칙 ( Single resposibility principle )
- OCP : 개방-폐쇄 원칙 ( Open/closed principle )
- LSP : 리스코프 치환 원칙 ( Liskov substitution principle )
- ISP : 인터페이스 분리 원칙 ( Interface segregation principle )
- DIP : 의존관계 역전 원칙 ( Dependency inversion principle )

<br>

### SRP 단일 책임 원칙

Single responsibility principle

- 한 클래스는 하나의 책임만 가져야 한다.
- 하나의 책임의 기준은 변경이다, 변경이 있을 때 파급 효과가 적어야 한다.

<br>

### OCP 개방-폐쇄 원칙

Open/closed principle

- 소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.
- 다형성을 활용해야 한다.
- 인터페이스를 구현한 새로운 클래스를 하나 만들어서 새로운 기능을 구현한다.

<br>

### LSP 리스코프 치환 원칙

Liskov substitution principle

- 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.
- 다형성에서 하위 클래스는 인터페이스 규약을 다 지켜야 한다는 것.
- ex ) 자동차 인터페이스의 엑셀을 앞으로 가는 기능, 뒤로 가게 구현하면 LSP 위반이다.

<br>

### ISP 인터페이스 분리 원칙

Interface sertrgation principle

- 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.
- 분리하면 인터페이스 자체가 변해도 클라이언트에 영향을 주지 않는다.
- 인터페이스가 명확해지고, 대체 가능성이 높아진다.

<br>

### DIP 의존관계 역전 원칙

Dependency inversion principle

- 구현 클래스에 의존하지 말고, 인터페이스에 의존해야 한다.
