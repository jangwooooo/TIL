# border

## border 속성이란
`border`속성은 태그의 테두리를 설정하는 속성이고, 세부적인 속성들을 한번에 쓸 수 있는 속성이다. width-style-color 순서로 사용.
* border-width : 테두리의 두께를 설정
* border-style : 테두리의 스타일(점선, 실선)을 설정
* border-color : 테두리의 색상을 설정
* border-top : 테두리의 위쪽만 설정
* border-bottom : 테두리의 아래쪽만 설정
* border-left : 테두리의 왼쪽만 설정
* border-right : 테두리의 오른쪽만 설정

## 사용 예시
    .style {
        border: 4px dotted green;       상하좌우 테두리 전부 두께4px, 점선, 초록색
        border-bottom: 5px solid blue;  아래쪽 테두리만 두께5px, 실선, 파란색
    }


