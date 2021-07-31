# Linux

## python, telnet, putty, git 설치

<br>

### _Python_

- apt-get update
- apt-get install python3
- apt-get install python3-pip -y
- cd /usr/bin => mv python3 python
- apt-get install ntp
- cp python python3
- pip3 install requests

### _Putty_

- apt-get install xinetd telentd
- vi /etc/xinetd.d/telnet
- :set paste
- /etc/init.d/xinetd restart
- apt-get install telnet
- apt-get install sudo
- docker start ub2
- docker exec -it ub2 bash
- docker commit ub2 ub_telnet
- docker images
- docker run -itd --name ubt -p 23:23 ub_telnet bash
- cd /usr/bin => vi start_telnet.sh => #!/bin/sh /etc/init.d/xinetd restart
- chmod +x start_telnet.sh
- telnet localhost 23

### _Git (in Putty)_

- apt-get install git
- git config --list
- git config --global user.name [github-username]
- git config --global user.email [github-email]
- git config credential.helper store

#

## 도커에서 리눅스 컨테이너 구동 팁

#

## Shell Script & Cron

<br>

### _Shell Script_

<br>

### _Cron (for backup)_

#

## [Note]

#

## [Reference]

[Reference1](https://www.youtube.com/watch?v=LQauC9s_8z4&list=PLEOnZ6GeucBVj0V5JFQx_6XBbZrrynzMh&index=7)
[Referenc2](https://www.youtube.com/watch?v=9qGVr4W4raY&list=PLEOnZ6GeucBVj0V5JFQx_6XBbZrrynzMh&index=8)
[Reference3](https://www.youtube.com/watch?v=035pZp2R50M&list=PLEOnZ6GeucBVj0V5JFQx_6XBbZrrynzMh&index=9)
