# Git&Github

## <u>[Git]</u>

#

## <u>[Github]</u>

<br/>

### _`Trying out Github`_

- we can use Github desktop
- publish file to Github

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
- 내가 개발하는 동안 다른 누군가도 개발해서 마스터 저장소에 먼저 반영하여 <br/>
  마스터 저장소가 업데이트 되는 상황 발생 가능
- fork 하면 기본적으로 upstream 브랜치 생성됨
- upstream 브랜치는 베이스 저장소의 마스터 브랜치와 커뮤니케이션 함 <br/>
  (upstream 브랜치를 이용하여 코드 변경사항 동기화)
- upstream 브랜치를 통해 베이스 저장소의 변경사항 요청 받기 가능
- upstream 브랜치를 통해 베이스 저장소의 최신 코드 가져오기 가능
- fetch origin 이후 upstream 코드를 현재 브랜치에 merge, and then push origin

<br/>

### _`Issues`_

- Issue는 Github의 기능 (Git 기능 X)
- Issues panel
- Issue: 아직 하지 않은 일, 사람들이 발견한 문제/버그 기록
- Issue 생성 후 pull request 시 Issue 명시로 활용 가능
- 라벨 attach 가능
- 피드백 조직화
- 프로젝트 더 잘 관리 가능
- milestone: version 올릴 때 필요한 것들을 모아두는 곳
- milestone 생성 후 그 안에 많은 이슈 할당 가능
- 이슈들이 모두 해결되면 milestone 달성
- 해결된 이슈 리스트화 가능 (milestone)

<br/>

#

### [레퍼런스]

[Reference1](https://nomadcoders.co/git-for-beginners)
