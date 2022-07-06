# Git
## Git이란
- - -
Git이란 `분산형 버전 관리 시스템`의 한 종류이다  
.  
.
## Git을 사용하는 이유
- - -
`버전 관리`가 편리하고 분산개발,작업내역관리,병렬개발 등 많은 장점을 가지고 있다.  
.  
.  
## Git 용어
- - -
## - repository
저장소를 의미하며, 저장소는 히스토리, 태그, 소스의 branch에 따라 버전을 저장한다. 저장소를 통해 작업자가 변경한 모든 히스토리를 확인 할 수 있다.
## - staging area
저장소에 커밋하기 전에 커밋을 준비하는 위치
## - commit
현재 변경된 작업 상태를 점검을 마치면 확정하고 저장소에 저장하는 작업  
## - branch
분기점을 의미하며, 작업을 할때에 현재 상태를 복사하여 Branch에서 작업을 한 후에 완전하다 싶을때 Merge를 하여 작업을 한다  
## - merge
다른 Branch의 내용을 현재 Branch로 가져와 합치는 작업을 의미한다  
.  
. 
## Git 명령어
- - -
### 깃 저장소 초기화
`git init`
### 원격저장소의 저장소를 local에 복사
`git clone`
### 레포 연결하기
`git remote add origin [레포주소]`
### 연결된 레포 제거
`git remote remove origin`
### 특정 파일을 staging area에 올린다
`git add [파일이름]`
### 모든 파일을 staging area에 올린다
`git add .`
### 커밋하고 커밋이름을 저장한다
`git commit -m "커밋이름"`
### 코드 변경 이력을 원격 저장소로 전송한다
`git push [저장소명] [브랜치명]`