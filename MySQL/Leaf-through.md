## [DB 필수 용어]

### _요구사항 분석, 시스템 설계, 모델링_

- DB 설계도 작성 -> 코딩

### _DB 모델링과 필수 용어_

- DB 모델링; 현실 세계 -> MySQL에 어떻게 옮겨 놓을지 계획 <br/>
  ex) 사람의 이름, 주민번호 ,주소 등 정보 저장 (속성 추출)
- DBMS 관련 용어

  - DataBase Management System (MySQL)
  - DataBase
  - Data (정보 한건 한건) -> Table(표) 형태로 저장
  - 열 (Column/Field), 행 (Row/Tuple) - 2차원 구조 (RDBMS)
  - 행의 수 => 데이터의 수 (열의 수는 데이터 수와 관련 X, 열은 이름이 있음)
  - 열에는 데이터 형식이 있음 (데이터 형식 지정)
  - 기본 키 (Primary Key); 유일한 키 (중복 X) + Not Null
  - 테이블을 데이터베이스에 담음, DB는 테이블(데이터)의 저장소

#

## [데이터베이스 구축 절차 실습]

- MySQL Workbench GUI
- DB 구축 절차

  1. DB 생성

     - Create Schema

  2. 테이블 생성

     - Create Table

  3. 데이터 입력

  4. 데이터 조회/활용

     - `SELECT \* FROM memberTBL;`
     - `SELECT memberName, memberAddress FROM memberTBL;`
     - `SELECT \* FROM memberTBL WHERE memberName = '상달이';`

#

## [데이터베이스 개체 - 인덱스]

- 테이블이 제일 중요한 개체
- 테이블 외 개체 - 인덱스, 스토어드 프로시저, 트리거, 함수, 커서, ...
- 인덱스 (부록, 색인) - 책 뒤의 찾아보기와 같은 기능 <br/>
  => SELECT (조회) 할 때 매우 유용
- 인덱스 없으면 Full Table Scan
- ex) `CREATE INDEX idx_indexTBL_firstname ON indexTBL(first_name);`
- 인덱스가 있든 없든 찾는 결과는 동일 (실제 데이터 결과에는 영향 미치지 않음)
- execution plan 확인 => Lookup
- 빠른 조회에 활용

#

## [데이터베이스 개체 - 뷰, 저장 프로시저, 트리거]

### _뷰_

- 가상의 테이블 <br/>
  테이블처럼 보이지만 테이블이 아님
- 테이블에 링크된 개념 (like 바로가기)
- 보안 강화

```sql
CREATE VIEW uv_memberTBL

AS
    SELECT memberName, memberAddress FROM memberTBL;

SELECT * FROM uv_membertbl;
```

### _저장 프로시저_

- MySQL 제공 프로그램 기능
- 자주 쓰는 경우 저장 프로시저로 만들어서 호출

```sql
DELIMITER //
CREATE PROCEDURE myProc()
BEGIN
  SELECT * FROM memberTBL WHERE memberName = '당탕이';
  SELECT * FROM productTBL WHERE productName = '냉장고';
END //

# DELIMITER -> ; 로 변경
DELIMITER ;

CALL myProc() ;
```

### _트리거_

- 테이블에 부착되어 INSERT/DELETE/UPDATE 작업 발생되면 실행되는 코드
- 자동 작업 처리

```sql
SHOW databases;

USE shopdb;

INSERT INTO memberTBL VALUES ('Figure', '연아', '경기도 군포시 당정동');

SELECT * FROM memberTBL;

UPDATE memberTBL SET memberAddress = '서울 강남구 역삼동'
  WHERE memberName = '연아';

SELECT * FROM memberTBL;

DELETE FROM memberTBL WHERE memberName = '연아'

SELECT * FROM memberTBL;

CREATE TABLE deletedMemberTBL (
    memberID char(10),
    memberName char(5),
    memberAddress char(20),
    deletedDate date  -- 삭제한 날짜
);

DELIMITER //
CREATE TRIGGER trg_deletedMemberTBL -- 트리거 이름
    AFTER DELETE -- 삭제 후에 작동하게 지정
    ON memberTBL -- 트리거를 부착할 테이블
    FOR EACH ROW -- 각 행마다 적용시킴
BEGIN
    -- OLD 테이블의 내용을 백업 테이블에 삽입
    INSERT INTO deletedMemberTBL
        VALUES (OLD.memberID, OLD.memberName, OLD.memberAddress, CURDATE() );
END //
DELIMITER ;

SELECT * FROM memberTBL;

DELETE FROM memberTBL WHERE memberName = '당탕이';

SELECT * FROM memberTBL;

SELECT * FROM deletedMemberTBL;
```

#

## [백업과 복원]

- 백업: 현재 DB를 다른 매체에 보관
- 복원: 원상태로 돌려놓는 작업
- DBA에게 매우 중요!

