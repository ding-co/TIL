## [문서 객체 조작하기]

[Reference](https://www.youtube.com/watch?v=a43xV0ajVgM&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=42)

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

[Reference](https://www.youtube.com/watch?v=k9ZXWAh2Hj0&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=43)

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

[Reference](https://www.youtube.com/watch?v=ByKGf9h9Qy0&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=44)

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

[Reference](https://www.youtube.com/watch?v=HQIM5PES29Q&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=45)

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

### [참고]

- hr 태그: 구분선
- 태그 안에 텍스트 넣기; textContent 속성 사용
- css; userSelect = 'none'; 클릭 시 텍스트 선택 x
- 웹 브라우저가 문서 객체를 모두 읽어들였을 때 실행되는 이벤트: DOMContentLoaded
- 속성 선택자; [속성=값]
- textarea 태그
- 선언적 함수; function f() {}
- 익명함수; const f = function () {}
- 화살표 함수; () => {} <br/>
