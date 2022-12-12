# URI(Uniform Resource Identifier)

### URI란

URI(Uniform Resource Identifier)란 `통합 자원 식별자`이다.

- Uniform: 리소스 식별하는 통일된 방식
- Resource: 자원, URI로 식별할 수 있는 모든 것(제한 없음)
- Identifier: 다른 항목과 구분하는데 필요한 정보

<br>

### URI 종류

- URL: Uniform Resource Locator
- URN: Uniform Resource Name

![img](https://user-images.githubusercontent.com/53969142/124256208-027fa900-db66-11eb-9062-33b95096e940.png)

<br>

### URL이란

URL은 리소스의 가장 흔한 형태로, 특정 서버의 한 리소스에 대한 구체적인 위치를 서술한다.  
오늘날 대부분의 URI는 URL이다.

#### URL 표준 포맷

- `scheme://[userinfo@]host[:port][/path][?query][#fragment]`
- `https://www.google.com/search?q=hello`  
  <br>

- 프로토콜(https)
- 호스트명(www.google.com)
- 포트 번호(443)
- 패스(/search)
- 쿼리 파라미터(q=hello)

<br>

### URN이란

콘텐츠를 이루는 한 리소스에 대해, 그 리소스 위치에 영향 받지 않는 유일무이한 `이름 역할`을 한다.

#### URN 특징

- urn은 리소스를 여기저기로 옮기더라도 문제없이 동작한다.