```sql
USE shopDB;

SELECT * FROM productTBL;

# 백업 이후
DELETE FROM productTBL;
SELECT * FROM productTBL;

# 복원 전 다른 DB 선택
USE sys;

# 복원 확인
USE shopDB;
SELECT * FROM productTBL;
```

- Administration - Data Export - shopdb 체크 - export self contained file 체크 - 경로 설정 (~/ShopDB.sql) <br/>
  create dump 체크, create schema 체크 - Start Export
- 복원 위해서 우선 다른 DB 선택 - Administration - Data Import/Restore - self contained 체크 - 경로 설정 <br/>
  default target schema로 shopdb 체크 - start import

#

## [MySQL과 응용프로그램 연동]

- python, php 연동 (후반부 예정)
- Visual Studio 2017 설치 (DB - Visual Studio 연동)
  - ASP .Net 체크 - 설치 - 설치 후 시작 체크 해제 - X
- Visual Studio 2017 실행
  - 로그인은 나중에 하기 (30일)
- MySQL 과 Visual Studio 연결해주는 Connector 설치
- ODBC 설정 (32비트)
  - 제어판 - 관리도구 - ODCB data sources 32bit - 시스템 DSN - 추가 - MySQL Unicode driver 선택 - 마침 - MyODBC (서버 이름), 127.0.0.1 (TCP/IP, 자기 자신 - MySQL 설치되어 있는 곳), root (User), Password, shobdb 선택 - test - 확인
- Visual Studio 실행

  - 파일 - 새로 만들기 - 프로젝트 - Visual C# - 웹 - 이전 버전 - ASP .NET 빈 웹 사이트 - 확인
  - 우측 솔루션 탐색기 - 웹 사이트 마우스 오른쪽 버튼 - 추가 - Web Form - 확인
  - 좌측 하단 디자인 - 왼쪽 도구 상자 - 고정 - 데이터 - SqlDataSource 클릭해서 마우스로 드래그 앤 드롭 - 데이터 소스 구성 - 새 연결 - Microsoft ODBC - 계속 - 사용자 소스 MyODBC 선택 - root/비번 - 연결 테스트 - 확인 - 확인 - 다음 - 다음 - 사용자 지정 sql - 다음 - `SELECT \* FROM memberTBL - 다음 - 쿼리 테스트 - 마침
  - 좌측 ListView 드래그 앤 드롭 - 데이터 소스 - sqlDatasource1 선택 - ListView 구성 - 전문가, 페이징 사용 - 확인 - 파일 - 모두 저장
  - 파일 - 브라우저에서 보기

#

## [Note]

- hwp; 한글 워드 프로세서
- 테이블 (자료구조)
- not null; 비어 있으면 안됨
- 테이블은 DBMS 안에 존재하는 것이 아니라 DB 안에 존재하는 것임
- DBMS가 이해하는 언어 => SQL (Structured Query Language, 구조화된 질의어)
- SQL; DBMS, 사람이 소통하는 언어
- Schema = DB
- 열 이름은 영어로 지정
- 대문자; 예약어 <br/>
  소문자; 사용자 정의어 (사실 대소문자 구분 X)
- 번개; 쿼리 모두 실행, 마우스 드래그 해서 번개 클릭
- `CREATE TABLE myTable(id int);` // refresh all
- 데이터는 언제든지 날라갈 수 있음 => 백업 관리 매우 중요!
- 회원가입; insert 개념, 응용 프로그램과 연동 필요
- MySQL Workbench 단축키 <br/>
  Ctrl + Enter: 쿼리 한 줄 실행 <br/>
  Ctrl + Shift + Enter: 쿼리 여러 줄 실행
- 뷰; 아르바이트생이 실제 회원 테이블에는 접근 불가 <br/>
  회원 테이블에서 필요한 열만 뽑아서 가상의 테이블인 뷰를 만들고, <br/>
  아르바이트생이 이 뷰에만 접근 가능 (보안 허용된 뷰)
- 트리거; 학생 정보 관리 테이블; 어떤 학생 자퇴 후 <br/>
  학생 테이블에서 데이터를 삭제하고 자퇴생 정보를 자퇴생 테이블로 자동으로 옮기고 <br/>
  나중에 자퇴 관련 데이터 요구 시 주면 됨
- 실무; Enterprise backup tool 있음
- ODBC; Open DataBase Connectivity
- MySQL ODBC Connector 최신 버전 따로 설치 (MySQL 8버전 32 비트)

#

## [Reference]

[Reference1](https://www.youtube.com/watch?v=VnnTh83sjcc&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=6)
[Reference2](https://www.youtube.com/watch?v=0bjKxoP03XI&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=7)
[Reference3](https://www.youtube.com/watch?v=kjQEV5j-iIk&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=8)
[Reference4](https://www.youtube.com/watch?v=V5GN2FMBl4w&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=9)
[Reference5](https://www.youtube.com/watch?v=FQQOiygNdvE&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=10)
[Reference6](https://www.youtube.com/watch?v=bpEF-6YTfb4&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=11)
