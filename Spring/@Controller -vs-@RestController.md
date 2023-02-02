# @Controller와 @RestController 비교

Spring에서는 컨트롤러를 지정해주기 위한 어노테이션으로 @Controller와 @Restcontroller를 사용합니다.

<br>

## @Controller

전통적인 Spring MVC의 컨트롤러인 @Controller는 주로 `View`를 반환하기 위해 사용한다.  
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbED6o9%2Fbtrx1wyKwpF%2FNtSlrTohpAI79l6MA95SZ1%2Fimg.png"/>

Controller가 반환한 뷰의 이름으로부터 View를 렌더링하기 위해서는 `ViewResolver`가 사용되며, ViewResolver 설정에 맞게 View를 찾아 렌더링한다.

<br>

하지만 Spring MVC의 컨트롤러를 사용하면서 Data를 반환해야 하는 경우도 있다.  
컨트롤러에서는 데이터를 반환하기 위해 @ResponseBody를 활용해주어야 한다.  
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb3McJC%2Fbtrx1IGcnGs%2F2iHFmw3bbqasfCJzwCKYuK%2Fimg.png">

객체를 반환하기 위해서는 viewResolver 대신에 `HttpMessageConverter`가 동작한다.  
HttpMessageConverter에는 여러 Convert가 등록되어 있고, 반환해야 하는 데이터에 따라 사용되는 Converter가 달라진다.  
단순 문자열인 경우에는 StringHttpMessageConverter가 사용되고, 객체인 경우에는 MappingJackson2HttpMessageConverter가 사용된다.  
Spring은 클라이언트의 HTTP Accept 헤더와 서버의 컨트롤러 반환 타입 정보 둘을 조합해 적합한 HttpMessageConverter를 선택하여 이를 처리한다.

<br>

## @RestController

@RestController는 @Controller에 @ResponseBody가 추가된 것이다.  
당연하게도 @RestController의 주용도는 Json 형태로 객체 데이터를 반환하는 것이다.  
이러한 이유로 동작 과정 역시 @Controller에 @ReponseBody를 붙인 것과 완벽히 동일하다.  
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FH03z4%2Fbtrx1IGclWg%2FcMTcF0HrJBYiahwCPsFME0%2Fimg.png">
