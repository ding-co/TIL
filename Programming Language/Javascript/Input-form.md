## [입력 양식: 버튼]

<br/>

### _버튼_

<br/>

> 클릭 이벤트

- button
- input type="button" <br/>
  (cf. input:button)

<br/>

> submit 이벤트

- form => input type="submit" <br/>
  (cf. input:submit)
- form 태그에 이벤트 연결 (input 태그로 연결 X)
- form 태그 안에 button 태그 있으면 input submit 과 동일하게 작동 <br/>
  => form 태그 안에 input type으로 button 지정 (submit 이벤트 발생 X)

#

## [입력 양식: 글자 입력]

<br/>

### _글자 입력_

<br/>

> input type="text" (한 줄 입력) <br/>
> textarea 태그 (여러 줄 입력) <br/>

- value 속성으로 값 추출
- change event, keydown/keyup/keypress event
- key event 발생 순서: keydown -> keypress -> 입력 양식에 값 들어감 -> keyup
- change event: 해당 input 태그 전체에 값 입력 마쳤을 때

<br/>

> p 태그에 contenteditable="true" 속성과 값 지정 (글자 직접 수정 가능) <br/>

#

## [입력 양식: 선택 상자]

<br/>

### _선택 상자_

<br/>

> 단일 선택 상자

```html
<head>
  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const select = document.querySelector('select');
      const p = document.querySelector('p');
      select.addEventListener('change', (event) => {
        const options = event.currentTarget.options;
        const index = options.selectedIndex;
        p.textContent = `선택: ${options[index].textContent}`;
      });
    });
  </script>
</head>

<body>
  <select>
    <option>떡볶이</option>
    <option>순대</option>
    <option>오뎅</option>
    <option>튀김</option>
  </select>
  <p>선택: 떡볶이</p>
</body>
```

> 다중 선택 상자

```html
<head>
  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const select = document.querySelector('select');
      const p = document.querySelector('p');
      select.addEventListener('change', (event) => {
        const options = event.currentTarget.options;
        const list = [];
        for (const option of options) {
          if (option.selected) {
            list.push(option.textContent);
          }
        }
        p.textContent = `선택: ${list.join(',')}`;
      });
    });
  </script>
</head>

<body>
  <select multiple>
    <option>떡볶이</option>
    <option>순대</option>
    <option>오뎅</option>
    <option>튀김</option>
  </select>
  <p>선택:</p>
  <p></p>
</body>
```

> Exercise 1. cm 길이 단위 변환

```html
<head>
  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const input = document.querySelector('input');
      const span = document.querySelector('span');
      const select = document.querySelector('select');

      const handler = () => {
        const value = Number(input.value);
        const selected = select.options[select.options.selectedIndex];
        span.textContent = value * Number(selected.value);
      };

      input.addEventListener('keyup', handler);
      select.addEventListener('change', handler);
    });
  </script>
</head>

<body>
  <input type="text" value="0" /> cm =
  <span>0</span>
  <select>
    <option value="10">mm</option>
    <option value="0.01">m</option>
    <option value="0.393701">inch</option>
  </select>
</body>
```

#

## [입력 양식: 체크박스와 라디오버튼]

> change 이벤트 <br/>
> checked 속성

<br/>

### _체크박스_

- input type="checkbox"
- 어떤 대상의 true 또는 false 속성 표현 <br/>
  ex) 회원 약관 체크
- 단독으로도 사용 가능

<br/>

### _라디오버튼_

- input type="radio"
- 여러 대상 중에서 하나를 선택 <br/>
  ex) 성별 선택
- 여러 개를 그룹으로 매핑 <br/>
  name 속성으로 같은 그룹 이름 매핑

<br/>

> Exercise 1. 체크박스와 라디오버튼

