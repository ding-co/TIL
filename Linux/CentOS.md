## [CentOS 리눅스 소개]

### _리눅스_

- 유닉스 (상용 OS)
- 리눅스는 무료 유닉스
- 리누스 토르발스 (커널 개발)
- CentOS [센토스] 도 리눅스의 배포판 중 하나

### _GNU 프로젝트_

- 리차드 스톨만 시작
- 목표: 모두가 공유할 수 있는 소프트웨어
- GPL 라이센스 (General Public License); 자유 소프트웨어 <br/>
  소프트웨어 수정 + 판매 등 자유 보장 but, 소스 오픈해야함

### _커널_

- [최신버전](https://kernel.org)
- CentOS8은 커널 4.18 포함
- 주버전.부버전.패치버전 (커널) <br/>
  Major.Minor.Patch version
- 기본 커널에서 최신 커널로 업그레이드 (커널 컴파일) 가능

### _Red hat Linux 와 CentOS Linux_

- 가장 유명한 배포판 중 하나가 Red Hat 사에서 제작한 Red Hat Linux
- 상용 - RHEL (Red Hat Enterprise Linux) <br/>
  GPL로 인해 공개된 소스코드 가져가서 로고만 변경한 후 <br/>
  다시 컴파일/빌드 해서 만든 것이 CentOS
- RHEL ~= CentOS
- 기업 별도 비용 => RHEL 사용! / 비용 절감 => CentOS
- Fedora (시험판) -> RHEL -> CentOS
- 64-bit CPU, HDD 20GB 이상, RAM 4GM 권장 <br/>
  (VMware는 더 높은 사양 요구됨)

#

## [CentOS8 리눅스 설치 - Server]

### _CentOS 리눅스 설치_

- Server 설치 및 설정

  - VMware Player - Server - edit - CD/DVD iso 파일 넣기 (connect 체크)
  - test 할 필요 없이 바로 install
  - 설정

    - 한국어 - 시간 및 날짜 서울 선택, 네트워크 이더넷 켬, 소프트웨어 선택 워크 스테이션, 설치 목적지 디스크 2번 클릭 후 custom 체크 - 파티션 2개로 분할 - 표준 파티션, +, swap, 4G (임시 메모리 공간) - / 파티션 (root 파티션)
    - root 비번 설정 - 완료 2번 - 일반 사용자 설정 - 완료 2번 - 재부팅
    - 라이센스 약관 동의 - 완료 - 설정 완료
    - 목록에 없습니까 - root - 로그인
    - 한국어 - 한국어 (한글) - 건너뛰기 - CentOS 시작
    - 화면 사이즈; 우측 상단 설정 아이콘 - 장치 - 디스플레이 - 해상도 (1024x768) 적용 - 유지
    - 개인 정보 - 화면 잠금 - 자동 화면 잠금 끔, 알림 표시 끔
    - 전원 - 빈 화면 안함

      ```linux
        # 자동 업데이트 끄기; 현재 활동 - 터미널
        [root@localhost ~]# gsettings set org.gnome.software download-updates false
        [root@localhost ~]# systemctl disable dnf-makecache.service
        [root@localhost ~]# systemctl disable dnf-makecache.timer
      ```

    - CentOS8 업데이트 자동 설치 해제 (현재 버전 유지)

      - [This.repo 내용](https://cafe.naver.com/thisislinux/6620)

      ```linux
      [root@localhost ~]# cd /etc/yum.repos.d/
      [root@localhost ~]# mkdir backup
      [root@localhost ~]# ls
      [root@localhost ~]# mv *.repo backup/
      [root@localhost ~]# ls
      [root@localhost ~]# gedit This.repo

      # 내용 복사 및 붙여넣기 - 저장

      [root@localhost ~]# dnf clean all
      [root@localhost ~]# exit
      ```

    - 서버 컴퓨터의 네트워크 - 고정 IP 설정

      - 서버 IP -> 고정 IP로 설정

      ```centos8
      [root@localhost ~]# cd /etc/sysconfig/network-scripts/
      [root@localhost ~]# ls
      [root@localhost ~]# gedit ifcfg-ens160

      # BOOTPROTO="none"
      # IPADDR="192.168.111.100"
      # NETMASK="255.255.255.0"
      # GATEWAY="192.168.111.2"
      # DNS1="192.168.111.2"

      # 네트워크 장치 내림
      [root@localhost ~]# nmcli connection down ens160

      # 네트워크 장치 올림
      [root@localhost ~]# nmcli connection up ens160

      # 가상머신 재부팅
      [root@localhost ~]# reboot

      [root@localhost ~]# ifconfig ens160

      # inet 192.168.111.100 만 체크!
      ```

    - 보안 기능 해제; selinux 해제

      ```centos8
      [root@localhost ~]# gedit /etc/sysconfig/selinux

      # SELINUX=disabled
      ```

    - 한글 설정

      - 우측 상단 설정 - 지역 및 언어 - 한국어(한글)만 남김

    - 해상도 수동 설정

      ```centos8
      [root@localhost ~]# gedit /etc/grub.d/10_linux

      # 169행쯤, 773 => 1024x768 해상도
      # ~ ~ ro ${args} vga=773"

      # 변경한 해상도 적용
      [root@localhost ~]# grub2-mkconfig -o /boot/grub2/grub.cfg
      [root@localhost ~]# clear

      # 방화벽 설정 설치
      [root@localhost ~]# dnf -y install firewall-config
      ```

    - gnome software 업데이트 끄기

      - 전체 활동 - 프로그램 표시 - 모두 - 소프트웨어 - 좌측 상단 소프트웨어 마우스 오른쪽 클릭 - <br/>
        자동 업데이트, 자동 업데이트 알림 모두 끔
      - 우측 상단 재부팅 - 다시 시작
      - 컴퓨터 끄기

    - 메모리 조절 (만약 RAM 4GB 일 경우, 8GB 이면 2GB로 유지하기)

      - 메모리 1.5G로 줄이기

        - Server - edit - 1536MB 수정 - OK

        - CD/DVD - use physical drive 체크

    - 스냅숏 저장

      - VMware Pro - open virtual machine - Server.vmx
      - VM - Snapshot - Snapshot manager - take snapshot - close
      - VM - Snapshot - Snapshot manager - Go to - Yes

#

## [CentOS8 리눅스 설치 - Server(B)]

- 텍스트 모드 (마우스 안먹힘)
- 영문 모드

### _설치_

- VMware Player - Server(B) - edit - CD/DVD - iso file 삽입 - Ok - Play (booting) - install - <br/>
  영문 - continue - time - seoul - done, network - on - done, software selection - minimal install - done - <br/>
  installation destination - 체크 - custom - done - swap 4G, 나머지 / 표준 partition - done - accept - <br/>
  begin - root 비번 설정, 사용자 비번 설정 - reboot

### _설정_

```centos8
root
<비번>

# 폰트 키우기
[root@localhost ~]# setfont sun12x22

# 아래 작업 네트워크 설정 이후에 하기 (네트워크 켜져 있어야 함)
[root@localhost ~]# dnf -y install bind-utils net-tools wget unzip bzip2
[root@localhost ~]# clear

# centos 버전 고정 작업
[root@localhost ~]# cd /etc/yum/repos.d
[root@localhost ~]# ls
[root@localhost ~]# rm -f *.repo
[root@localhost ~]# ls

[root@localhost ~]# wget http://download.hanbit.co.kr/centos/8/This.repo
[root@localhost ~]# ls
[root@localhost ~]# cat This.repo
```

- 네트워크 IP 설정 (매우 중요!)

```centos8
[root@localhost ~]# cd /etc/sysconfig/network-scripts/
[root@localhost ~]# ls
[root@localhost ~]# vi ifcfg-ens32

# BOOTPROTO="none"
# IPADDR=192.168.111.200
# NETMASK=255.255.255.0
# GATEWAY=192.168.111.2
# DNS1=192.168.111.2

[root@localhost ~]# nmcli connection down ens32
[root@localhost ~]# nmcli connection up ens32
[root@localhost ~]# reboot

root
<비번>

[root@localhost ~]# setfont sun12x22

[root@localhost ~]# ip addr

# ens32: inet 192.168.111.200 체크!

[root@localhost ~]# ping -c 3 www.google.com
[root@localhost ~]# clear
```

- selinux 끄기

```centos8
[root@localhost ~]# vi /etc/sysconfig/selinux

# SELINUX=disabled
```

- 해상도 설정 (800x600)

```centos8
[root@localhost ~]# vi /etc/grub.d/10_linux

# :set nu // 행 번호 표시
# 169 행
# ~ ~ ro ${args} vga=771"

[root@localhost ~]# grub2-mkconfig -o /boot/grub2/grub.cfg
[root@localhost ~]# reboot

root
<비번>

# 컴퓨터 끄기
[root@localhost ~]# halt -p
```

- 메모리 할당 및 스냅숏 설정

  - VMware Player - Server(B) - edit - 512MB, dvd - connect 체크 해제, iso 빼기

  - VMware Pro - open a virtual machine - Server(B).vmx - VM - Snapshot - Snapshot Manager <br/>
    Take Snapshot - "설정 완료" - close

#

## [CentOS8 리눅스 설치 - Client]

- PC용 리눅스 (xwindow 화면/gnome 환경)
- VMware Player - Client - edit - CD/DVD - conenct 체크, iso 삽입 - OK - booting - Install - Enter
- 한국어 - 계속 진행 - 시간; 서울, 네트워크; 켬, 소프트웨어 선택; 워크 스테이션, 설치 목적지; 디스크 두 번 클릭 후 오토매틱 (파티션 따로 할 필요 X, NVMe으로 둠) - 설치 시작 - root 암호, 사용자 centos 지정 - 재부팅 - 라이센스 동의 - 완료 - 목록에 없습니까 - root 로그인
- 한국어 - 다음 - 한글 선택 - 다음 - 건너뛰기 - centos 시작 - 도움말 X
- 전체 활동 - 터미널

```linux
# 자동 업데이트 끄기
[root@localhost ~]# gsettings set org.gnome.software download-updates false
[root@localhost ~]# systemctl disable dnf-makecache.service
[root@localhost ~]# systemctl disable dnf-makecache.timer

# Centos8 출시 시점의 dnf 명령어만 쓸 수 있도록 설정
[root@localhost ~]# cd /etc/yum/repos.d/
[root@localhost ~]# ls
[root@localhost ~]# rm -f *.repo
[root@localhost ~]# ls
[root@localhost ~]# wget http://download.hanbit.co.kr/centos/8/This.repo
[root@localhost ~]# ls
[root@localhost ~]# dnf clean all

# 해상도 (1024x768) 설정
[root@localhost ~]# gedit /etc/grub.d/10_linux

# 169행
# ~ ~ ro ${args} vga=773"

# 해상도 적용
[root@localhost ~]# grub2-mkconfig -o /boot/grub2/grub.cfg

# root 접속 못하도록, centos 사용자만 접속 가능하도록 설정
[root@localhost ~]# gedit /etc/pam.d/gdm-password

# 5행에 한줄 추가 후 저장
# auth required pam_succeed_if.so user != root quiet

[root@localhost ~]# reboot
```

```linux
# 목록에 없습니까? - root 로그인 <-- 접속 못함
# centos로 로그인 - 한국어 - 한글

# 우측 상단 - 설정 - 개인 정보; 화면 잠금, 알림 모두 끔, 전원; 빈 화면 안함, 지역 및 언어에서 한글만 남기고 나머지 모두 지움
# 우측 상단 - 설정 - 배경 변경
# 현재 활동 - 프로그램 표시 - 모두 - 소프트웨어 - 좌측 상단 소프트웨어 마우스 오른쪽 버튼 - 업데이트 기본 설정 - 모두 끔

# 현재 활동 - 터미널

# 자동 로그인 설정

# root 사용자로 변경
[cenots@localhost ~]$ su -

# gedit으로 해도 상관 없음
[root@localhost ~]# vi /etc/gdm/custom.conf

# a: append, 2줄 추가
# [daemon]
# AutomaticLoginEnable=True
# AutomaticLogin=centos

# :wq

# reboot

# 컴퓨터 끄기
```

- 메모리 조절 및 스냅숏 잡기

  - VMware Player - Client - edit - 메모리 1536MB, DVD 빼고 connect 체크 해제 - OK
  - VMware Pro - file - open virtual machine - client - VM - SnapShot - SnapShot manager - take snapshot - "설정 완료"

#

## [CentOS8 리눅스 설치 - WinClient]

- windows 접근 테스트용
- WinClient - edit - 메모리 2048 (빠른 설치 위함) - DVD - connect 체크, iso 삽입 - Ok - play
- 다음 - 지금 설치 - 동의 - 다음 - 사용자 지정 설치 - 다음 - (자동 재부팅)
- 지역 한국 - 예 - Microsfot 입력기 - 예 - 건너뛰기 - 이메일 아무렇게 입력 - 다음 - 로컬계정으로 Windows 설정 - ThisIsLinux - 다음 - 비밀번호 없이 - 다음 - 예 - 수락
- 좌측 상단 - Player - Install VMware tools (마우스 자연스럽게 나올 수 있음)
- 내 PC - DVD 드라이브 - setup - 예 - 기본값 - 다음 - 마침 - 재부팅
- 바탕화면 배경 변경
- 디스플레이 해상도 (1024x768) 체크
- 시스템 종료
- 메모리 조절; VMware Player - WinClient - edit - 메모리 1024, CD 체크 해제 및 iso 빼기
- 스냅숏 잡기; VMware Pro - File - open - VM - SnapShot - SnapShot Manager - Take SnapShot - "설정 완료"

#

## [Note]

- 커널 (자동차의 엔진)
- 리눅스 배포판 (자동차 여러 종류)
- RHEL은 무료버전이 없음
- 체크섬 프로그램; 다운로드 파일 정상 확인 (SSH 256만 확인해도 됨)
- xwindow; 설치에 대한 그래픽 지원
- 리눅스에서 이더넷(랜카드) 이름 - ens160
- root (리눅스 관리자, 소문자)
- gnome 환경 (xwindow 자체 환경)
- exit (터미널 창 닫기)
- 리눅스; 대소문자 완벽하게 구분함
- Shift + Spacebar: 한글 <-> 영문 변경
- dnf (설치)
- 항상 VMware Player 닫고 <-> VMware Pro 실행하기 (충돌 방지)
- 서버 컴퓨터는 root 계정으로 로그인
- rm -rf /boot <--- 아주 위험한 명령어 (부팅 관련 폴더 날림)
- 부팅 시 move it / copy it / cancel 뜨면 move it 클릭하기!
- xwindow (GUI) 모드는 Server 에 설정하고, Server(B) 는 텍스트 모드로 세팅
- 텍스트 모드는 한글 입출력이 잘 안되서 영문 모드로 설치 진행
- 텍스트 모드에서는 복사/붙여넣기가 안됨
- cat (파일 내용 출력)
- gedit은 xwindow 에서 열림, 텍스트 모드에서는 vi (편집기) 에디터 이용 <br/>
  a (insert), esc - :wq (write quit, 소문자로 입력)
- 텍스트 모드 사용시 시스템 사양 떨어져도 서버 성능 좋아짐 <br/>
  (xwindow 안쓰면 서버 자체에 집중 가능)
- passwd (비번 변경)
- 실습에서 사용하는 버전 (CentOS8 1905 버전)
- Client (centos 사용자 사용할 예정이지만 설정은 root 권한으로 진행해야 함)
- $ 들어가면 일반 사용자, # 들어가면 root 사용자
- su 명령어 입력하고 암호 입력하면 root 권한으로 명령어 실행 (su는 super user), exit 하면 다시 일반 사용자로 바뀜
- DHCP (Dynamic Host Configuration Protocol)
- [VMware Network Setting](https://cafe.naver.com/thisislinux/6974)

#

## [Reference]

[Reference1](https://www.youtube.com/watch?v=63Zt9Woif-4&list=PLVsNizTWUw7EJ9z-LW3lv3VC-6HI9I3hN&index=5)
[Reference2](https://www.youtube.com/watch?v=bLlbCq2dRgk&list=PLVsNizTWUw7EJ9z-LW3lv3VC-6HI9I3hN&index=6)
[Reference3](https://www.youtube.com/watch?v=rjwie8jgjJI&list=PLVsNizTWUw7EJ9z-LW3lv3VC-6HI9I3hN&index=7)
[Reference4](https://www.youtube.com/watch?v=yDd1-Ew88w0&list=PLVsNizTWUw7EJ9z-LW3lv3VC-6HI9I3hN&index=8)
[Reference5](https://www.youtube.com/watch?v=k6rSQ3QMmOU&list=PLVsNizTWUw7EJ9z-LW3lv3VC-6HI9I3hN&index=9)
