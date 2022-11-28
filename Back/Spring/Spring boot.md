# Spring boot

## Spring boot란?

- Spring framework 기반 프로젝트를 복잡한 설정없이 쉽고 빠르게 만들어주는 라이브러리.
- 스프링을 쉽게 사용할 수 있도록 필요한 여러가지 복잡한 설정을 대부분 미리 세팅해놓아 바로 웹개발을 가능하게 한다.

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcmuOwd%2FbtrfpPjNC6t%2FSiYsRR6rE3ikyTJmKKK8w1%2Fimg.png)

## Spring boot 장점

<br>

**1. 라이브러리 관리 자동화**  
스프링부트의 Starter 라이브러리를 등록해서 라이브러리 의존성을 간단히 관리할 수 있다.

**2. 설정 자동화**  
스프링 부트는`@EnableAutoConfiguration` 어노테이션을 선언해서 스프링에서 자주 사용했던 설정들을 알아서 등록해준다.  
이 기능이 스프링 부트의 마법이라고 불린다고 한다.

**3. 내장Tomcat**  
스프링 부트는 WAS인 `Tomcat`을 내장하고 있다.  
`@SpringBootApplication` 어노테이션이 선언되어 있는 클래스의 main()메소드를 실행하는 것만으로 서버를 구동시킬 수 있다.  
내장 톰캣을 사용하기 위한 별도 설정없이 `web starter` 의존성만 추가해주면 된다.

**4. 독립적으로 실행 가능함**  
웹 프로젝트라면 war파일로 패키징 해야하는데 스프링 부트는 내장 Tomcat을 지원하기 때문에 jar 파일로 패키징해서 웹 애플리케이션을 실행시킬 수 있다.
