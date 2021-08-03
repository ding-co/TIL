## [localStorage 객체]

<br/>

### _localStorage 객체 기본_

- 지역적으로 사용할 수 있는 데이터 저장소 (간단한 용도)

<br/>

> localStorage 객체의 메서드

- localStorage.getItem('키')
- localStorage.setItem('키', '값')
- localStorage.removeItem('키')
- localStorage.clear() // 전체 제거

```html
<head>
  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const p = document.querySelector('p');
      const clearBtn = document.querySelector('button');
      const input = document.querySelector('input');
      const select = document.querySelector('select');

      const value = localStorage.getItem('키');
      const color = localStorage.getItem('color');

      if (value !== null) {
        p.textContent = `이전 실행했을 때의 값: ${value}`;
        input.value = value;
      }

      if (color !== null) {
        document.body.style.backgroundColor = color;
        select.value = color;
      } else {
        document.body.style.backgroundColor = 'black';
      }

      clearBtn.addEventListener('click', () => {
        localStorage.clear();
      });

      input.addEventListener('keyup', () => {
        localStorage.setItem('키', input.value);
      });

      select.addEventListener('change', () => {
        const color = select.options[select.options.selectedIndex].value;
        localStorage.setItem('color', color);
        document.body.style.backgroundColor = color;
      });
    });
  </script>
</head>
<body>
  <p></p>
  <button>지우기</button>
  <input type="text" />
  <select name="" id="">
    <option value="black">검정색</option>
    <option value="green">초록색</option>
    <option value="red">빨강색</option>
  </select>
</body>
```

#

### _localStorage 객체: 키 하나로 저장하기_

- 데이터가 많아지는 경우, 키 하나에 여러 데이터 함께 넣음 <br/>
  ex) 저장 형식: "색상","메시지" (키 하나에) <br/>
  활용 형식: {color: "색상", message: "메시지"}

<br/>

> 데이터 형식 정하기

```html
<script>
  const load = () => {
    const data = localStorage.getItem('애플리케이션');
    if (data !== null) {
      const [color, message] = data.split(',');
      return {
        color: color,
        message: message,
      };
    } else {
      return {
        color: 'red',
        message: '',
      };
    }
  };

  const save = (data) => {
    localStorage.setItem('애플리케이션', `${data.color},${data.message}`);
  };
</script>
```

#

### _localStorage 객체: JSON 객체와 결합해서 사용_

<br/>

> JSON 형식 기초

- JavaScript Object Notation

  - JS에서 객체 표현하는 형식으로 데이터를 저장(표현) 하는 형식

<br/>

- 규정 <br/>
  1. 키는 문자열만! <br/>
  2. 문자열은 반드시 큰따옴표! <br/>
     cf) 데이터는 문자열, 숫자, 불만 저장 가능 <br/>
     컨테이너 데이터는 객체, 배열만 사용 가능 <br/>
     (함수를 저장하거나 할 수는 X)

<br/>

> JSON 객체 (자바스크립트 라이브러리)

- JSON.stringify(): 자바스크립트 객체 -> JSON 문자열
- JSON.parse(): JSON 문자열 -> 자바스크립트 객체

```html
<script>
  const load = () => {
    const data = localStorage.getItem('애플리케이션');
    if (data !== null) {
      return JSON.parse(data);
    } else {
      return {
        color: 'red',
        message: '',
      };
    }
  };

  const save = (data) => {
    localStorage.setItem('애플리케이션', JSON.stringify(data));
  };
</script>
```

#

### [Note]

- 개발자 도구 - 애플리케이션 탭 - LocalStorage
- localStorage 값 가져오지 못하면 return null

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=uXURy9veEQA&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=51)
[Reference2](https://www.youtube.com/watch?v=w-3v65zj3EM&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=52)
[Reference3](https://www.youtube.com/watch?v=Id7o7DwhiFY&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=53)
