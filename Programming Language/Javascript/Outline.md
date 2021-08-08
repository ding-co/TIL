## [책 소개 + 강의 소개]

- 모던 웹을 위한 자바스크립트 & 제이쿼리 개정판
- JS 로드맵의 줄기 탄탄히 하기
- 디테일 줄이고 범위 조금 넓힘
- 약 70강 완강 예상 (계획 변경)

#

## [개발 환경 설치]

- 텍스트 에디터; 프로그램 코드를 입력 <br/>
  => VS Code

- 코드 실행기; 작성한 코드 실행 <br/>
  => Google Chrome (웹 브라우저)

#

## [코드 실행 방법]

- 코드 실행 방법 2가지

  1. 개발자 도구의 콘솔 사용 (interactive shell)
     - 간단 테스트 용도
     - REPL (Read Evaluate Print Loop)
  2. 파일 만들어서 코드 실행 (VS Code 이용)
     - 기본적 방법

- alert() 경고 창
- about:blank 빈 페이지 (기존 웹 페이지 코드와 충돌 X)
- 콘솔 위치 변경 (우측 상단 Dock side icon 클릭)

#

## [오류 확인 방법]

### _오류 확인 방법_

1. 콘솔에서 오류 확인하기

   - 코드 잘못 입력 시 바로 오류 출력

2. 파일 실행 때 오류 확인하기

   - 오류 확인은 개발자 도구 - 콘솔 탭으로 확인

### _초기 자주 발생하는 오류_

- ReferenceError: 단어 오탈자 발생
- SyntaxError: 일반적으로 기호에서 오탈자 발생

#

## [VS Code 관련 추가적인 내용]

- 색 테마 변경 => extension 설치
- 들여쓰기
- 자바스크립트 표준 스타일 (코딩 스타일/컨벤션)
- tab size 2
- 멀티 커서 기능 <br/>
  1. Alt + 마우스 클릭
  2. Ctrl + Alt + 방향키(위/아래)
- 코딩 전용 폰트 - Monospace (고정 폭 글꼴) <br/>
  ex) Consolas font (한국어 지원 X), D2Coding (한글 지원) <br/>
  파일 - 기본 설정 - 설정 - Font Family 에서 폰트 설정

#

## [기본 용어]

### _표현식_

- Expression
- 값을 만들어내는 코드
- 의미가 있는 표현식
- 값의 관점에서 보는 것

### _문장_

- Statement
- 코드를 실행하는 단위
- 문장 종결 기호로 줄바꿈과 세미콜론 쓸 수 있음 <br/>
  (표준 스타일에서는 세미콜론 안 쓰도록 권장)
- 실행의 관점에서 보는 것

=> 표현식이면서 문장 가능 (두 가지 속성 모두 취할 수 있음)

### _키워드_

- 프로그래밍 창시자가 정한 단어

### _식별자_

- 값의 이름 붙이기
- [식별자 규칙]
  - 키워드 사용 X
  - 숫자로 시작 X
  - 특수 문자는 \_와 $만 허용
  - 공백 문자 포함 X
- [식별자 이름 관례]
  - Camel case
- [식별자 이름 관례 종류]
  1. 대문자로 시작하면 클래스 ex) Array, Number, Component, ...
  2. 모든 것이 대문자 => 상수 ex) ARRAY, NUMBER, PI, ...
  3. 소문자로 시작 (4가지)
     - 식별자 뒤에 괄호 있음 / 단독 사용 가능 => 함수
     - 식별자 뒤에 괄호 있음 / 단독 사용 불가 => 메서드
     - 식별자 뒤에 괄호 없음 / 단독 사용 가능 => 변수
     - 식별자 뒤에 괄호 없음 / 단독 사용 불가 => 속성

#

## [주석과 출력]

- HTML 파일과 결합해서 사용하는 방식
- 자바스크립트 단독으로 사용하는 방식

### _주석_

- 프로그램 코드를 사람에게 설명하기 위한 목적
- 코드 실행기가 무시함 (코드 실행에 영향 주지 X)

- HTML 코드 주석
- 자바스크립트 주석

```html
<head>
  <!-- 주석 내용 -->
  <script>
    // 한 줄 주석
    /*
    여러 줄 주석
     */
  </script>
</head>
```

### _출력_

- alert() // 경고창 출력 (함수)
- console.log() // 콘솔에 출력 (메서드)

#

### [Note]

- JS: 학습 범위가 매우 넓음
- JS는 표준이 있는 언어라서 다른 웹 브라우저에서도 동작함
- Visual Studio !== Visual Studio Code
- VS Code extension; 한국어 언어 팩
- 스크립트 계열 프로그래밍 언어 (파이썬, 루비, 자바스크립트, ...)
- about:blank 페이지 (빈 페이지) - Ctrl + Shift + I (개발자 도구) - Console 탭
- VS Code - html 파일 형식으로 새 파일 작성 및 저장 - html:5 <br/>
  head 태그 안에 script 태그 생성 (자동 완성 기능) - 코드 입력 <br/>
  반드시 저장 후 크롭에 드래그 앤 드롭으로 탭 띄우기
- REPL (읽고 + 실행(평가)하고 + 출력하는 것의 + 반복)
- Tab 키를 눌렀을 때 띄어쓰기로 변환해주는 기능 => Soft Tab
- tab / Shift + tab
- 표현식 하나를 나타내는 문장 => 표현식 문장, 식문 (expression statement)
- console.log('hi') <br/>
  console이 log 한다. 'hi' 를 <br/>
  (주어 + 동사 + 목적어)
- 동사 + 목적어 => 명령문 <br/>
  ex) alert('hi') <br/>
  alert 해라 'hi'를

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=pXuyfvJPENA&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=1)
[Reference2](https://www.youtube.com/watch?v=pwR0y76Od_U&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=2)
[Reference3](https://www.youtube.com/watch?v=TA8waU1lJd8&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=3)
[Reference4](https://www.youtube.com/watch?v=V6fA-6UO2sA&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=4)
[Reference5](https://www.youtube.com/watch?v=2qqJUx_S33M&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=5)
[Reference6](https://www.youtube.com/watch?v=PU_QuhU1Vfs&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=6)
[Reference7](https://www.youtube.com/watch?v=kvvKsAiSFXM&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=7)
