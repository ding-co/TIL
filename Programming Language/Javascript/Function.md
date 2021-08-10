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
-

#

## [Reference]

[Reference1](https://www.youtube.com/watch?v=KYzqZXF0jIM&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=26)
[Reference2](https://www.youtube.com/watch?v=L_ge1GlThnU&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=27)
[Reference3](https://www.youtube.com/watch?v=TrRPLL2sOmQ&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=28)
[Reference4](https://www.youtube.com/watch?v=dbI1bkWnoE4&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=29)
[Referecne5](https://www.youtube.com/watch?v=znOCf5pj9R4&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=30)
