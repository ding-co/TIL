## <u>[예외 처리]</u>

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

- unhandled Exception type은 컴파일러가 체크해주는 일반 예외
- RuntimeException는 컴파일러가 체크하지 않음

<br/>

> 예외 처리 코드

- try-catch-[finally] 블록
- 생성자 내부/메소드 내부에서 작성되는 예외 처리 코드

```java
try {

} catch(예외 클래스 e) {

  예외 처리

} [finally] {

  항상 실행; // finally는 옵션

}
```

<br/>

- 다중 catch
- Exception: 모든 예외의 최상위 부모 클래스
- 구체적 예외 처리 이후 마지막은 catch (Exception) 으로 나머지 예외 처리

```java
try {

} catch(ArrayIndexOutOfBoundsException e) {

  예외 처리1

} catch(NumberFormatException e) {

  예외 처리2

} catch(Exception e) {

}
```

<br/>

> 예외 떠넘기기

- throws 키워드
- 메소드에서 처리하지 않은 예외를 호출한 곳으로 넘기는 역할
- 메소드를 호출한 곳에서 다양한 방식으로 처리 가능
- 메소드 선언시 , (쉼표) 이용하여 여러 개 떠넘기기 가능
- main 메소드에 throws 키워드 사용하는 것은 좋지 않음 <br/>
  (간단하게 테스트 용도로 하기도 함)

#

## [참고]

- eclipse; [source] -> [format] // ctrl + shift + f; 코드 라인 정리
- main 메소드는 JVM이 호출함
- 예외객체.printStackTrace() // 예외 객체 발생 부분 추적해서 print

#

### [레퍼런스]

[Reference1](https://www.youtube.com/watch?v=9NzkWg8btNM&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=54)
[Reference2](https://www.youtube.com/watch?v=QJm-96zVBco&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=55)
[Reference3](https://www.youtube.com/watch?v=uCo-VmCYbcA&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=56)
