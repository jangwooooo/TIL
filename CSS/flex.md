# Flex

> ## Flex란
레이아웃 배치 전용 기능으로 고안된 속성이다.  
<br/>
- - -
> ## FLex 속성
### flex적용
`display: grid`
>### 배치 방향 설정
가로 방향 배치  
`flex-direction: row`   
세로 방향 배치  
`flex-direction: column`   
역순으로 가로 배치  
`flex-direction: row-reverse`  
역순으로 세로 배치      
`flex-direction: column-reverse`
>### 줄넘김 처리 설정
기본값  
`flex: nowrap`  
담을 공간이 부족할 때 줄넘김    
`flex: wrap`  
담을 공간이 부족할 떄 역순으로 줄넘김  
`flex: wrap-reverse`
>### 메인축 방향 정렬
기본값  
`justify-content: start`  
끝점으로 정렬  
`justify-content: end`  
가운데로 정렬  
`justify-content: center`  
아이템들 사이에 균일한 간격  
`justify-content: space-between`  
아이템들 둘레에 균일한 간격  
`justify-content: space-around`  
아이템들 사이와 양 끝에 균일한 간격  
`justify-content: space-evenly`
>### 수직축 방향 정렬
기본값  
`align-items: stretch`  
시작점으로 정렬  
`align-items: start`  
끝점으로 정렬  
`align-items: end`  
가운데로 정렬  
`align-items: center`  
텍스트 베이스라인 기준으로 정렬  
`align-items: baseline`  
<br/>
>## Flex속성 사용 후기
flex속성을 이용하여 레이아웃을 구성해보니 매우 편하고 유용하여 앞으로 많이 사용할 것 같아 FLex속성에 대해 더 열심히 공부해야 겠다는 생각이 들었다.