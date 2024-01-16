[[CLI]]
### git init
: 로컬 저장소 설정 초기화
git의 버전 관리를 시작할 디렉토리에서 
- [!] 주의사항
- git 로컬 저장소 내에 또다른 git 로컬 저장소를 만들지 말 것
- (master)가 없을 때만 !!
- git 저장소 안에 git 저장소가 있을 경우 가장 바깥 쪽의 git 저장소가 안쪽의 git 저장소의 변경사항을 추적할 수 없기 때문
# __Working Directory : 현재 작업__
### git add
: 변경사항이 있는 파일을 staging area에 추가
# __Staging Area : 선별장__
### git commit
: 선별해서 저장소로 보내는 작업
# __Repository : 저장소__
#### Remote Repository : 원격 저장소
: 코드와 버전 관리 이력을 온라인 상의 특정 위치에 저장하여 여러 개발자가 협업하고 코드를 공유할 수 있는 저장 공간
ex) GitLab, GitHub, Bitbucket
#### Local Repository : 로컬 저장소
: 개인 컴퓨터 (add, commit 모두 로컬에 저장)
#### 로컬 -> 원격
1. remote repo 생성
2. local에 remote repo 등록 `git remote add 별칭 remote_repo_url`
3. local에서 push 한다. `git push 별칭 브랜치명`
- [!] commit 이력이 없다면 push 할 수 없다!!

pull 작업 add commit push

#### .gitignore
: Git에서 특정 파일이나 디렉토리를 추적하지 않도록 설정하는데 사용되는 텍스트 파일
(버전관리가 필요없는 것들)
- [!] 파일명 앞에 .이 붙어있으면 숨김의 의미를 가짐 (`ls -a`사용해야 보임)

#### github은 어디에 활용할까?
- 개인 포트폴리오
- 프로젝트 협업

#### github 활용하기
- TIL(Today I Learned)을 통해 내가 학습하는 것을 기록
	- TIL : 매일 내가 배운 것을 마크다운으로 정리해서 문서화하는 것
	- [!] 단순히 배운 것만을 필기하는 것이 아닌 스스로 더 나아가 어떤 학습을 했는지를 기록하는 것

#### '문서화'의 중요성
: 신입 개발자에게 요구되는 가장 중요한 덕목
[네이버 개발 블로그](https://d2.naver.com/news/3435170)

#### github profile

#### README.md
- [!] 반드시 .git과 같은 위치에 있어야함

