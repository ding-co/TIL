## [구문 오류와 예외]

### _구문 오류_

- 프로그램 실행 전에 발생하는 오류
- SyntaxError <br/>
  ex) 괄호 짝, 문자열 열고 닫기, ...

<br/>

### _예외 (런타임 오류)_

- 프로그램 실행 중에 발생하는 오류 <br/>
  (오류 발생 하지 않은 부분은 정상 실행)
- Exception <br/>
  ex) 식별자 이름 잘못 적기, 네트워크 통신 오류로 데이터 받지 못함, ...

#

## [예외 처리]

### _예외 처리_

- 기본 예외 처리; if-else 조건문 이용 (예외 발생 예상 가능한 경우)
- 고급 예외 처리; try-catch-finally 이용 (대부분 예외 예상 불가능)
  - try {예외 발생 가능성 있는 코드};
  - catch (예외객체) {예외 발생했을 때 실행할 코드};
    - 예외객체.name와 예외객체.message (브라우저마다 보유 속성 다름)
  - finally {무조건적으로 실행하는 코드};

#

## [finally를 사용하는 이유와 throw 구문]

### _`finally`를 사용하는 이유_

- 무조건적으로 실행하는 코드
- try catch 구문 내에 return/break 키워드 존재할 때 의미를 가짐

```js
const 예 = () => {
  try {
    console.log('예외가 발생할 가능성이 있는 코드');
    return;
  } catch (예외_객체) {
    console.log('예외가 발생할 때 실행할 코드');
  } finally {
    console.log('무조건적으로 실행할 코드');
  }
};

예();
```

### _`throw` 구문_

```js
// 원 둘레 구하는 함수
const getPerimeter = (r) => {
  // 기본 예외 처리
  if (r < 0) {
    // 강제적으로 오류 발생
    throw '길이는 음수가 될 수 없습니다.';
  }
  const pi = 3.14;
  return 2 * pi * r;
};

// 반지름, 길이 모두 양수 => 무조건 양수 리턴
// 잠재적 위험성 내포 -> 예외 처리!

try {
  console.log(getPerimeter(-10));
} catch (e) {
  console.log('어떤 문제가 발생했습니다.');
}

console.log('프로그램 정상적으로 종료되었습니다.');
```

#

## [객체 매개변수]

```js
function 메일보내기(발신인, 수신인, 내용) {
  console.log(`발신인: ${발신인}`);
  console.log(`수신인: ${수신인}`);
  console.log(내용);
}

메일보내기('구름', '별', '간식줘!');

// 같은 자료형의 매개변수가 여러 개면 무엇을 의미하는지 이해하기 힘듦
// 프로그램 규모가 커져서 함수 선언과 함수 호출 사이 간격이 멀어지면 문제 원인 파악 힘듦
```

```js
// 과거의 패러다임: 짧고 빠른 코드 작성!
// 현재의 패러다임: 쉽게 읽을 수 있는 코드 작성!

// 객체를 활용한 이름 있는 매개변수 (객체 매개변수)
function 메일보내기(객체) {
  console.log(`발신인: ${객체.발신인}`);
  console.log(`수신인: ${객체.수신인}`);
  console.log(객체.내용);
}

// 같은 자료형으로 매개변수 구성할 때 매개 변수 이름 붙여서 호출함
메일보내기({
  발신인: '별',
  수신인: '구름',
  내용: '간식줘!',
});

// 하지만 작성 내용이 많아져서 실수 발생 가능 ex) 내용 -> 내욤
// 오류 찾는데 시간 정말 많이 소요 가능...

// 따라서 예외를 강제로 발생시켜서 개발자가 예외를 처리하도록 만들어야 함
```

```js
// 객체 매개변수 예외 발생 시키기
function 메일보내기(객체) {
  // 매개변수가 잘못 들어왔다! -> 예외!!

  // 과거 방법 1.
  if (typeof 객체.발신인 === 'undefined') {
    throw '발신인 매개변수에 문제가 있습니다!';
  }
  if (typeof 객체.수신인 === 'undefined') {
    throw '수신인 매개변수에 문제가 있습니다!';
  }
  if (typeof 객체.내용 === 'undefined') {
    throw '내용 매개변수에 문제가 있습니다!';
  }
  console.log(`발신인: ${객체.발신인}`);
  console.log(`수신인: ${객체.수신인}`);
  console.log(객체.내용);
}

메일보내기({
  발신인: '별',
  수신인: '구름',
  내용: '간식줘!',
});
```

