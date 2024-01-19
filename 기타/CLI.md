### CLI (Command Line Interface)
> 명령어를 통해 사용자와 컴퓨터가 상호 작용하는 방식

### GUI (Graphic User Interface)
> 그래픽을 통해 사용자와 컴퓨터가 상호작용하는 방식

### 왜 CLI를 사용해야 할까?
-  GUI는 CLI에 비해 사용하기 쉽지만 단계가 많고 성능을 상대적으로 더 많이 소모
- 수많은 서버/ 개발 시스템이 CLI를 통한 조작 환경 제공

### 기초 문법
- `.` :  현재 디렉토리
- `..` : 현재의 상위 디렉토리 (부모 폴더)
	(~/ : 홈 디렉토리 - C드라이브/사용자 )
- `touch` :  파일 생성
- `mkdir` : 새 디렉토리 생성
- `ls` :  현재 작업 중인 디렉토리 내부의 폴더/파일 목록을 보여줌
		폴더(역슬래시가 뒤에 붙음), 파일(x)
- `ls -a` : 숨겨진 파일까지 전부 열람 가능
- `cd` : 현재 작업 중인 디렉토리를 변경 (위치 이동)
- `start` : 폴더/파일 열기
- `code` : 바로 VSCode로 열어줌
-  `rm` : 파일 삭제 (`-r`옵션을 사용해 디렉토리 삭제)
- `vim` : git에서 작업할 수 있음
	- `esc` : command 모드
		- `:q!` : 나가기
		- `:wq` : 저장 후 나가기
	- `i` : edit 모드
- 방향키 위 : 이전 명령어 불러오기

### [[git]] 관련 문법
- `git status` : 현재 git의 상태 (습관화!!! - 안했다가 낭패볼지도ㅠ)
	- Untracked files : 현재 파일중에 생성된 파일이 존재 (한번도 git 버전 관리가 안된 파일 존재) 파일이 빨간색
	- 파일이 초록색 - commit 가능
- `git add 파일명` : 파일을 staging area로
- `git commit -m '주요 변경사항 msg'` : 변경사항에 대한 정보를 msg로 보내면서 commit
- `git log` : 로그 확인
- `git config --global -l` : git global 설정 정보 보기
- `git remote` : 원격 저장소 관련 명령어
	- `git remote add origin remote_repo_url` : origin - 추가하는 원격 저장소 별칭
- `git push (-u) 별칭 브랜치명` : 원격 저장소에 등록 (-u를 쓰면 )
- `git pull` : 원격 저장소의 변경사항만을 받아옴 (업데이트) - local repo가 존재해야 가능(.git 폴더가 있을 때)
- `git clone remote_repo_url` : 원격 저장소 전체를 복제(다운로드) - local repo 없을 때(.git 폴더가 없을 때)
- `git remote rm 원격_저장소_이름` : 현재 로컬 저장소에 등록된 원격 저장소 주소 삭제

### CLI에서 가장 중요한 것
- 내가 어디있는지(경로) 알아야 한다
- 절대 경로 : Root 디렉토리부터 목적 지점까지 거치는 모든 경로를 전부 작성한 것
	> 절대 경로 예시
	> > C:\\\Users\\\SSAFY\\\codes
- 상대 경로 : 현재 작업하고 있는 디렉토리를 기준으로 계산된 상대적 위치를 작성한 것
	>  만약 현재 작업하고 있는 디렉토리가  C:\Users 일 때 절대 경로 예시의 상대 경로는 
	>  >SSAFY\\\codes

