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

     - SELECT \* FROM memberTBL;
     - SELECT memberName, memberAddress FROM memberTBL;
     - SELECT \* FROM memberTBL WHERE memberName = '상달이';

#

## [데이터베이스 개체 - 인덱스]

- 테이블이 제일 중요한 개체
- 테이블 외 개체 - 인덱스, 스토어드 프로시저, 트리거, 함수, 커서, ...
- 인덱스 (부록, 색인) - 책 뒤의 찾아보기와 같은 기능 <br/>
  => SELECT (조회) 할 때 매우 유용
- 인덱스 없으면 Full Table Scan
- ex) CREATE INDEX idx_indexTBL_firstname ON indexTBL(first_name);
- 인덱스가 있든 없든 찾는 결과는 동일 (실제 데이터 결과에는 영향 미치지 않음)
- execution plan 확인 => Lookup
- 빠른 조회에 활용

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
- CREATE TABLE myTable(id int); // refresh all
- 데이터는 언제든지 날라갈 수 있음 => 백업 관리 매우 중요!
- 회원가입; insert 개념, 응용 프로그램과 연동 필요
- MySQL Workbench 단축키 <br/>
  Ctrl + Enter: 쿼리 한 줄 실행 <br/>
  Ctrl + Shift + Enter: 쿼리 여러 줄 실행

#

## [Reference]

[Reference1](https://www.youtube.com/watch?v=VnnTh83sjcc&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=6)
[Reference2](https://www.youtube.com/watch?v=0bjKxoP03XI&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=7)
[Reference3](https://www.youtube.com/watch?v=kjQEV5j-iIk&list=PLVsNizTWUw7Hox7NMhenT-bulldCp9HP9&index=8)
