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

### [Note]

- 개발자 도구 - 애플리케이션 탭 - LocalStorage
- localStorage 값 가져오지 못하면 return null

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=uXURy9veEQA&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=51)
