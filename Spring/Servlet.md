# Servlet

### Servlet이란?

```
클라이언트의 요청을 처리하고, 그 결과를 반환하는 Servlet 클래스의 구현 규칙을 지킨 자바 웹 프로그래밍 기술
```

간단히 말해서, 서블릿이란 `자바를 사용하여 웹을 만들기 위해 필요한 기술`이다.  
예를 들어,어떠한 사용자가 로그인을 하려고 할 때. 사용자는 아이디와 비밀번호를 입력하고,로그인 버튼을 누릅니다.  
그때 서버는 클라이언트의 아이디와 비밀번호를 확인하고, 다음 페이지를 띄워주어야 하는데, 이러한 역할을 수행하는 것이 바로 Servlet이다.

<br>

### Servlet 동작 방식

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F993A7F335A04179D20">

1. 사용자(클라이언트)가 URL을 입력하면 HTTP Request가 Servlet Container로 전송합니다.
2. 요청을 전송받은 Servlet Container는 HttpServletRequest, HttpServletResponse 객체를 생성합니다.
3. web.xml을 기반으로 사용자가 요청한 URL이 어느 서블릿에 대한 요청인지 찾습니다.
4. 해당 서블릿에서 service메소드를 호출한 후 클리아언트의 GET, POST여부에 따라 doGet() 또는 doPost()를 호출합니다.
5. doGet() or doPost() 메소드는 동적 페이지를 생성한 후 HttpServletResponse객체에 응답을 보냅니다.
6. 응답이 끝나면 HttpServletRequest, HttpServletResponse 두 객체를 소멸시킵니다.

<br>

### Servlet Container

```
Servlet을 관리해주는 컨테이너
```

우리가 서버에 서블릿을 만들었다고 해서 스스로 작동하는 것이 아니고 `서블릿을 관리해주는 것`이 필요한데, 그러한 역할을 하는 것이 바로 서블릿 컨테이너 입니다.  
서블릿 컨테이너는 **클라이언트의 요청(Request)을 받아주고 응답(Response)할 수 있게, 웹서버와 소켓으로 통신**하며 대표적인 예로 톰캣(Tomcat)이 있습니다.
