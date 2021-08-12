## [forof forin for 반복문]

> `forof`, `forin` 반복문 - 배열 등과 함께 사용 <br/>

> `for` 반복문 - 범용적으로 사용

### _`forof` 반복문_

```js
const 배열 = ['바나나', '사과', '귤'];

// const 뒤에는 새로 만드는 요소라 이름을 아무렇게 지정해도 됨
// 요소; 반복 변수 (반복문 내부에서 사용하는 변수)
for (const 요소 of 배열) {
  console.log(요소);
}
```

### _`forin` 반복문_

```js
const 배열 = ['바나나', '사과', '귤'];

// 1. 배열 요소 개수만큼 반복 일어남
// 2. 각각 반복에서 반복 변수에 인덱스가 하나씩 들어감
for (const 인덱스 in 배열) {
  console.log(인덱스, 배열[인덱스]);
}
```

### _`for` 반복문_

```js
// 특정 횟수만큼 반복
// 반복 변수 - i, j, k, ...
for (let i = 0; i < 20; i++) {
  console.log(`${i}번째 반복입니다.`);
}

// 역 반복문
for (let i = 20; i >= 10; i--) {
  console.log(`${i}번째 반복입니다.`);
}
```

- 반복 변수 - const vs. let
- for 반복문에서는 무조건 let 사용!

```js
# 반복 변수 i는 한번 선언되고 활용하여 값을 변경하면서 인덱스 추적
# => let으로 선언해야함

for (let i = 0; i < 배열.length; i++) {
  const 인덱스 = i;
  const 요소 = 배열[i];
}

# for 반복문 본문에서는 반복문 내부가 끝나면 완전히 사라지고 새로 만들어지므로
# => const 사용 가능
```

- forof, forin 반복문에서는 반복 변수를 const로 선언해도 됨!

#

## [while 반복문]

### _`while` 반복문_

```js
// 1. 불 표현식 확인
// 2-a. true라면 -> 본문을 실행하고 1번으로 돌아감
// 2-b. false라면 -> 종료
while (불_표현식) {
  본문;
}

// while 반복문: 무한 반복
let i = 0;
while (true) {
  alert(`${i}번째 반복입니다.`);
  i++;
}

let i = 0;
while (confirm('계속 진행하시겠습니까?')) {
  alert(`${i}번째 반복입니다.`);
  i++;
}

// for 반복문과 while 반복문 비교
// for 반복문 - 특정 횟수 반복 또는 배열 기반 반복에 많이 사용
// while 반복문 - 조건 중요할 때 사용
// 조건의 예; 결과가 나올 때까지, 특정 시간이 될 때까지,
//           파일을 읽으며 특정 단어를 찾을 때까지 등...
```

### _`break` 키워드_

- switch 조건문이나 반복문 벗어날 때 사용하는 키워드

```js
let i = 0;
while (i < 10) {
  i++;
  console.log(`${i}번째 반복입니다.`);
  break;
}
```

### _`continue` 키워드_

- 반복문 안의 반복 작업 멈추고 다음 반복 작업으로 돌아가는 키워드

```js
let i = 0;
while (i < 10) {
  i++;
  console.log(`${i}번째 반복입니다.`);
  continue;
  console.log('현재 반복이 끝났습니다.');
}
```

#

## [4장 마무리 + 피라미드 예제]

#

### [Note]

- 조건문/반복문 구문 형태는 고정된 구문이므로 다 외우기!
- 보조 기능의 지원 (코드 조각, Enter/tab)
- 코드 조각 사용; 최소한의 조작 -> 최대한의 행동 <br/>
  (pair programming 시 유용, 폼나고 속도감 good)
- tab/shift + tab (한꺼번에 지정), esc/tab (마무리)
- 반복문 헤더와 본문 <br/>
  반복문 헤더: {} 이전 내용 <br/>
  반복문 본문: {} 안 내용
- 비파괴적으로 동작하기 위해서는 원본, 새로운 생성본 모두 메모리에 존재해야함!
- 배열 대부분 비파괴적 처리
- 스택 해제, 스코프
- 사소한 것이 모이면 실력을 고이게 만든다
- continue 구문; early continue 테크닉
- early return
- JS; 파일 처리 위해서 Node.js 알아야 함

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=w5bpDsquwKc&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=23)
[Reference2](https://www.youtube.com/watch?v=I-1zobW0Efo&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=24)
[Reference3](https://www.youtube.com/watch?v=sN9vXNkV3JE&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=25)
