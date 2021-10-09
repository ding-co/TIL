## [리액트 맛보기]

### _리액트_

1.  리액트 기본 환경 설정
    - 리액트 코어
    - 리액트 DOM 처리 모듈
    - babel (transcompiler)
2.  ReactDOM.render()

    - babel 이용

      - JS 코드 내부에 HTML 코드 넣기 지원

3.  컴포넌트 만들기

    - 콘텐츠 넣기
    - 속성 넣기
    - 스타일 넣기

4.  컴포넌트 배열
    - 배열 활용해서 여러 개 요소 지정 후 한꺼번에 삽입 가능
5.  이벤트 연결
    - 캐멀 케이스 이용

```js
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel">
      const 콘텐츠 = '안녕하세요';
      const 속성 = 'http://placedog.net/400/200';
      const 스타일 = {
        backgroundColor: 'yellow',
      };
      const 배열 = [<li>사과</li>, <li>오렌지</li>, <li>바나나</li>];
      const 핸들러 = (event) => {
        alert('클릭했습니다!');
      };

      const 컴포넌트 = (
        <div onClick={핸들러}>
          <h1 style={스타일}>{콘텐츠}</h1>
          <img src={속성} />
          <ul>{배열}</ul>
        </div>
      );

      const 컨테이너 = document.querySelector('#root');

      ReactDOM.render(컴포넌트, 컨테이너);
    </script>
  </body>
</html>
```

### _클래스 컴포넌트_

- 클래스 컴포넌트 만들기
- props의 의미
  - properties 약자

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel">
      class App extends React.Component {
        constructor(props) {
          super(props); // this.props = props
          console.log(props);
        }
        render() {
          return (
            <h1>
              {this.props.속성A} - {this.props.속성B}
            </h1>
          );
        }
      }

      const 컴포넌트 = <App 속성A="값A" 속성B="값B" />;

      const 컨테이너 = document.querySelector('#root');

      ReactDOM.render(컴포넌트, 컨테이너);
    </script>
  </body>
</html>
```

- 타이머 만들기 예제
- 컴포넌트의 생애 주기 이벤트

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel">
      class Timer extends React.Component {
        constructor(props) {
          super(props);
          // 화면에 변화하는 값을 만들 때 this.state 객체 활용
          this.state = {
            현재_시간: new Date().toLocaleString(),
          };
        }

        render() {
          return <h1> {this.state.현재_시간} </h1>;
        }

        // 컴포넌트가 화면에 추가될 때 자동으로 호출되는 메서드
        componentDidMount() {
          // 화면에 변화하는 값을 지정하고 + 반영할 때 this.setState() 활용
          this.timerId = setInterval(() => {
            this.setState({
              현재_시간: new Date().toLocaleString(),
            });
          }, 1000);
        }

        // 컴포넌트가 화면에서 제거될 때 자동으로 호출되는 메서드
        componentWillUnmount() {
          clearInterval(this.timerId);
        }
      }

      class App extends React.Component {
        constructor(props) {
          super(props);
        }
        render() {
          return <Timer />;
        }
      }

      const 컴포넌트 = <App />;

      const 컨테이너 = document.querySelector('#root');

      ReactDOM.render(컴포넌트, 컨테이너);
    </script>
  </body>
</html>
```

- 이벤트 연결하기

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel">
      class App extends React.Component {
        constructor(props) {
          super(props);
          this.이벤트핸들러 = this.이벤트핸들러.bind(this);
          this.state = {
            숫자: 0,
          };
        }
        render() {
          return (
            <h1 onClick={this.이벤트핸들러}>{this.state.숫자}번 클릭합니다!</h1>
          );
        }
        이벤트핸들러(event) {
          this.setState({
            숫자: this.state.숫자 + 1,
          });
        }
      }

      const 컴포넌트 = <App />;

      const 컨테이너 = document.querySelector('#root');

      ReactDOM.render(컴포넌트, 컨테이너);
    </script>
  </body>
</html>
```

#

### [Note]

- 리액트 학습

  1. JS 기본
  2. FE 라이브러리 이것저것
  3. Node.js 기본
  4. BE 라이브러리 이것저것
  5. npm 활용 전역 모듈 <br/>
     이후에 살펴보는 내용

- 바벨의 기능

  - JS Extension (JS 확장 문법)
    - JSX
  - JSX -> JS 변환하여 웹 브라우저에서 사용 가능!
  - [reference](http://babeljs.io/repl)

- 컴포넌트 만들 때의 규칙

  - 닫는 태그 없는 경우 반드시 슬래시로 닫아야 함
  - 컴포넌트는 태그 하나만 가능
    - 여러 태그 사용하기 위해서는 div 태그로 감싸기
    - fragment 활용

- 문서 객체 모델 기본 조작

  - 태그 만들기
  - 콘텐츠 지정
  - 속성 지정
  - 스타일 지정

- 라이브러리; 복잡성을 숨겨둠

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=roNHl2PaptE)
[Reference2](https://www.youtube.com/watch?v=b0-tyXJTBnU)
