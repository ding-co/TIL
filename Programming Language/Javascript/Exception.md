## [구문 오류와 예외]

### _구문 오류_

- 프로그램 실행 전에 발생하는 오류
- SyntaxError <br/>
  ex) 괄호 짝, 문자열 열고 닫기, ...

<br/>

### _예외 (런타임 오류)_

- 프로그램 실행 중에 발생하는 오류 <br/>
  (오류 발생 하지 않은 부분은 정상 실행)
- Exception <br/>
  ex) 식별자 이름 잘못 적기, 네트워크 통신 오류로 데이터 받지 못함, ...

#

## [예외 처리]

### _예외 처리_

- 기본 예외 처리; if-else 조건문 이용 (예외 발생 예상 가능)
- 고급 예외 처리; try-catch-finally 이용 (대부분 예외 예상 불가능)
  - try; 예외 발생 가능성 있는 코드
  - catch (예외객체); 예외 발생했을 때 실행할 코드
    - 예외객체.name와 예외객체.message (브라우저마다 보유 속성 다름)
  - finally; 무조건적으로 실행하는 코드

#

### [Note]

- 자바스크립트: 동적 언어; 구문오류 제외한 모든 오류 => 예외
- null (없음)
- 예외 처리 안하면 이후의 코드 실행 안됨 <br/>
  예외 처리 하면 이후의 코드 정상 실행
- 예외 객체; 예외와 관련된 정보 담고 있는 객체
- JS는 매우 유연한 언어라 문법적으로 예외 발생 경우 매우 적음

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=h6uMV3iuGHE&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=54)
[Reference2](https://www.youtube.com/watch?v=v4F15l_1Zws&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=55)
