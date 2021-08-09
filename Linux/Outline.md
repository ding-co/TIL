## [Linux를 시작하기 전에]

- CentOS 8 version
- 목표: 리눅스 초보자 -> 리눅스 중급자
- 리눅스 서버 & 네트워크 구축
- 전반적인 리눅스 정리
- [실습 가능 컴퓨터 확인](https://www.grc.com/securable.htm)
- [카페](https://cafe.naver.com/thisisLinux)

#

## [가상머신 개념과 VMware 설치]

### _가상머신 개념_

- 가상머신; 가상의 컴퓨터 (동시 작동 가능)
- 1대의 PC에서 4대의 가상머신 설치 예정 (리눅스 3대, Windows 1대)
- 가상 머신 소프트웨어; 가상 머신 운영 SW (ex. VM ware)
- 호스트 OS: PC 자체에 이미 설치되어 있는 OS <br/>
  게스트 OS: 가상 컴퓨터에 설치되어 있는 OS
- 멀티 부팅 개념과 다름 (멀티 부팅: 컴퓨터 1대에서 한번에 하나씩만 부팅됨)
- VM ware (전산실), 라우터 (게이트웨이, 외부로 통하는 네트워크 장비), <br/>
  여러 대의 책상, 각 책상마다 네트워크 랜선 연결, <br/>
  서버 컴퓨터를 책상에 올려놓음 그리고 OS 설치
- VMware Workstation Pro (유료) <br/>
  VMware Workstation Player (개인 무료)
- VMware Workstation Pro 설치 (player 도 자동으로 설치됨)
- 64 bit 필수, RAM 8GB 권장, SSD 권장

### _실습 환경 구축_

- VMware Pro 최신 버전 설치 (Pro 는 30일 평가판)

#

## [가상머신 4대 설치]

### _가상머신 겉모양_

- 가상머신 (가짜 컴퓨터)

### _가상머신 4대 생성_

- 가상머신 저장 폴더 <br/>
  C:\CentOS8, Server, Server(B), Client, WinClient
- OS 는 나중에 설치

1. Server [CentOS8]

   - CentOS8 64-bit
   - Edit Virtual Machine settings (서버 컴퓨터 뚜껑 열기)
   - RAM 2GB, HDD SCSI[스카시] 80GB / Single file
   - USB, Sound, Printer 모두 remove

2. Server(B) [Red Hat Enterprise Linux 8 64-bit]

   - Red Hat Enterprise Linux 8 64-bit
   - HDD 40GB / Single file
   - edit => HDD SCSI 40GB
   - USB, Sound, Printer 모두 remove

3. Client [Red Hat Enterprise Linux 8 64-bit]

   - Red Hat Enterprise Linux 8 64-bit
   - HDD 40GB

4. WinClient (32-bit)

   - Windows 10
   - 60GB / Single
   - Customize Hardware => USB, Sound, Printer 모두 remove

#

## [VMware 특징 및 네트워크 설정]

### _VMware 특징_

- 가상머신 장점
- 1대의 컴퓨터 -> 실무 환경 거의 비슷한 네트워크 컴퓨터 환경 구성
- 운영체제의 특정 시점 저장하는 스냅숏 기능 (1~3초 소요)
- 내 마음대로 하드디스크 등 H/W 장착 및 테스트 가능
- suspend 기능 (노트북 뚜껑 닫기)

### _네트워크 설정_

- 네트워크 정보 파악과 변경 <br/>
  호스트 OS에서 IP 정보 확인: Powershell <br/>
  ipconfig /all 에서 VMnet8에서 IPv4 확인!
- 192.168.111.1 로 세팅하기 <br/>
  VMware Pro - Edit - virtual network editor - VMnet8 change setting 에서 Subnet IP 수정 <br/>
  (30일 지나도 이 기능은 사용 가능)
- .1 이 숫자는 hostOS 번호 (게이트웨이가 호스트OS에게 추가적으로 할당한 것)
- 게이트웨이 (겸 DNS 서버)는 .2로 고정
- DHCP 서버; .254, 다른 컴퓨터에게 자동으로 ip 할당해주는 서버 컴퓨터
- Server [.100], Server(B) [.200], Client [자동 IP], WinClient [자동 IP] 할당 예정

#

## [Note]

- 실습 환경; VM ware (가상머신 프로그램)
- VMware Workstation pro; 가상 네트워크 사용자 설정, 스냅숏 기능
- 윈도우 + tab; 여러 프로세스 한번에 확인 가능
- Processor (Cpu)
- vmdk (virtual machine disk)
- NAT
- lck (잠금)
- 가상 머신은 독립적 서버 컴퓨터
- 포커스 이동 (마우스) <br/>
  Ctrl + Alt: 게스트 OS 포커스 빠져 나오기
- Ctrl + Alt + Enter: 전체화면
- Suspended (정상 종료 X, 부품 변경 불가) => 다시 부팅
- 2대 이상 부팅 위해서는 player 다시 실행
- 윈도우 + R: 실행창
- 호스트 OS (진짜 컴퓨터)

#

## [Reference]

[Reference0](https://www.youtube.com/watch?v=ovrU9K3jfJs&list=PLVsNizTWUw7EJ9z-LW3lv3VC-6HI9I3hN&index=1)
[Reference1](https://www.youtube.com/watch?v=HeHO4JyGuVo&list=PLVsNizTWUw7EJ9z-LW3lv3VC-6HI9I3hN&index=2)
[Reference2](https://www.youtube.com/watch?v=64oghFmlwzU&list=PLVsNizTWUw7EJ9z-LW3lv3VC-6HI9I3hN&index=3)
[Reference3](https://www.youtube.com/watch?v=UPAJU1EzMyk&list=PLVsNizTWUw7EJ9z-LW3lv3VC-6HI9I3hN&index=4)
