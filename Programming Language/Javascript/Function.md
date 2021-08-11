## [함수 기본]

### _함수_

1. 프로시저적 관점

```html
<script>
  // 프로시저 형태의 함수 (매개변수 갖지 않는 함수)
  const f = function () {
    // 점프! (함수 호출 위치 -> 함수 본문으로 이동)
    console.log('hi', x);
    // 함수 끝 -> 원래 위치로 돌아감 (리턴; 함수 본문 -> 함수 호출 위치)
  };

  const x = 10;
  f();
</script>
```

2. 수학적 관점

```html
<script>
  const f = function (x) {
    // 점프!
    return x + 5; // 리턴 '값'
  };

  console.log(f(3));
</script>
```

#

## [함수 기본 예제]

### _익명 함수_

- 현대에 많이 사용

```html
<script>
  // 익명 함수
  const f = function (매개변수1, 매개변수2) {
    return 리턴값;
  };
</script>
```

### _선언적 함수_

- 초기에 많이 사용

```html
<script>
  // 선언적 함수
  function f(매개변수1, 매개변수2) {
    return 리턴값;
  }
</script>
```

### _기본 예제_

```html
<script>
  // 최솟값 구하는 함수
  const min = function (배열) {
    let output = 배열[0];

    for (const value of 배열) {
      if (output > value) {
        output = value;
      }
    }

    return output;
  };

  console.log(min([52, 412, 51, 61, 124, 1]));
</script>
```

#

## [나머지 매개변수와 전개 연산자 (함수 호출)]

### _API_

- Application Programming Interface (약속)
- 애플리케이션 프로그램을 만들 때의 약속 <br/>
  ex) 파일 형식, 함수, ...
-

### _나머지 매개변수 (rest parameter)_

- 함수를 만들 때 사용
- 자료형은 무조건 배열

```html
<script>
  const 함수 = function (a, b, ...매개변수) {
    console.log(a, b, 매개변수);
  };

  함수(); // undefined undefined [] (빈 배열)
  함수(1); // 1 undefined []
  함수(1, 2, 3); // 1 2 [3]
</script>
```

### _전개 연산자: 함수 호출_

- 함수 호출 시 사용
- ...배열

```html
<script>
  const 함수 = function (a, b, c) {
    console.log(a, b, c);
  };

  const a = [1, 2, 3];
  함수(a[0], a[1], a[2]);
  함수(...a);
</script>
```

#

## [기본 매개변수와 가독성]

### _기본 매개변수_

- 가독성 + 코드의 안전성 위한 기능 (선입견 대응)
- 현대의 기본 매개변수

```html
<script>
  const isLeapYear = function (연도 = 기본값) {};
</script>
```

- 과거의 기본 매개변수

```html
<script>
  const isLeapYear = function (연도) {
    // 첫번째 방법
    if (typeof 연도 === 'undefined') {
      연도 = new Date().getFullYear();
    }

    // 두번쨰 방법
    연도 = typeof 연도 === 'undefined' ? new Date().getFullYear() : 연도;
    연도 = typeof 연도 !== 'undefined' ? 연도 : new Date().getFullYear();

    // 세번째 방법
    연도 = 연도 || new Date().getFullYear();
  };
</script>
```

### _가독성_

- 성능적 관점; 프로그램이 더 적은 CPU (메모리 자원) 사용 - 과거
- 가독성 관점; 코드를 쉽게 읽고 이해, 안전하게 쓸 수 있는 속성 - 현대 <br/>
  (기업 입장의 비용 절감, <br/>
  프로그램의 복잡성 증가 => 단위 테스트 중요해짐, <br/>
  지원 도구의 활용)

#

## [5.1절 확인문제]

- [구버전] 나머지 매개변수

```html
<script>
  const max = function () {
    // 함수 내부 - arguments (나머지 매개변수)
    // forin/forof 반복문 사용 불가, for문만 사용 가능
    let output = arguments[0];
  };
</script>
```

- [구버전] 전개 연산자

```html
<script>
  const input = [1, 2, 3, 4];
  console.log(max(...input)); // max(1, 2, 3, 4) // 최신 JS

  console.log(max.apply(null, input));
</script>
```

#

## [콜백함수]

- 함수의 매개변수로 함수 전달하기
- 매개변수로 전달되는 함수 => 콜백함수

```html
<script>
  const 테스트 = function (콜백함수) {
    콜백함수();
  };

  const 함수 = function () {
    console.log('hi');
  };

  테스트(함수);
</script>
```

### _콜백함수 매개변수로 숫자 하나를 받는 형태_

