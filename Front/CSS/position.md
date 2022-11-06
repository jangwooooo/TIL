# position 속성

## postirion 속성이란
`position` 속성은 요소를 어떻게 위치시킬지 정하는 속성이다.  
정확한 위치 지정을 위해 `top`, `right`, `bottom`, `left` 속성과 같이 사용한다.


## 종류

## position: static  
`position` 속성을 별도로 지정해주지 않으면 자동으로 `static` 이 적용된다.  
`static` 요소는 원래 있어야 하는 위치 즉 HTML에 작성된 순서대로 화면에 표시된다.

## position: relative
`poosition` 속성을 `relative`로 설정하면 요소를 원래 위치에서 벗어나게 배치할 수 있다.  
요소의 위치 지정은 `top`, `right`, `bottom`, `left` 속성을 이용해서 할 수 있다.

## position: absolute
속성이 `relative`인 컨테이너에 속성이 `absolute`인 요소가 있다면 배치 기준이 자신이 아닌 `relative` 컨테이너를 기준으로 하게 된다.  
만약 없다면 `<body>`요소가 배치 기준이 된다.

## position: fixed
`position` 속성을 `fixed`로 설정하면 스크롤과 상관없이 항상 화면 좌측상단에 위치하게 된다.  
이유는 배치기준이 자신이나 부모 요소가 아닌 브라우저 전체화면이기 떄문이다.