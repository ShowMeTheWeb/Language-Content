# GIT

### 형상 관리란?
형상 관리(SCM : Software Configuration Management) 는 소프트웨어 개발 프로세스 각 단계에서 소프트웨어의 변경 점을 체계적으로 추적하고 관리하는 일렬의 활동

형상 관리 툴 종류
- 중앙집중식 타입 (Client/Server)
  - CVS (Concurrent Version System)
    > 1980년대 만들어짐. 파일 관리나 커밋 중 오류 발생 시 롤백이 되지 않는다.
  - SVN (Subversion)
    > trunk : 프로젝트에서 가장 중심이 되는 디렉토리<br/>
    > branches : trunk에서 뻗어져 나온 나뭇가지, 프로젝트 내의 작은 프로젝트<br/>
    > tags : 버전 별로 소스코드를 따로 관리하는 공간

- 분산저장소 타입
  - GIT
    > 개발자가 자신만의 commit history를 가질 수 있고, 개발자와 서버의 저장소는 독립적 

### git 의 핵심기능
- git의 핵심기능은 버전 관리(Version Control), 백업(Backup), 협업(Collaboration)으로 나눌 수 있다.


### git 상태
- Working Directory (작업 트리) : 우리 눈에 보이는 디렉터리<br/>
- Staging Area (스테이지) : 버전으로 만들 파일이 대기하는 곳<br/>
- Repository (저장소) : 스테이지에서 대기하고 잇던 파일들을 버전으로 만들어 저장하는 곳


### git 명령어
- git init : 깃 초기화하기 (상태 관리를 시작)
- git status : 깃의 상태
- git add : 스테이지에 올린다
- git commit : 스테이지에 있는 파일을 버전으로 생성
  > git commit -m "저장할 메시지" <br/>
  > git commit -am "저장할 메시지" : 한번이라도 커밋한 파일만 사용 가능
- git config --global user.mail "vaccine1220@naver.com" : git 작업에 사용할 사용자 이메일
- git config --global user.name "SMTW" : git 작업에 사용할 사용자 이름
- git remote add origin https://github.com/ShowMeTheWeb/test123.git
  > 원격 서버 주소를 origin 이라는 이름으로 추가를 하겠다.
- git push origin master : 컴퓨터에 있는것을 서버로 업로드
- git pull origin master : 서버로부터 가져옴 
- git reset --hard 버전 : 최근 커밋과 스테이징, 파일을 해당 버전으로 롤백 (혼자 모든 프로젝트를 할때만 사용)
  > git reset HEAD~1 (현재 커밋의 위치) : 기존 커밋 롤백
- git revert : 깃헙에 올라간 실수한 커밋을 되돌리는것 (커밋이 추가됨)
- git branch : 브랜치를 만들거나 확인하는 명령
  > git branch -d 브랜치 이름 : 브랜치 삭제
- git checkout 브랜치이름 : 현재 브랜치에서 다른 브랜치로 이동
- git merge 브랜치이름 : 현재 브랜치에 브랜치이름을 합친다
- git rebase 브랜치이름 : 현재 브랜치에 브랜치이름을 합친다.
  > merge와 다르게 master가 브랜치를 포함하여 한줄로 표시됨.
- git diff : 수정한 파일이 저장소에 있는 최신 파일과 어떻게 다른지 확인
- git cherry-pick 커밋번호 : 원하는 사항만 빼와서 커밋
- git tag 태그명 : 커밋번호가 별로면 태그달기
- git stash : 임시 저장
- git fetch : 원격 저장소의 커밋들을 로컬 저장소로 가져온다. 병합(Merge)은 따로 해야함