```html
<script>
  const 테스트 = function (배열, 콜백함수) {
    for (const 값 of 배열) {
      콜백함수(값);
    }
  };

  const 함수 = function (콜백함수의_매개변수) {
    console.log(`${콜백함수의_매개변수}번째 안녕하세요`);
  };

  테스트([52, 273, 103], 함수);
</script>
```

### _함수를 곧바로 전달하기_

```html
<script>
  const 테스트 = function (배열, 콜백함수) {
    for (const 값 of 배열) {
      콜백함수(값);
    }
  };

  테스트([52, 273, 103], function (콜백함수의_매개변수) {
    console.log(`${콜백함수의_매개변수}번째 안녕하세요`);
  };);
</script>
```

### _배열의 콜백함수를 사용하는 메서드_

- forEach 메서드

  - 배열의 요소를 콜백함수로 전달해서 순회

```html
<script>
  const 배열 = [273, 52, 103, 32, 57];
  배열.forEach(function (value, index) {
    console.log(`${index}번째의 값은 ${value}`);
  });
</script>
```

- filter 메서드

  - 콜백함수로 true/false return 하는 함수가 올 것으로 예상
  - 최종적으로 filtering 한 배열 return
  - 비파괴척 처리 => return 값을 변수에 넣기

```html
<script>
  let 배열 = [273, 52, 103, 32, 57];

  배열 = 배열.filter(function (value, index) {
    return value % 2 === 0;
  });

  console.log(배열);
</script>
```

- map 메서드

  - 기존의 배열 요소를 기반으로 새로운 배열 만들어서 return

```html
<script>
  let 배열 = [273, 52, 103, 32, 57];

  배열 = 배열.filter(function (value, index) {
    return value + '!!';
  });

  console.log(배열);
</script>
```

- 화살표 함수

  - (매개변수) => {본문}
  - {} 내부에 있는 코드가 return 코드 한 개 <br/>
    -> 중괄호와 return 키워드 생략 가능
  - 간단한 함수 작성 시 많이 활용

```html
<script>
  let 배열 = [273, 52, 103, 32, 57];

  배열 = 배열.filter(function (value, index) {
    return value % 2 === 0;
  });

  배열 = 배열.filter((value, index) => {
    return value % 2 === 0;
  });

  배열 = 배열.filter((value, index) => value % 2 === 0);

  console.log(배열);
</script>
```

#

## [타이머 함수, 즉시 호출 함수 (IIFE), 엄격 모드]

### _타이머 함수_

- JS에서 콜백함수 사용하는 대표적 함수
- handler가 콜백함수임
- 시계 만들 때, 움직인 구현 등에 활용

```html
<script>
  setTimeout(); // 특정한 시간 후에 한 번 작업 수행
  setInterval(); // 특정한 시간마다 작업 수행

  // 1000 밀리 초 = 1초
  const a = setTimeout(function () {
    console.log('setTimeout 함수 입니다!');
  }, 1000);

  const b = setInterval(function () {
    console.log('setInterval 함수 입니다!');
  }, 1000);

  console.log(a, b); // 1 2

  // 타이머 제거 함수
  // 타이머 취소 작업이 먼저 일어남 (콜백함수 내부는 실행 X)
  clearTimeout(a);
  clearInterval(b);
</script>
```

### _즉시 호출 함수 (IIFE)_

- 함수를 만들고 즉시 호출하는 함수
- 한 웹사이트 안에 JS 코드 많이 들어감 <br/>
  => 여러 script 태그 안에서 함수 이름 등의 중복 발생 시 오류 발생 가능 <br/>
  => 충돌 방지 위한 코드로 즉시 호출 함수 활용 (상수, 변수 등 함수 내부에서만 작동)

```html
<script>
  //   (function () {

  //   })()

  //   (() => {

  //   })()
</script>

<script>
  (function () {
    const a = 10;
    console.log(a);
  })();
</script>

<script>
  (function () {
    const a = 20;
    console.log(a);
  })();
</script>
```

### _엄격 모드_

- strict mode
- JS 유연성 막기 (안전 장치)
- 'use strict' 문자열
- 다른 사람이 만든 코드까지 엄격 모드 제한하면 문제 발생 가능 <br/>
  => 즉시 호출 함수 안 'use strict' (즉시 호출 함수 내부에서만 엄격 모드 작동)

```html
<script>
  (function () {
    'use strict';
  })();
</script>

<script>
  'use strict';

  a = 10;
  b = 20;

  alert(a, b);
</script>
```

#

## [선언적 함수와 익명 함수의 차이]

### _선언적 함수 vs. 익명 함수_

- 선언적 함수

  - 선언적 함수는 전체 코드를 읽기 전에 선언한 순서대로 만들어짐 <br/>
    (위에서 아래로 차례대로 읽으면서 실행되지 X)

