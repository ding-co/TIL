## [조건문 기본]

### _if 조건문_

```js
// if 본문 내용에 문장이 하나이면 중괄호 생략 가능
if (불_표현식) {
  문장;
  문장;
}
```

### _날짜와 시간 구하기_

- Date 객체 이용

```js
// 날짜 구하기 (사전에 범위 항상 확인!)
const date = new Date();

// 올해
date.getFullYear();

// 월 (0 ~ 11)
date.getMonth();

// 일 (1 ~ 31)
date.getDate();

// 시간 (0 ~ 23)
date.getHours();
```

#

## [3.1절 마무리]

### _if else 조건문_

- 완전히 상반된 조건 (서로 배타적) => else로 조건 비교 횟수 줄이기

```js
// 불 표현식 한 번만 비교
if (불_표현식) {
  // 불 표현식이 true일 때 실행하는 문장
} else {
  // 불 표현식이 false일 때 실행하는 문장
}
```

### _if - else if - else_

- 배타적 조건 존재 => else if, else로 조건 비교 횟수 줄이기

```js
// 사용자에게 숫자를 입력받아 음수, 0, 양수 구분하는 코드
const a = Number(prompt('숫자를 입력해주세요.', ''));

if (a < 0) {
  console.log('음수입니다.');
} else if (a === 0) {
  console.log('0입니다.');
} else {
  console.log('양수입니다.');
}
```

#

## [나머지 조건문]

### _switch 조건문_

- break 키워드를 사용하지 않으면 조건을 잡은 case 절 아래 모든 문장 실행됨

```js
// 자료 <- 비교가 일어나는 대상
switch (자료) {
  case 조건A:
    break;
  case 조건B:
    break;
  default:
    [break];
}
```

### _조건부 연산자_

- 삼항 연산자 (전체가 하나의 결과를 내는 연산)

```js
// 불_표현식 ? 참일_때의_결과 : 거짓일_때의_결과

const x = Number(prompt('숫자를 입력해주세요.', ''));

alert(x > 0 ? '0보다 큰 숫자입니다.' : '0이하의 숫자입니다.');
```

### _짧은 조건문_

- 논리 연산자 사용한 조건문
- short circuit evaluation (단락/단축 평가)
- 현대에는 많이 사용하지는 않음 (과거 코드 읽기 위해서는 알아야 함)

```js
alert('시작');
true || alert('또는 연산자');

false && alert('그리고 연산자');
alert('종료');

// 시작
// 종료
```

```js
alert('시작');
true || alert('또는 연산자');
false || alert('또는 연산자');

false && alert('그리고 연산자');
true && alert('그리고 연산자');
alert('종료');

// 시작
// 또는 연산자
// 그리고 연산자
// 종료
```

#

## [3장 누적 예제 (이론과 실전)]

### _짝수와 홀수 구분하기: 이론 공부의 중요성_

```js
// 첫번째 방법 (현실적인 방법)
// 홀수: 끝자리 => 1, 3, 5, 7, 9
// 짝수: 끝자리 => 2, 4, 6, 8, 0

const 입력 = prompt('정수를 입력해주세요.', '');

// 인덱스가 0부터 시작하므로 마지막 인덱스는 입력.length - 1
const 끝자리 = Number(입력[입력.length - 1]);

if (
  끝자리 === 1 ||
  끝자리 === 3 ||
  끝자리 === 5 ||
  끝자리 === 7 ||
  끝자리 === 9
) {
  alert('입력한 숫자는 홀수입니다.');
} else {
  alert('입력한 숫자는 짝수입니다.');
}
```

```js
// 참고
// 끝자리 === 1 || 3 || 5 || 7 || 9 와 같이 코드 작성 불가
// 이유: || (또는) 연산자는 이항 연산자 이므로 양쪽 피연산자를 무조건적으로 bool로만 받을 수 있음
// 따라서 처음에 저 3은 true로 변환됨 => 문제 발생

// 그러므로 프로그래밍에서는 각각의 위치가 다음과 같아야 함
// 끝자리 === 1 ||
// 끝자리 === 3 ||
// 끝자리 === 5 ||
// 끝자리 === 7 ||
// 끝자리 === 9
```

```js
// 두번째 방법 (이론 필요, 프로그래밍적 발상법)
// 코드 짧고 숫자 연산이므로 속도 빠름

const 입력 = Number(prompt('정수를 입력해주세요.', ''));

if (입력 % 2 === 1) {
  alert('입력한 숫자는 홀수입니다.');
} else {
  alert('입력한 숫자는 짝수입니다.');
}
```

### _태어난 연도를 입력받아 띠 출력하기: 실전의 중요성_

```js
const 입력 = Number(prompt('태어난 해를 입력해주세요.', '')) % 12;
const tti = '원숭이,닭,개,돼지,쥐,소,호랑이,토끼,용,뱀,말,양'.split(',');
alert(`${tti[입력]}입니다.`);

// 감동...
```

#

## [3.2절 확인 문제]

```js
// 삼항 연산자 예제
const result =
  100 > 200 ? prompt('값을 입력해주세요', '') : confirm('버튼을 클릭해주세요');

alert(result);
```

#

### [Note]

- 제어문 (Control statement) <br/>
  코드의 실행 흐름과 직접적인 관련이 있는 문장
- 조건문: 조건에 따라서 어떤 문장을 실행할지 결정해주는 문장
- 코드 조각 잘 활용하자!
- prompt(), confirm(), alert() // 대화상자
- if 조건문 <br/>
  switch 조건문 <br/>
  조건부 연산자를 활용한 조건 분기 <br/>
  논리 연산자를 활용한 조건 분기
- break 키워드 (반복문 벗어날 때 사용)
- 일반적으로는 switch 조건문보다 if 조건문을 많이 사용
- 논리 연산자 <br/>
  - ||(또는) 연산자 - 둘 중 하나가 true => 전체 true
  - &&(그리고) 연산자 - 둘 중 하나가 false => 전체 false
- 가우스 수학자의 덧셈 발상법
- 눈도장 찍기의 중요성 <br/>
  좌절하지 않으면서 이론도 절대로 무시하지 말고 계속 공부하면서 꾸준히 하자! <br/>
- 좋은 발상법(이론) => 중복된 코드 최소화 (코드가 짧아짐) <br/>
  하지만 처음에는 무식해도 완성을 어떻게든 해보는 것이 중요함!
- 문장 구분시 줄바꿈(개행) 또는 세미콜론(;) 사용
- 가독성이 좋은 코드

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=ESW7aHnYgYc&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=16)
[Reference2](https://www.youtube.com/watch?v=00g7l_bdBFk&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=17)
[Reference3](https://www.youtube.com/watch?v=K52sKtTlh4U&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=18)
[Reference4](https://www.youtube.com/watch?v=6vIvmiTJDZI&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=19)
[Reference5](https://www.youtube.com/watch?v=5k4OFfGSYmk&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=20)
