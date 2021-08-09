## [MySQL 시작하기 전에]

- MySQL 8.0 version
- 목표: DB 초보자 -> DB 중급자 (MySQL)
- 64 bit
- [카페](https://cafe.naver.com/thisisMySQL)

#

## [DBMS 개요와 MySQL 소개]

### _DBMS 개요_

- 데이터베이스: DB, 데이터의 집합 <br/>
  <u>여러 명의 사용자가 동시에 접근 가능</u>
- DBMS: DB 운영 S/W (DataBase Management System/Software) <br/>
  MySQL/MariaDB, PostgreSQL, Oracle, SQL Server, SQLite, ...
  - 데이터의 무결성 (데이터 결함/오류 X)
  - 데이터의 독립성 (데이터와 응용 프로그램은 독립적)
  - 보안 (사용자 계정 관리)
  - 데이터 중복의 최소화
  - 응용 프로그램 제작 및 수정이 쉬워짐 (유지보수)
  - 데이터의 안전성 향상 (백업, 복원 기능)
- 오프라인 관리 -> 파일 시스템 (ex. 메모장) 사용 -> DBMS (대량 데이터)
- DBMS 분류
  - 계층형 DBMS (트리 구조)
  - 망형 DBMS (수평 + 수직 연결) // 현재 거의 사용 X
  - 관계형 DBMS (RDBMS) - 최소 단위: 테이블 (표)
- RDBMS
- RDBMS 운영 언어 => SQL
- SQL
  - 다른 시스템으로 이식성이 좋다
  - 표준이 계속 발전 (SQL2019)
  - 대화식 언어
  - 분산형 클라이언트/서버 구조

### _MySQL 소개_

- MySQL; DBMS S/W, Oracle사 제작 (외부 합병)
- 상업용 -> 상용 라이센스 필요
- MySQL 8.0 version, 관계형 DBMS
- Edition - 무료 (Community) / 상용 (Enterprise, 회사)

#

## [MySQL 8.0 설치]

- Windows 10 x64 (64 bit 필수)
- MySQL Server, MySQL Client, MySQL Workbench, Sample Database
- 기본 사양 확인: 시작 - 마우스 오른쪽 - 시스템
- Setup Type: Custom - MySQL Server, MySQL Workbench, Sample Database
- 고가용성 - Standard / Config Type: 개발용 컴퓨터
- MySQL port: 3306
- Root 비밀번호 설정 / 기억하기
- 윈도우 서비스 이름: MySQL
- DB 서버 접속
- Edit - Preferences - SQL Editor - Safe Update 체크 해제 (귀찮아짐)
- C:\Program Files\MySQL\MySQL Server 8.0\bin 을 Path에 추가 <br/>
  (명령 프롬프트로 작업하기 위해)
- 시작 - 마우스 오른쪽 - powershell 관리자 - cmd 명령어

```cmd
SETX PATH "C:\Program Files\MySQL\MySQL Server 8.0\bin;%PATH%"
```

#

## [샘플 데이터베이스 생성]

- 대용량 샘플 데이터베이스 설치 <br/>
  C:\employees
- 명령 프롬프트 cmd

```cmd
cd \employees
mysql -u root -p    // mysql을 root user로 접속

source employees.sql;

show databases;   // employees 확인
exit
```

- Linux 환경에서 MySQL 설치하기 (부록 참조)

#

## [Note]

- 관계형 DBMS (Relational DBMS)
- 엑셀 시트; table (표) 구조
- row (행), column (열) / field
- 표준 SQL, <br/>
  Oracle (PL/SQL) / SQL Server (T-SQL) / MySQL (SQL)
- MySQL Workbench; MySQL 통합 개발 환경 (MySQL Client)
- Local (내 PC)

#

## [Reference]

[Reference0](https://www.youtube.com/watch?v=xKYeJxBTt2E&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=1)
[Reference1](https://www.youtube.com/watch?v=z0uuNBhWfQg&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=2)
[Reference2](https://www.youtube.com/watch?v=NuolcziNaI0&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=3)
[Reference3](https://www.youtube.com/watch?v=AcoNC00U_a8&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=4)
[Reference4](https://www.youtube.com/watch?v=ySKbcqTC_Sk&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=5)
