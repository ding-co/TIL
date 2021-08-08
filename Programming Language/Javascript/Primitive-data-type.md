## [문자열과 숫자]

### _문자열_

- "" or '' (차이 없음)
- 이스케이프 문자 사용 \
- 문자열에 적용할 수 있는 처리
  1. 문자열 연결 연산: 문자열 + 문자열
  2. 문자 선택 연산: 문자열[인덱스] -> 문자 하나 추출
  3. 문자열의 길이: 문자열.length -> 문자 개수

### _숫자_

- 정수, 실수 따로 구분은 안함 => number
- %: 나머지 연산자

#

## [불]

### _불 자료형_

- 참/거짓 나타내는 자료형 (true/false)
- 불을 만드는 법
  1. true/false 그대로 입력
  2. 비교 연산자 사용 (6가지)
     - ===, !==, >, >=, <, <=
- 불 사용 => 조건문에서 많이 활용
- 불 연산자 3가지
  1. 논리 부정 연산자: !불 (반전)
  2. 논리 합 연산자
  3. 논리 곱 연산자

#

## [불 연산]

### _논리 합 연산자_

- 연산자: ||
- 형태: 불 || 불 <br/>
  => 적어도 하나만 true 면 전체 값이 true

### _논리 곱 연산자_

- 연산자: &&
- 형태: 불 && 불 <br/>
  => 양쪽 모두가 true여야 전체 값이 true

실용적인 예 <br/>
ex) 사계절 구분, 시간, ...

#

## [2.1절 마무리]

### _자료형 검사_

- typeof 자료 => 자료형이 문자열로 나옴
- typeof() + typeof()
- typeof(typeof())

### _템플릿 문자열_

- ` 이용 (백틱, 역틱, 억음부호, 그레이브 엑센트)
- ${표현식}

```html
<script>
  console.log(`${14} ${125 + 55}`);
</script>
```

### _비교 연산자 ==, !=_

- 잘 사용 X (결과 예측 힘듬, 프로그램에서 잠재적 오류 발생 가능)
- javascript equality meme

#

## [상수와 변수 기본]

### _상수_

- 항상 같은 수
- 고정된 형태: const 식별자 = 자료
- 상수 관련 오류
  1. 한번 선언하면 중복 선언 불가능! => 다른 이름 사용
  2. const a 선언만 하면 오류 발생 => const 식별자 = 자료 고정된 형태 사용!
  3. 값 변경 불가

### _변수_

- 변할 수 있는 수 (값 변경 가능)
- let 식별자 = '자료' <br/>
  let 식별자 <br/>
  식별자 = '자료'
- 변수 관련 오류
  - 중복 선언 불가능! (같은 이름으로)

식별자를 상수/변수로 사용하겠다 => 선언/정의 <br/>
식별자 = 자료 => 할당 <br/>
처음으로 값 할당 => 초기화

#

## [2.2절 마무리]

### _변수에 적용할 수 있는 연산자_

- 상수에는 적용 불가 (변수에만 적용 가능)
- 복합 대입 연산자
  - +=, -=, \*=, /=, %=, ... <br/>
    cf) a += 100 경우에 a는 lvalue와 rvalue로 모두 사용
- 증감 연산자
  - ++, -- (전위 증/감, 후위 증/감) // 보통 후위 증/감 연산자 많이 사용

### _undefined 자료형_

1. 상수와 변수로 선언하지 않은 식별자
2. 값이 없는 변수

#

## [자료형 변환]

### _입력_

- 문자열 입력: prompt("메시지", "디폴트 값")
- 불 입력: confirm()

### _자료형 변환_

- 숫자 자료형으로 변환: Number()
- 문자열 자료형으로 변환: String()
- 불 자료형으로 변환: Boolean()
  1. 0, NaN, "", null, undefined => false
  2. 이외의 경우 => true

### _NaN_

- 자료형은 숫자
- 숫자가 아닌 값

#

## [2장 누적 예제]

### _inch -> cm 단위 변경_

```html
<script>
  // 입력: prompt() // inch 단위 숫자 입력 받음
  const input = Number(prompt('inch 단위의 숫자를 입력해주세요.'));

  // 처리: 1 inch -> 2.54cm
  const output = input * 2.54;

  // 출력: cm 단위의 숫자
  alert(`${input}inch = ${output}cm입니다.`);