```html
<script>
  함수();

  function 함수() {
    console.log('A 함수입니다.');
  }

  function 함수() {
    console.log('B 함수입니다.');
  }

  function 함수() {
    console.log('C 함수입니다.');
  }

  // C 함수입니다.
</script>
```

- 익명 함수

  - 익명 함수는 무조건 위에서 아래로 읽어지면서 만들어짐
  - 코드 하나씩 실행하면서 만들어짐

```html
<script>
  let 함수 = function () {
    console.log('A 함수입니다.');
  };

  함수 = function () {
    console.log('B 함수입니다.');
  };

  함수 = function () {
    console.log('C 함수입니다.');
  };

  함수();

  // C 함수입니다.
</script>
```

- 익명 함수와 선언적 함수 동시 사용 시 문제 발생 가능

```html
<script>
  함수();

  // 나중에 실행됨
  함수 = function () {
    console.log('익명 함수입니다.');
  };

  // 먼저 만들어짐
  function 함수() {
    console.log('선언적 함수입니다.');
  }

  함수();

  // 선언적 함수입니다.
  // 익명 함수입니다.
</script>
```

#

## [Note]

- 함수(): 함수를 호출한다 => 함수의 본문 실행
- 순수 함수와 비순수 함수
- 왜 프로시저가 함수로 발전?
- 스코프의 개념
- 프로시저 형태의 함수: 매개변수 갖지 않는 함수
- 함수 괄호 안에 오는 것 => 매개변수
- 함수를 사용하는 이유: 코드의 재사용 => 추상화
- 매개변수와 리턴값을 쓰는 이유: 코드 깔끔 + 활용도 높음
- API 설계자 / API 사용자 (분야가 다른 것임, 멋짐 X) <br/>
  잘하는 사람이 멋진 것일 뿐...
- 나머지 매개변수 자료형 => 무조건 배열 나옴
- 나머지 매개변수를 일반 매개변수 앞에 쓸 수 없음 -> 명확 X
- 전개 연산자; 배열 복사, 객체 복사에 많이 쓰임
- 단위 테스트; 코드를 작성하고 빠르게 문제가 있는지 없는지 테스트 해주는 과정 자동화 한 것
- 과거 코드 짧게 작성하는 코드 골프 대회 있었음 (코드 최대한 짧게 작성하는 대회)
- 국내 프로그래밍 언어; 아희
- 클린 코드, 클린 아키텍쳐, 이펙티브 시리즈 등 가독성 관련 책
- new Date().getFullYear() // 올해 연도 구하기
- 함수의 헤더; 함수의 이름, 매개변수
- JS; 함수의 매개변수로 어떤 것이든지 모두 전달 가능 <br/>
  JS에서는 함수도 하나의 값이므로 매개값으로 전달 가능
- 자바스크립트의 콜백함수는 필요한 매개변수만 받아서 사용할 수 있음
- const는 재할당 안됨
- setTimeout은 clearTimeout으로 끔 <br/>
  setInterval은 clearInterval로 끔
- setTimeout, setInterval 함수에서 0 밀리초로 셋팅 시 <br/>
  => 타이머 무조건 꺼짐 (JS의 단일 쓰레드 특성)
- IIFE (Immediately Invoked Function Expression)
- JS는 네임 스페이스라는 문법이 따로 없어서 이름 충돌 쉽게 발생 가능한 언어 <br/>
  => 객체로 네임 스페이스 유사적으로 만들어 활용 <br/>
  => 따라서 선언적 함수 잘 사용 안함
- HTML 코드 내부의 script 태그는 하나씩 전체가 실행됨 (각각 실행됨) <br/>
  => 선언적 함수 사용하면 JS 코드 실행 흐름 예측하기 힘들어짐
- this 키워드
- for 반복문에서 사용할 수 있는 break 키워드를 forEach() 메서드에서는 구현 안됨 <br/>
  => break 필요 시 for 반복문 사용

#

## [Reference]

[Reference1](https://www.youtube.com/watch?v=KYzqZXF0jIM&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=26)
[Reference2](https://www.youtube.com/watch?v=L_ge1GlThnU&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=27)
[Reference3](https://www.youtube.com/watch?v=TrRPLL2sOmQ&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=28)
[Reference4](https://www.youtube.com/watch?v=dbI1bkWnoE4&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=29)
[Referecne5](https://www.youtube.com/watch?v=znOCf5pj9R4&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=30)
[Reference6](https://www.youtube.com/watch?v=Q5E5sENGPWI&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=31)
[Reference7](https://www.youtube.com/watch?v=tjGg1G_DyKQ&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=32)
[Reference8](https://www.youtube.com/watch?v=ANqKWpNjC70&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=33)