```js
// 과거 방법 2.
function isRequired(객체, 속성이름) {
  if (typeof 객체[속성이름] === 'undefined') {
    throw `${속성이름} 매개변수에 문제가 있습니다!`;
  }
}
function 메일보내기(객체) {
  isRequired(객체, '발신인');
  isRequired(객체, '수신인');
  isRequired(객체, '내용');
  console.log(`발신인: ${객체.발신인}`);
  console.log(`수신인: ${객체.수신인}`);
  console.log(객체.내용);
}

메일보내기({
  발신인: '별',
  수신인: '구름',
  내용: '간식줘!',
});
```

```js
// 현대적인 방법 - 객체 매개변수 문법 + 기본값 지정/예외 강제 발생 가능
// 객체 매개변수 예외 처리 방법
function isRequired(이름) {
  throw `${이름} 매개변수에 문제가 있습니다.`;
}

function 메일보내기({
  발신인 = isRequired('발신인'),
  수신인 = isRequired('수신인'),
  내용 = '기본값',
}) {
  console.log(`발신인: ${발신인}`);
  console.log(`수신인: ${수신인}`);
  console.log(내용);
}

메일보내기({
  발신인: '별',
  수신인: '구름',
  내용: '간식줘!',
});
```

```js
// 객체 매개변수의 객체 기본값

// 현재 자신의 계정 -> 관리자 계정으로 문제 발생 했다고 메일 보냄
function 메일보내기({
  발신인 = '사용자',
  수신인 = '관리자',
  내용 = '문제가 발생했음!',
}) {
  console.log(`발신인: ${발신인}`);
  console.log(`수신인: ${수신인}`);
  console.log(내용);
}

// 적어도 매개변수로 객체가 들어 와야 함
메일보내기({});
```

```js
// 매개변수 입력하지 않으면, {}가 기본값으로 들어간 것으로 인식한 뒤 다음 처리 진행함
function 메일보내기({
  발신인 = '사용자',
  수신인 = '관리자',
  내용 = '문제가 발생했음!',
} = {}) {
  console.log(`발신인: ${발신인}`);
  console.log(`수신인: ${수신인}`);
  console.log(내용);
}

// 매개변수로 아무 것도 넘기지 않음
메일보내기();
```

#

### [Note]

- 자바스크립트: 동적 언어; 구문오류 제외한 모든 오류 => 예외
- null (없음)
- 예외 처리 안하면 이후의 코드 실행 안됨 <br/>
  예외 처리 하면 이후의 코드 정상 실행
- 예외 객체; 예외와 관련된 정보 담고 있는 객체
- JS는 매우 유연한 언어라 문법적으로 예외 발생 경우 매우 적음
- 파일 처리 등에서 finally 절 많이 나옴
- 예외 처리; 모든 것을 예측하기 힘듦, 경험적으로 얻게 되는 테크닉
- JS에서 예외 처리하는 대표적인 2가지 예
  1. 다른 사람이 강제로 발생시킨 예외를 처리하는 경우
  2. 없는 속성에 접근해서 활용하는 경우
- 일반적으로 개발 시 숫자 등을 직접 입력하는 것보다 <br/>
  상수를 한번 거쳐서 입력하는 것이 좋음 (가독성 증가)
- 부동 소수 계산 오차의 한계
- 예외 처리의 가장 힘든점; 노동(돈/시간)과 위험성의 균형 잡기
- throw new Error('')
- JS; 언어가 매우 유연해서 기본적인 예외가 거의 발생 X <br/>
  => 굉장히 많은 잠재적인 위험/버그의 잠재성을 내포 <br/>
  => throw 키워드 사용하여 예외 강제 발생 <br/>
  => 프로그램 중단되므로 try catch 구문 사용
- throw 키워드는 라이브러리/프레임워크 만들 떄 주로 사용
- throw 키워드는 직접적으로 잘 사용 안하고 이걸로 발생한 예외를 당하게 될 때, <br/>
  => try catch 구문 사용
- 잠재적인 규칙/법 (프레임워크라는 국가 아래 내가 보살핌 받음)
- JS는 동적 프로그래밍 언어 특성 가짐
- 현대에는 프로그램의 규모가 커지면서 코드를 작성하는 것보다 보는 시간이 더 많아짐 <br/>
  => 가독성의 중요성!!!

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=h6uMV3iuGHE&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=54)
[Reference2](https://www.youtube.com/watch?v=v4F15l_1Zws&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=55)
[Reference3](https://www.youtube.com/watch?v=-1a9z-bbU9g&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=57)
[Reference4](https://www.youtube.com/watch?v=9vbzoKHhUlM&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=58)
[Reference5](https://www.youtube.com/watch?v=uMZaeGzbmSM&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=59)
