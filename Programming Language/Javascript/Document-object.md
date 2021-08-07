## [라이브 서버와 DOMContentLoaded 이벤트]

### _문서 객체 모델_

- DOM (Document Object Model)
- DOMContentLoaded 이벤트
  - 문서 객체 모두 만들어진 이후 script 태그 내용 실행
  - script 태그는 최대한 head 태그 안에 넣도록 권장
  - document.addEventListener('DOMContentLoaded', () => {})

#

## [document.querySelector()/querySelectorAll() 메소드]

> 문서 객체 가져오기 <br/>
> 선택자; 태그, 아이디, 클래스, 속성, 후손 (like css selector)

### _document.querySelector()_

- 여러 요소 있더라도 첫 요소 하나만 추출
- document.querySelector('h1')
- document.querySelector('#id')
- document.querySelector('.class') <br/>
  동시에 2개 이상 클래스 지정 위해 .으로 연결 (띄어쓰기는 다른 의미) <br/>
  ex) document,querySelector('.class1.class2')
- document.querySelector('[type=text]')
- document.querySelector('body input')

### _document.querySelectorAll()_

- 여러 요소를 배열에 담아 추출 <br/>
  => for of 구문 이용하여 각 요소 활용 가능

#

## [문서 객체 조작하기]

<br/>

### _문서 객체 글자 조작하기_

- textContent
- innerHTML (내부 문자열에 HTML 태그 활용 가능)

<br/>

### _문서 객체 속성 조작하기_

- setAttribute(속성 이름, 값)
- getAttribute(속성 이름)
- 표준에 있는 속성 -> 그냥 입력

<br/>

### _문서 객체 스타일 조작하기_

- style.backgroundColor
- style['background-color']
- style['backgroundColor']

<br/>

#

## [문서 객체 생성, 제거, 이동]

<br/>

### _문서 객체 생성하기_

- createElement(태그 이름)
- appendChild()

<br/>

### _문서 객체 제거하기_

- parentNode.removeChild()

<br/>

### _문서 객체 이동하기_

- appendChild()

#

## [문서 객체 이벤트 기본]

<br/>

### _이벤트 연결_

- addEventListener(이벤트 이름, 이벤트 리스너)
- 이벤트 리스너(핸들러): 이벤트 발생 시 호출되는 콜백 함수

<br/>

### _이벤트 연결 해제_

- removeEventListener(이벤트 이름, 이벤트 리스너)
- 이벤트 리스너는 따로 변수로 설정해줘야 함

#

## [이벤트 활용]

<br/>

### _키보드 이벤트_

- keydown
- keyup
- keypress; 아시아계 문자에 잘 작동하지 않는 경우 있음

<br/>

### _이벤트 객체_

- 콜백함수의 첫 번째 매개변수로 이벤트 객체 가져옴
- 이벤트.code

<br/>

### _이벤트 발생 객체_

- 이벤트 발생 객체가 이벤트 핸들러 안에서 활용될 수 있음 (이름으로 활용 가능)
- **event.currentTarget**; 이벤트를 발생시킨 객체
- 익명 함수 사용 시, this 키워드 활용

<br/>

### _기본 이벤트 막기_

- event.preventDefault()
- contextmenu 이벤트에 많이 활용

#

### [Note]

- VS Code extension; live server
- 문서 객체: HTML 요소 <br/>
  문서 객체 모델: HTML 요소를 조작하는 객체들의 집합
- HTML 코드들은 위에서 아래로 차례대로 실행됨
- innerHTML 속성: 문자열
- hr 태그: 구분선
- 태그 안에 텍스트 넣기; textContent 속성 사용
- css; userSelect = 'none'; 클릭 시 텍스트 선택 x
- 웹 브라우저가 문서 객체를 모두 읽어들였을 때 실행되는 이벤트: DOMContentLoaded
- 속성 선택자; [속성=값]
- textarea 태그
- 선언적 함수; function f() {}
- 익명함수; const f = function () {}
- 화살표 함수; () => {} <br/>

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=-oVDoTAy_P0&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=40)
[Reference2](https://www.youtube.com/watch?v=L9QkNhMDcOg&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=41)
[Reference3](https://www.youtube.com/watch?v=a43xV0ajVgM&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=42)
[Reference4](https://www.youtube.com/watch?v=k9ZXWAh2Hj0&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=43)
[Reference5](https://www.youtube.com/watch?v=ByKGf9h9Qy0&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=44)
[Reference6](https://www.youtube.com/watch?v=HQIM5PES29Q&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=45)