</script>
```

#

### [Note]

- JS 기본 자료형 <br/>
  Boolean, Number, String, Null, Undefined, (Symbol)
- 인덱스는 0부터 시작
- 컴퓨터는 한정된 자원으로 자료를 표현 <br/>
  크기를 넘은 개념 또는 무한한 개념 표현 못함 <br/>
  실수도 정확하게 표현하지 못함 (부동 소수점 연산 불완전)
- 오차 발생할 수 없는 상황 <br/>
  ex) 우주 프로그램 등 모두 정수로 계산해서 소수로 변환
- JS; % 연산 시 왼쪽 피연산자의 부호를 따라감 (음수 연산 시) <br/>
  소수 이용하여 % 연산 하면 오차가 발생하여 잘 사용 X
- == 와 === 연산자는 다른 것임
- 문자열의 대소 비교는 사전순 (잘 사용 X)
- 단항 연산자: 피연산자 1개 <br/>
  이항 연산자: 피연산자 2개 <br/>
  삼항 연산자: 피연산자 3개
- 부정 연산자 제거하기 - 드모르강의 법칙 사용 <br/>
  ex) !(12 <= 현재 시간 && 현재 시간 <= 13) <br>
  => 12 > 현재 시간 || 현재 시간 > 13 <br/>
  부등식은 반대로! + 논리곱 <-> 논리합 교체!
- 연산자 | 1개 => 비트 합 연산자 <br/>
  연산자 & 1개 => 비트 곱 연산자 <br/>
  비트 연산자는 논리 연산이 아님
- 부등식/방정식 기본 개념 숙지 필요
- 일반적으로 비교 연산자가 오른쪽으로만 입을 열도록 하는 방식 <br/>
  변수를 왼쪽에 쓰는 방식
- 범위 표현 시 논리 연산자 사용
- typeof는 연산자로 사용되는 키워드 // 단항 연산자
- 연산 우선 순위는 () 이용하기
- 현대 언어들이 상수와 변수 나누는 대표적 이유 <br/>
  => 안전하게 쓸 수 있음, 다중 처리 때 안정성 보장
- 할당 연산자의 방향성; = 은 오른쪽에 있는 것을 왼쪽에 넣는 방향성을 가진 연산자
- 상수와 변수의 사용 범위 <br/>
  상수는 언제 쓰고? -> 기본적 <br/>
  변수는 언제 쓰지? -> 변수!
- C, Java, C#, C++ 등 <br/>
  => 코드를 작성하고 컴파일
- 루비, 파이썬, 루아 등 <br/>
  => 기본적으로 인터프리터 언어 <br/>
  => 컴파일 최적화 힘듦
- 자바스크립트 <br/>
  => 어떻게든 해볼테니, 추가 정보가 필요! <br/>
  => 상수와 변수 구분해서 사용!
- lvalue, rvalue <br/>
  lvalue (left value); 넣는 놈 (메모리 위치) <br/>
  rvalue (right value); 꺼내는 놈, 값
- 함수 실행 결과로 나온 최종적인 결과 => 리턴 값
- Number(true) -> 1 (켜져있다, 존재한다) <br/>
  Number(false) -> 0 (꺼져있다, 존재하지 않는다)
- 프로그램(Program = pro[미리] + gram[작성된 것])
- 컴퓨터; 입력 -> 처리 -> 출력
- 현대; 작은 프로그램(서브 프로그램)들이 모여서 거대한 프로그램 구성
- 개발에 필요한 지식
  1. 생각 -> 코드 (프로그래밍 지식)
  2. 수학적 지식 등 추가적 지식
- '무엇을 먼저 해야겠다' 라는 발상이 제일 중요!

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=6F5Wmm4IOLQ&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=8)
[Reference2](https://www.youtube.com/watch?v=X-j4Za0v-S8&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=9)
[Reference3](https://www.youtube.com/watch?v=9P9OM-taRiU&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=10)
[Reference4](https://www.youtube.com/watch?v=F5M0BaX7knI&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=11)
[Reference5](https://www.youtube.com/watch?v=lPjAr8sdOuM&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=12)
[Reference6](https://www.youtube.com/watch?v=Y4bGtMlJ8P8&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=13)
[Reference7](https://www.youtube.com/watch?v=FvCvDoj1TKk&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=14)
[Reference8](https://www.youtube.com/watch?v=mLL3pG2SsSk&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=15)
