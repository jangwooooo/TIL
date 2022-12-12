# HTTP 메시지

### HTTP 메시지 구조

![img](https://velog.velcdn.com/images/pppp0722/post/879dcdd5-5cca-4885-bb58-481662d717ee/image.png)

<br>

<img src="https://kimsangyeob.github.io/images/http-web-basic/http-messages.png" width="300" height="300"/>

<br>

### start-line

**request-line = method SP(공백) request-target SP HTTP-version CRLF(엔터)**

- method (GET)
- request-target (/search?q=hello&hl=ko)
- HTTP-version (HTTP/1.1)

**status-line = HTTP-version SP status-code SP reason-phrase CRLF**

- HTTP-version (HTTP/1.1)
- status-code (200)
  - 200: 성공
  - 400: 클라이언트 요청 오류
  - 500: 서버 내부 오류
- reason-phrase (OK)

<br>

### header

**header-field = field-name ":" OWS field-value OWS (OWS:띄어쓰기 허용)**

**용도**  
HTTP 전송에 필요한 모든 부가정보

- 예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보,
  서버 애플리케이션 정보, 캐시 관리 정보..

<br>

### message body

**용도**

- 실제 전송할 데이터
- HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능

<br>

### 단숨한 확장 가능

- HTTP는 단순하다.
- HTTP 메시지도 매우 단순하다.
- 크게 성공하는 표준 기술은 단순하지만 확장 가능한 기술이다.
