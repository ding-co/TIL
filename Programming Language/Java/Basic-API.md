## <u>[기본 API 클래스]</u>

### - 자바 기본 제공 표준 API

<br>

### _`Java API Document`_

- 자바 라이브러리 (직접 작성하지 않고 가져다 쓸 수 있음)
- [자바 API 도큐먼트](https://docs.oracle.com/en/java/javase/)
- Java Platform: 자바 언어가 실행하는 환경
- Standard Edition: JDK (Java Development Kit)
- [JDK8](https://docs.oracle.com/javase/8/docs/api/index.html) / [JDK11](https://docs.oracle.com/en/java/javase/11/docs/api/index.html)
- 이클립스; F1 - Help 뷰 - 링크 클릭

<br/>

### _`java.lang 패키지`_

- 클래스, 인터페이스 import 없이 사용 가능

<br/>

> Object 클래스

- 모든 자바 클래스의 최상위 부모 클래스 (root)
- 필요 시 Object 클래스의 method override 가능

<br/>

- **_객체 비교 메소드 equals()_**

  - 비교 객체를 매개값으로 받음 (return boolean)
  - 비교 연산자인 ==와 동일 결과 return
  - 번지 비교 (같은 객체 참조?)
  - **method override** <br/>
    (for 두 객체가 필드값 같은 동등 객체인지 비교)
  - 여기서의 동등 객체란 객체는 서로 다르지만 내부 데이터 같은 객체
  - 사전에 두 객체는 같은 종류의 객체여야 함

  <br/>

  ```java
  public class Member {
    public String id;

    public Member(String id) {
      this.id = id;
    }

    @Override
    public boolean equals(Object obj) {
      if(obj instanceof Member) {
        Member member = (Member) obj;
        if(id.equals(member.id)) {    // String 클래스가 가지고 있는 equals method
          return true;
        }
      }
      return false;
    }
  }
  ```

<br/>

- **_객체 해시코드 메소드 hashCode()_**

  - return int (객체 식별 정수값)
  - 객체 메모리 번지 이용하여 해시코드 생성
  - **method override** <br/>
    (for 두 객체가 동등한지 비교)
  - 논리적으로 완전히 동등 객체가 되기 위해서는 hashCode()와 equals() 모두 override 필요
  - 같은 해시코드 갖고 있는지 먼저 체크 후 객체 내부 데이터 비교 <br/>
    (hashCode() return true => equals() return true => 동등 객체)
  - HashSet, Hashtable, HashMap API
  - HashMap; 키가 동등한지 아닌지 hashcode로 활용 <br/>
    (동일한 키 중복 저장 X; overwrite 함)

<br/>

```java
import java.util.HashMap;

public class KeyExample {

  public static void main(String[] args) {

    HashMap<String, String> hashMap = new HashMap<String, String>(); // 키, 값 구조

    hashMap.put("key1", "value1");
    hashMap.put("key2", "value2");
    hashMap.put("key1", "value3"); // 예전 키, 값 쌍 제거하고 새로운 키, 값 쌍으로 대체

    System.out.println(hashMap.size()); // 해시맵 키,값 쌍 개수 => 2
  }
}
```

<br/>

- **_객체 문자 정보 메소드 toString()_**

  - return String
  - **method override** <br/>
    중요 문자 정보 return
  - 참조변수만 출력하면 자동으로 toString() 메소드 호출하여 출력됨

<br/>

> System 클래스

- OS 정보가 가지고 있는 표준 입/출력 장치 이용
- JVM 종료 시 사용
- G.C 실행 요청 시 사용
- 모든 필드와 메소드는 정적 필드와 정적 메소드 (OS 기능 - 자바에서 바로 사용)

<br/>

- **_프로그램 종료 메소드 exit()_**

  - return void <br/>
    argument: int status (종료 상태값)
  - exit(0); 정상 종료
  - JVM 강제 종료 (자바 프로세스 종료)

<br/>

- **_현재 시각 읽기 메소드 currentTimeMillis() / nanoTime()_**

  - currentTimeMillis(): 1 / 10^3 단위 long 값 return
  - nanoTime(): 1 / 10^9 단위 long 값 return (정밀 시간 측정)

<br/>

> Class 클래스

- 클래스(바이트 코드 파일)를 메모리로 로딩할 때 사용
- resource 파일 찾을 때 이용
- 클래스와 인터페이스의 메타 데이터 관리 <br/>
  (메타 데이터: 클래스/인터페이스 타입 이름 및 파일 경로 정보, 필드 정보, 생성자 정보, 메소드 정보) <br/>

<br/>

- **_Class 객체 얻기 메소드 forName() / getName()_**

  - 클래스로부터 얻는 방법

    - 클래스이름.class
    - Class.forName("패키지...클래스이름") <br/>
      [예외처리 필요]

    <br/>

  - 객체로부터 얻는 방법 (이미 인스턴스 생성되어 있는 경우)

    - 참조변수.getClass()

  <br/>

  - getName(): 클래스 전체 이름 얻기 <br/>
    getSimpleName(): 패키지 제외한 클래스 이름 얻기 <br/>
    getPackage(), getPackage().getName() <br/>
    getField(), getConstructors(), getMethods()

<br/>

- **_클래스 경로 활용 => 주위 리소스 절대 경로 얻기 getResource("파일 이름").getPath()_** <br/>

  - getResource(): return URL (type)
  - URL.getPath()
  - 절대 경로 구하여 이미지 데이터 읽고 UI에 나타내는 것으로 활용 가능

<br/>

> String 클래스

- 문자열 저장할 때 사용

<br/>

> Wrapper 클래스

- 기본 타입의 데이터를 갖는 객체 만들 때 사용
- 문자열 -> 기본 타입 변환 시 사용

<br/>

> Math 클래스

- 수학 함수 이용
- 모두 정적 메소드

<br/>

#

## [Note]

- GC: Garbage Collector (쓰레기 수집기)
- API: Application Programming Interface
- class에도 final 키워드 적용 가능
- static final fieldName; 상수
- Case Insensitive: 대소문자 구분 X <br/>
  Case Sensitive: 대소문자 구분 O
- Deprecated: 가급적 사용 X (앞으로 지원 안할 수도 있음)
- Ctrl + Shift + O: 자동 import
- Ctrl + Space bar: 자동 override
- (Java) 클래스의 필드/생성자/메소드 정보 얻어서 활용 => Reflection
- Class 객체 얻기 메소드; 모두 같은 객체 참조 (새로운 인스턴스 생성한 적 X)
-

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=4g6CWh3weuY&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=57)
[Reference2](https://www.youtube.com/watch?v=RHi_kkS2noQ&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=58)
[Reference3](https://www.youtube.com/watch?v=nJbaGQtFLTU&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=59)
[Reference4](https://www.youtube.com/watch?v=IEs-pnSXvoU&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=60)
