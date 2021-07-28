# Java

## <u>[익명 객체]</u>

[Reference1](https://www.youtube.com/watch?v=yMGt8KYikac&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=52)
[Reference2](https://www.youtube.com/watch?v=ZWVSnfwth8M&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=53)

<br/>

### _`익명 자식 객체 생성`_

> 자식 클래스가 재사용되지 않고 특정 위치에서만 사용되는 경우 편리

```java
[상속]
부모클래스 변수 = new 부모클래스(매개값, ...) { ... };

// 부모클래스를 상속해서 { ... } 에 자식 클래스 내용 작성 후
// 자식 객체를 생성하고 부모클래스 타입의 변수에 대입
// 익명 자식 객체는 항상 부모 타입 변수에 대입됨
```

- 필드 선언 시, 초기값으로 익명 자식 객체 생성하여 대입
- 메소드 내에서 로컬 변수 선언 시 초기값으로 대입
- 매개 변수의 매개값으로 익명 자식 객체 생성하여 대입

<br/>

### _`익명 구현 객체 생성`_

> 구현 객체 클래스가 재사용되지 않고 특정 위치에서만 사용되는 경우 편리 <br/>
> UI 이벤트 처리에 많이 활용

```java
[구현]
인터페이스 변수 = new 인터페이스() { ... };

// 인터페이스는 객체 생성 불가
// 인터페이스를 구현한 클래스 내용을 { ... } 에 선언하고
// { ... }를 가지고 생성한 구현 객체를 인터페이스 타입의 변수에 대입
```

- 필드 선언 시 초기값으로 익명 구현 객체 생성하여 대입
- 메소드 내에서 로컬 변수 선언시 초기값으로 익명 구현 객체 생성하여 대입
- 매개변수의 매개값으로 익명 구현 객체 생성하여 대입

<br/>

### _`익명 객체의 로컬 변수 사용`_

- 메소드 종료 시 메소드 안의 로컬 변수들은 다 사라짐
- 하지만, 메소드 안의 익명 객체는 계속 힙 영역에 남아서 실행 상태로 존재 가능 <br> (cf. <u>쓰레드 개념</u>)
- 컴파일 시 익명 객체에서 사용하는 매개변수나 로컬변수는 final 특성 가짐 (값 변경 불가)
- 따라서 메소드 안의 익명 객체에서 사용할 메소드 내의 매개변수나 로컬변수는 final 특성을 가짐 <br> [Java 8 이후 final 생략 가능] <br/> (cf. 로컬 클래스 내부에서 로컬 변수 사용 시 final 특성 가짐)
- 필드 값은 자유롭게 변경 가능

#

## <u>[예외 처리]</u>

[Reference1](https://www.youtube.com/watch?v=9NzkWg8btNM&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=54)

<br>

### _`예외와 예외 클래스`_

> 에러(Error): 컴퓨터 H/W 관련 고장으로 응용프로그램 실행 오류 발생 <br/>
> 예외(Exception): 프로그램 자체에서 발생하는 오류 (사용자 조작 실수/개발자 잘못된 코딩)

- 예외 발생 가능성이 높은 코드를 컴파일 할 때 컴파일러는 예외 처리 유무 확인
- java.lang.Exception: 모든 예외 클래스의 최상위 부모
- 예외처리 코드: 예외가 발생하고 나서 실행하는 코드

  <br/>

> 일반 예외(exception)

- 컴파일러 체크 예외

<br/>

> 실행 예외(runtime exception)

- 컴파일러 넌 체크 예외
- 개발자 경험에 의존
- RuntimeException 상속 받는 예외
- ex) NullPointerException, ArrayIndexOutOfBoundsException, <br/> NumberFormatException, ClassCastException ...

<br/>

### _`예외 처리`_

<br/>

#

## [Tip]
