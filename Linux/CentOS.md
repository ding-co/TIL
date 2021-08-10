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

    - 한국어 - 시간 및 날짜 - 서울 선택, 네트워크 - 이더넷 켬, 소프트웨어 선택 - 워크 스테이션,
    - 설치 목적지 - custom 체크
    - 파티션 2개로 분할
      - 표준 파티션, +, swap, 4G (임시 메모리 공간)
      - / 파티션 (root 파티션)
    - root 비번 설정 - 완료 2번
    - 일반 사용자 설정 - 완료 2번
    - 재부팅
    - 라이센스 약관 동의 - 완료 - 설정 완료
    - 목록에 없습니까 - root - 로그인
    - 한국어 - 한국어 (한글) - 건너뛰기 - CentOS 시작 - x
    - 화면 사이즈; 우측 상단 설정 아이콘 - 장치 - 디스플레이 - 해상도 (1024x768) 적용 - 유지
    - 개인 정보 - 화면 잠금 - 자동 화면 잠금 끔, 알림 표시 끔
    - 전원 - 빈 화면 안함
    - 자동 업데이트 끄기; 현재 활동 - 터미널

      ```centos8
        [root@localhost ~]# gsettings set org.gnome.software download-updates false
        [root@localhost ~]# systemctl disable dnf-makecache.service
        [root@localhost ~]# systemctl disable dnf-makecache.timer
      ```

    - CentOS8 업데이트 자동 설치 해제;

      - 현재 활동 - 터미널
      - [This.repo 내용](https://cafe.naver.com/thisislinux/6620)

      ```centos8
      [root@localhost ~]# cd /etc/yum.repos.d/
      [root@localhost ~]# mkdir backup
      [root@localhost ~]# ls
      [root@localhost ~]# mv *.repo backup/
      [root@localhost ~]# ls
      [root@localhost ~]# gedit This.repo

      # 내용 복사 및 붙여넣기 - 저장 - X

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

## [Note]

- 커널 (자동차의 엔진)
- 리눅스 배포판 (자동차 여러 종류)
- RHEL은 무료버전이 없음
- 체크섬 프로그램; 다운로드 파일 정상 확인 (SSH 256만 확인)
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

#

## [Reference]

[Reference1](https://www.youtube.com/watch?v=63Zt9Woif-4&list=PLVsNizTWUw7EJ9z-LW3lv3VC-6HI9I3hN&index=5)
[Reference2](https://www.youtube.com/watch?v=bLlbCq2dRgk&list=PLVsNizTWUw7EJ9z-LW3lv3VC-6HI9I3hN&index=6)