```html
<head>
  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const checkbox = document.querySelector('input[type=checkbox]');
      const checkboxResult = document.querySelector('h1#checkbox');
      checkbox.addEventListener('change', () => {
        if (checkbox.checked) {
          checkboxResult.textContent = '체크';
        } else {
          checkboxResult.textContent = '해제';
        }
      });

      const radios = document.querySelectorAll(
        'input[type=radio][name=gender]'
      );
      const radioResult = document.querySelector('h1#radioButton');
      radios.forEach((radio) => {
        radio.addEventListener('change', (event) => {
          radioResult.textContent = event.currentTarget.value;
        });
      });
    });
  </script>
</head>

<body>
  <input type="checkbox" /><br />
  <h1 id="checkbox"></h1>

  <input type="radio" name="gender" value="여성" />여성<br />
  <input type="radio" name="gender" value="남성" />남성<br />
  <input type="radio" name="gender" value="직접 지정" />직접 지정<br />
  <h1 id="radioButton"></h1>
</body>
```

> Exercise 2. 체크박스 - 타이머, 배경 색상

```html
<head>
  <script>
    document.addEventListener('DOMContentLoaded', () => {
      let [seconds, timerId] = [0, 0];
      const checkbox = document.querySelector('input[type=checkbox]');
      const checkboxResult = document.querySelector('h1#checkbox');
      checkbox.addEventListener('change', () => {
        if (checkbox.checked) {
          document.body.style.backgroundColor = 'red';
          timerId = setInterval(() => {
            seconds += 1;
            checkboxResult.textContent = `${seconds}초`;
          }, 1000);
        } else {
          document.body.style.backgroundColor = 'white';
          clearInterval(timerId);
        }
      });
    });
  </script>
</head>

<body>
  <input type="checkbox" />타이머 활성화
  <h1 id="checkbox">0초</h1>
</body>
```

#

## [기본 할 일 목록]

<br/>

### _To do list_

```html
<head>
  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const addToDo = () => {
        if (input.value !== '') {
          const div = document.createElement('div');
          document.body.appendChild(div);

          const checkbox = document.createElement('input');
          checkbox.type = 'checkbox';
          checkbox.addEventListener('change', () => {
            if (checkbox.checked) {
              span.style.textDecoration = 'line-through';
            } else {
              span.style.textDecoration = '';
            }
          });
          div.appendChild(checkbox);

          const span = document.createElement('span');
          span.textContent = input.value;
          input.value = '';
          div.appendChild(span);

          const deleteBtn = document.createElement('button');
          deleteBtn.textContent = '제거하기';
          deleteBtn.addEventListener('click', () => {
            div.parentNode.removeChild(div);
          });
          div.appendChild(deleteBtn);
        }
      };

      const h1 = document.createElement('h1');
      h1.textContent = 'To do list';
      document.body.appendChild(h1);

      const input = document.createElement('input');
      input.addEventListener('keyup', (event) => {
        if (event.keyCode === 13) {
          addToDo();
        }
      });
      document.body.appendChild(input);

      const addBtn = document.createElement('button');
      addBtn.textContent = '추가하기';
      addBtn.addEventListener('click', () => {
        addToDo();
      });
      document.body.appendChild(addBtn);
    });
  </script>
</head>
```

#

### [Note]

- input type을 JS에서 가져올 시, document.querySelector('input[type=button]') 형식
- 선택 상자 (드롭 다운 박스)
- br 태그: HTML 줄 바꿈 태그
- \`${}\`: 템플릿 문자열
- [a, b] = [0, 0]: 다중 할당 연산

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=n2EBSjdIAzo&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=46)
[Reference2](https://www.youtube.com/watch?v=xXeDA06E0EA&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=47)
[Reference3](https://www.youtube.com/watch?v=TsvqQsQrgms&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=48)
[Reference4](https://www.youtube.com/watch?v=wCf_TS-J2AA&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=49)
[Reference5](https://www.youtube.com/watch?v=7wD-5T5Xv2M&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=50)
