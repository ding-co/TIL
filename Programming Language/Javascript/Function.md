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
- 나머지 매개변수를 매개변수 앞에 쓸 수 없음 -> 명확 X
- 전개 연산자; 배열 복사, 객체 복사에 많이 쓰임

#

## [Reference]

[Reference1](https://www.youtube.com/watch?v=KYzqZXF0jIM&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=26)
[Reference2](https://www.youtube.com/watch?v=L_ge1GlThnU&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=27)
[Reference3](https://www.youtube.com/watch?v=TrRPLL2sOmQ&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=28)
