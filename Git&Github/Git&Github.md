# Git&Github

## <u>[Git]</u>

#

## <u>[Github]</u>

<br/>

### _`Trying out Github`_

- We can use Github desktop
- Publish file to Github

<br/>

### _`Forking and Cloning`_

- Fork는 Github의 기능 (Git 기능 x) <br/>
- Forking: Repository copy

<br/>

### _`Pull Requests`_

- 메인 프로젝트 레포지토리를 fork 해서 내 레포지토리로 복사한 후
- 내 local PC에 그 레포지토리를 Cloning을 한다
- 이후 변경사항을 commit & push 하고
- 다시 메인 레포리토리로 pull requests 처리를 한다
- 즉, 모든 동료들이 코드 복사본을 가지고, 변경사항으로 pull request 처리

<br/>

### _`Origin and Upstream`_

- fork 한 후 베이스 코드 저장소에 코드 변경이 있다면 무슨 문제가 생길까??
- 내가 개발하는 동안 다른 누군가도 개발해서 메인 저장소에 먼저 반영하여 <br/>
  메인 저장소가 업데이트 되는 상황 발생 가능
- fork 하면 기본적으로 upstream 브랜치 생성됨
- upstream 브랜치는 베이스 저장소의 메인 브랜치와 커뮤니케이션 함 <br/>
  (upstream 브랜치를 이용하여 코드 변경사항 동기화)
- upstream 브랜치를 통해 베이스 저장소의 변경사항 요청 받기 가능 <br/>
  upstream 브랜치를 통해 베이스 저장소의 최신 코드 가져오기 가능
- fetch origin 이후 upstream 코드를 현재 브랜치에 merge, and then push origin

<br/>

### _`Issues`_

- Issue는 Github의 기능 (Git 기능 X)
- Issues panel
- Issue: 아직 하지 않은 일, 사람들이 발견한 문제/버그 기록
- Issue 생성 후 pull request 시 Issue 명시로 활용 가능
- 라벨 attach 기능
- 피드백 조직화
- 프로젝트 더 잘 관리 가능
- milestone: version 올릴 때 필요한 것들을 모아두는 곳
- milestone 생성 후 그 안에 많은 이슈 할당 가능
- 이슈들이 모두 해결되면 milestone 달성
- 해결된 이슈 리스트화 가능 (milestone)

<br/>

#

## <u>[CLI]</u>

<br/>

### _`CLI log, commit, push`_

- git add 파일이름.확장자명 (working area -> staging area) <br/>
  git add . (this directory - all file)
- git commit -m "commit message" <br/>
  (cf. git commit -help; command help)
- git log: commit 이력 볼 수 있음 <br/>
  HEAD -> main; local PC에 커밋됨 <br/>
  origin/main; github repository에 커밋됨 <br/>
  q를 통해 log 창 나가기
- git push origin main

<br/>

### _`Checkout and Hard Reset`_

- 마지막 커밋 로그 (이전 로그 누적 combination): HEAD <br/>
  HEAD; 현재 파일 정보 위치 표시
- git checkout <돌아가고 싶은 commit 이름> <br/>
  (실제로 과거 커밋 아직 수정 X)
- git checkout main: 다시 원래 상태로 되돌아오기
- git reset --hard HEAD^ <br/>
  --hard: 커밋 삭제, HEAD^: HEAD에서 얼마나 멀리 갈지 표시 <br/>
- ex1) git reset --hard HEAD 현재 같은 장소 그대로 <br/>
  ex2) git reset --hard HEAD^ 한 커밋 이전으로 돌아가기 <br/>
  ex3) git reset --hard HEAD^^ 두 커밋 이전으로 돌아가기 <br/>
  if, doesn't work; git reset --hard "HEAD^" / git reset --hard HEAD~1 (number) <br/>
  hard reset; 리셋하는 파일 삭제, 완전히 과거로 돌아감
- git push origin main --force; 강제 push로 깃허브 커밋 삭제

<br/>

### _`Mixed Reset`_

- git reset HEAD^: mixed reset (복합 리셋) <br/>
  취소할 시, git checkout main
- 선택한 커밋을 다시 untracked로 바꿈 <br/>
  변경사항을 다시 working area로 옮김 (unstaged area)
- 커밋은 이전 상태로 돌아가지만 변경된 파일은 그대로 둠 (삭제 X) <br/>
  hard reset; 이전 커밋으로 돌아가고, 파일 변경 내역 삭제
- 아직 완료되지 않은 파일을 실수로 커밋했을 때 활용

<br/>

### _`Soft Reset`_

- mixed reset과 비슷
- git reset HEAD~2 --soft (2단계 이전으로 돌아감)
- 이전 커밋에서 변경한 내역을 unstaged 영역에 두지 않음 <br/>
  대신 staged 영역에 추가함
- unstaged 영역에 작업중인 파일이 있을 때 섞이지 않고 싶을 때 활용
- 대부분 hard reset으로 되돌려서 다시 시작
- 가끔 mixed reset 하여 git add, commit, push

<br/>

#

## [Note]

- VS Code; M: Modified, U: Untracked, A: added
- origin: 원격 코드 저장소
- 항상 작업 디렉토리에서 git 명령어 수행!
- windows terminal에서 ^ 이 git 명령어로 인식 안될 수 있음
- git remote -v (원격 저장소 확인) <br/>
  git pull origin main (origin 에서 코드 가져오기), conflict 발생 가능 <br/>
  => accept current changed (VS Code) <br/>
  병합 시 충돌 사항 해결하여 add하고 commit 이후 push <br/>
  cf. git push origin main --force (when local and origin both commit mistake)

#

### [Reference]

[Reference1](https://nomadcoders.co/git-for-beginners)
