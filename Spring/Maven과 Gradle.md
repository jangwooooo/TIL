# Maven과 Gradle 비교

## 메이븐(Maven)

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPA9i4%2Fbtq8bsoZE6Y%2FxNQw1nKBQP2i2OURKZDZn0%2Fimg.png)

### Maven이란?

- 아파치 메이븐은 자바용 프로젝트 관리 도구이다.
- 아파치 Ant의 대안으로 만들어졌다.
- 아파치 라이센스로 배포되는 오픈 소스 소프트웨어이다.

프로젝트를 진행하면서 사용하는 수많은 라이브러리들을 관리해주는 도구이다.  
여기서 메이븐의 특징은 그 라이브러리들과 연관된 라이브러리들까지 모두 연동이 되서 관리가 된다는 점이다.  
즉, 메이븐은 네트워크를 통해 연관된 라이브러리까지 같이 업데이트를 해주기 떄문에 사용이 편리하다.

### POM - Project Objext Model

Maven의 기능을 이용하기 위해 POM이 사용된다.  
POM은 약자 이름 그대로 Project Objext Model의 정보를 담고 있는 파일이다.  
pom.xml에서 주요하게 다루는 기능들은 아래와 같다.

- 프로젝트 정보 : 프로젝트의 이름, 라이센스 등
- 빌드 설정 : 소스, 리소스, 생명주기별 실행한 플러그인 등 빌드와 관련된 설정
- 빌드 환경 : 사용자 환경 별로 달라질 수 있는 프로파일 정보
- pom 연관 정보 : 의존 프로젝트(모듈), 상위 프로젝트, 포함하고 있는 하위 모듈 등

<hr>
<br>

## 그래들(Gradle)

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEh1RA%2Fbtq79q6tnlQ%2FCQZ2CP3BJgDKBAiKAmCWLk%2Fimg.png)

### Gradle이란?

- 빌드,프로잭트 구성/관리, 테스트, 배포 도구
- 안드로이드 앱의 공식 빌드 시스템
- 빌드 속도가 Maven에 비해 10~100배 가량 빠름
- JAVA, C/C++M Python 등을 지원
- 빌드툴인 Ant Builder와 Groovy 스크립트 기반으로 만들어져 기존 Ant의 역할과 배포 스크립트의 기능을 모두 사용 가능

  **Groovy?**  
  Groovy는 Java 가상 머신에서 실행되는 스크립트 언어다. Java 가상 머신에서 동작하지만,  
   Java와는 달리 소스 코드를 컴파일 할 필요는 없다.  
   Groovy는 스크립트 언어이고, 소스 코드를 그대로 실행한다.  
   또한 Java와 호환되고, Java 클래스 파일을 그대로 Groovy 클래스로 사용할 수 있다.  
   Java 문법과 유사하여 빌드 처리를 관리할 수 있는 면에서

<br>
기존 메이븐의 경우 XML로 라이브러리를 정의하고 활용하도록 되어 있으나,

Gradle의 경우 별도의 빌드 스크립트를 통하여 사용할 어플리케이션 버전, 라이브러리 등의 항목을 설정할 수 있다.  
Groovy 스크립트 언어로 구성되어 있기에 XML과 달리 변수선언, if, else, for등의 로직이 구현가능하며 간결하게 구성이 가능하다.

<hr>
<br>

## 메이븐(Maven) VS 그래들(Gradle)

먼저 같은 기능과 라이브러리 의존성을 가지는 maven과 gradle의 스크립트를 비교해 보자  
<br>

### pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.5.2</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.example2</groupId>
    <artifactId>demo-maven</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>demo-maven</name>
    <description>Demo project for Spring Boot</description>
    <properties>
        <java.version>11</java.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```

<br>

### build.gradle

```gradle
plugins {
    id 'org.springframework.boot' version '2.5.2'
    id 'io.spring.dependency-management' version '1.0.11.RELEASE'
    id 'java'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '11'

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

test {
    useJUnitPlatform()
}
```

<br>

1. 스크립트 길이와 가독성 면에서 gradle이 우세하다.
2. 빌드와 테스트 실행 결과 gradle이 더 빠르다. (gradle은 캐시를 사용하기 떄문에 테스트 반복 시 차이가 더 커진다.)
3. 의존성이 늘어날 수록 성능과 스크립트 품질의 차이가 심해질 것이다.

<br>

maven은 프로젝트가 커질수록 빌드 스크립트의 내용이 길어지고 가독성이 떨어진다.  
반면에 gradle은 훨씬 적은 양의 스크립트로 짧고 간결하게 작성할 수 있다.

<br>

maven이 정적인 형태의 XML 기반으로 작성되어 동적인 빌드를 적용할 경우 어려움이 많다면,  
gradle은 Groovy를 사용하기 때문에 동적인 빌드는 Groovy 스크립트로 플러그인을 호출하거나 직접 코드를 짜면 된다.

<br>

maven의 경우 멀티 프로젝트에서 특정 설정을 다른 모듈에서 사용하려면 상속을 받아야 하지만,  
gradle은 설정 주입 방식을 사용하기 때문에 멀티 프로젝트에 매우 적합하다.

<br>
아래 사진은 gradle과 maven의 속도 비교 표이다.

**Gradle vs Maven : Performance Comparison**

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdKtmEU%2Fbtq8bsvQoKc%2FDjilAAylpcHLJFRtXQCd01%2Fimg.png)
![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbS9riQ%2Fbtq8aN1zMjC%2FKn1fpOCrvzF1lWKkoDNy4K%2Fimg.png)
![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcEGqWA%2Fbtq8dulsWv5%2FRPudjkBsjzmp0gKd3Qk0z1%2Fimg.png)
![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1me5I%2Fbtq8aOznGOG%2FMMblyASIa9QaGkmi9xEw30%2Fimg.png)
<br>

과거에는 maven을 많이 사용했었지만 요즘은 gradle로 넘어오는 추세이다.
