## <u>[기본 API 클래스]</u>

### - 자바 기본 제공 표준 API

<br>

### _`Java API Document`_

- 자바 라이브러리 (직접 작성하지 않고 가져다 쓸 수 있음)
- [자바 API 도큐먼트](https://docs.oracle.com/en/java/javase/)
- Java Platform: 자바 언어가 실행하는 환경
- Standard Edition: JDK (Java Development Kit)
- [JDK8](https://docs.oracle.com/javase/8/docs/api/index.html) / [JDK11](https://docs.oracle.com/en/java/javase/11/docs/api/index.html)
- 이클립스; 찾고자 하는 내용 선택(드래그)해서 F1 - Help 뷰 - 링크 클릭

#

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
- 모두 정적 필드와 정적 메소드 (OS 기능 - 자바에서 바로 사용)

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

- **_String 생성자_**

  - 직접 String 객체 생성 (다양한 생성자 overloading 되어 있음) <br/>
    ex) String str = "자바";

    ```java
    public class Main {
      public static void main(String[] args) {
        byte[] bytes = new byte[100];

        System.out.print("입력: ");
        int readByteNo = System.in.read(bytes);

        // - 2 => enter (/r /n)
        String str = new String(bytes, 0, readByteNo - 2);
        System.out.println(str);
      }
    }
    ```

- **_String 메소드_**

  - _*charAt(int index)*_

    - 문자 추출
    - 지정한 index 해당 문자 return char

    <br/>

  - _*equals(Object anObject)*_

    - 두 문자열 비교
    - == 연산자 사용 X
    - Object 클래스의 메소드 override
    - 기준문자열객체.equals(비교문자열객체)

    <br/>

  - _*getBytes()*_

    - 문자열 -> byte[] <br/>
      각각의 문자를 byte로 만들어서 배열로 저장 후 return
    - OS가 기본적으로 사용하는 문자셋 이용 -> byte <br/>
      (시스템(OS)의 기본 문자셋으로 인코딩된 바이트 배열 리턴)
    - 윈도우 운영체제; MS949 (EUC-KR) 문자셋 이용 (영어 1바이트, 한글 2바이트) <br/>
      cf. UTF-8 문자셋 (영어 1바이트, 한글 3바이트) <br/>
    - byte[] -> 문자열 디코딩 시, 어떤 문자셋으로 인코딩 되었는지에 따라 다름 <br/>
      String(byte[] bytes, String charsetName) 생성자 이용 <br/>
      charsetName 에 처음에 인코딩 했을 시의 문자셋으로 동일하게 적용해야 복원이 잘 됨

    <br/>

  - _*getBytes(Charset charset)*_

    - 우리가 제공하는 set 정보 이용 -> byte <br/>
      ex) EUC-KR, UTF-8
    - charset이 정한 기준대로 byte 배열 만들어짐 <br/>
      (특정 문자셋으로 인코딩된 바이트 배열 리턴)

    <br/>

  - _*indexOf(String str)*_

    - 주어진 문자열 시작 위치 return int
    - 문자열 위치 찾기 용도
    - 전체 문자열에서 주어진 문자열이 포함되어 있지 않으면 return -1 <br/>
      cf) contains("찾는 문자열")

    <br/>

  - _*length()*_

    - 문자열 길이 return int
    - input form 에서 사용자의 id, password 등 받을 때, <br/>
      사용자가 최소한의 문자 수를 입력하는지 체크 용도에 활용 가능

    <br/>

  - _*replace(CharSequence target, CharSequence replacement)*_

    - 기존 존재하는 문자열에서 특정 부분 대체 (문자열 대치)
    - replace("찾고자 하는 문자열", "대치 시킬 새로운 문자열")
    - <u>힙 영역에 새로운 문자열 객체가 생성됨</u> <br/>
      (원본 문자열은 변경 X, 비파괴적 처리 메소드임) <br/>
      이유: String 타입은 문자열이 한번 저장되면 다른 문자열로 변경 불가 <br/>
      (immutable object)

    <br/>

  - _*substring(int beginIndex)*_

    - 문자열에서 특정 위치 ~ 마지막까지 일부분 추출 <br/>
      (주어진 인덱스 ~ 끝까지)

    <br/>

  - _*substring(int beginIndex, int endIndex)*_

    - 문자열에서 시작 위치 ~ 끝 위치 일부분 추출 <br/>
      (주어진 시작과 끝 인덱스 사이)
    - 주어진 끝 위치는 exclusive [미만]

    <br/>

  - _*toLowerCase()*_, _*toUpperCase()*_

    - toLowerCase(): 원본 문자열(알파벳) 모두 소문자로 변환한 새로운 문자열 return
    - toUpperCase(): 원본 문자열(알파벳) 모두 대문자로 변환한 새로운 문자열 return
    - 검색 엔진에 활용
    - 힙 영억에 새로운 문자열 객체 생성됨 <br/>
      (원본 문자열 변경 X, 비파괴적 처리 메소드)

    <br/>

  - _*trim()*_

    - 문자열 앞, 뒤 공백 제거
    - 힙 영역에 새로운 문자열 객체 생성됨 <br/>
      (원본 문자열 변화 X, 비파괴적 처리 메소드)

    <br/>

  - _*valueOf(int i)*_, _*valueOf(double d)*_

    - 기본 타입 값 -> 문자열
    - 여러 기본 타입 메소드 overloading 되어 있음
    - String.valueOf() 정적 메소드

<br/>

> Wrapper(포장) 클래스

- 문자열 -> 기본 타입 변환 시 사용 가능
- 기본 타입의 데이터를 갖는 객체 만들 때 사용 <br/>
  기본 타입의 값을 내부에 두고 포장하는 객체 (포장 객체) <br/>
  ex 1) char (기본 타입) - Character (포장 클래스) <br/>
  ex 2) int (기본 타입) - Integer (포장 클래스)
- Boxing: 기본 타입의 값 -> Wrapper 객체 <br/>
  (1. 생성자 이용 - 기본 타입의 값 / 문자열 -> 기본 타입의 값) // deprecated <br/>
  (2. Wrapper 클래스가 가진 valueOf() 정적 method 이용; () 안에 기본 타입의 값 / 문자열 모두 가능) <br/>
- Unboxing: Wrapper 객체 -> 기본 타입의 값 <br/>
  (기본 타입 이름 + Value() 메소드 호출) <br/>
  ex 1) obj.charValue() <br/>
  ex 2) obj.intValue() <br/>
- Auto boxing: Wrapper 클래스 타입에 기본 값이 대입 될 경우 자동 박싱 발생
- Auto unboxing: 기본 타입에 포장 객체가 대입 되거나 연산에서 자동 언박싱 박생
- 문자열 -> 기본 타입 값으로 변환 <br/>
  포장 클래스로 문자열 -> 기본 타입 값 변환 <br/>
  'parse+기본 타입 이름' 정적 메소드 <br/>
  ex) Integer.parseInt(), Double.parseDouble() <br/>
- 포장 값 비교 <br/>
  포장 객체는 내부 값 비교 위해 == 및 != 연산자 사용 X <br/>
  언박싱한 값 얻어 비교!
- 박싱 객체 공유 <br/>
  boolean 타입: true, false (값의 범위) <br/>
  char 타입: \u0000 ~ \u0007f (값의 범위) <br/>
  byte, shrot, int 타입: -128 ~ 127 (값의 범위) <br/>
  => <u>언박싱한 값으로 비교하는게 좋음</u> <br/>
  => <u>equals() 활용!!!</u>

<br/>

> Math 클래스

- 수학 함수 이용
- 모두 정적 메소드

- **_수학 계산에 사용하는 다양한 메소드_**

  - _*int abs(int a), double abs(double a)*_

    - 절대값

    <br/>

  - _*double ceil(double a)*_

    - 올림값

    <br/>

  - _*double floor(double a)*_

    - 버림 값

    <br/>

  - _*int max(int a, int b), double max(double a, double b)*_

    - 최대값

    <br/>

  - _*int min(int a, int b), double min(double a, double b)*_

    - 최소값

    <br/>

  - _*double random()*_

    - 랜덤값 (난수값)
    - 0.0 이상 1.0 미만 <br/>
      cf). 1 ~ 10 임의의 정수 난수 얻기 <br/>
      (int)(Math.random() \* 10) + 1

    <br/>

  - _*double rint(double a)*_

    - 가까운 정수의 실수값

    <br/>

  - _*long round(double a)*_

    - 반올림값

#

### _`java.util 패키지`_

- 날짜 정보 제공 유용한 API 포함
- import 필요 <br/>
  cf) Ctrl + Shift + o (자동 임포트)

<br/>

> Date 클래스

- 날짜 표현 클래스
- 날짜와 시간 정보 저장 클래스
- 객체 간 날짜 data 주고 받을 때 매개 변수나 리턴 타입으로 주로 사용 <br/>
  ex 1) void method(Date date){...}, Date method(){...} <br/>
  ex 2) <u>Date now = new Date();</u>
- 원하는 날짜 형식 문자열 얻기 위해 java.text 패키지의 SimpleDataFormat 클래스와 함께 사용 <br/>
  ex) <u>SimpleDateFormat sdf = new SimpleDateFormat("yyyy년 MM월 dd일 hh시 mm분 ss초");</u>
- format() 메소드 호출 <br/>
  ex) <u>String strNow = sdf.format(now);</u>

<br/>

> Calendar 클래스

- 달력을 표현한 클래스
- 운영체제의 날짜와 시간 기준으로 다양한 정보 얻을 수 있음
- 추상 클래스이므로 new 연산자 사용하여 인스턴스 생성 불가
- getInstance() 정적 메소드 이용 -> Calendar 하위 객체 얻을 수 있음 <br/>

  ```java
  Calendar now = Calendar.getInstance();

  int year = now.get(Calendar.YEAR);        // return 연도
  int month = now.get(Calendar.MONTH) + 1;  // return 월 (0 ~ 11) + 1
  int day = now.get(Calendar.DAY_OF_MONTH); // return 일
  int week = now.get(Calendar.DAY_OF_WEEK); // return 요일 (1 일 ~ 7 토)
  int amPm = now.get(Calendar.AM_PM);       // return 오전/오후
  int hour = now.get(Calendar.HOUR);        // return 시
  int minute = now.get(Calendar.MINUTE);    // return 분
  int second = now.get(Calendar.SECOND);    // return 초
  ```

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
- Enter 입력 시, /r /n (2개 키코드 값 입력됨) <br/>
  /r (13) 캐리지 리턴, /n (10) 라인 피드
- ssn(social security number): 주민번호
- String 에서 new로 String 객체를 생성하지 않고 그냥 문자열 literal로 번지를 참조변수에 대입 시, <br/>
  같은 객체를 공유하게 됨 <br/>
  new 로 생성하면 항상 새로운 별개의 객체가 됨
- 문자열을 byte 배열로 바꾸는 과정: 인코딩 <br/>
  byte 배열을 다시 문자열로 만드는 과정: 디코딩
- 이클립스; window - Preferences - General - Workspace; 윈도우 OS 기본 인코딩 문자셋 (MS949) 확인 가능
- 배열 길이 => .length <정적 필드 속성> <br/>
  문자열 길이 => .length() <메소드>
- Java 언어; 문자열 내부 문자 대소문자 구분 O (case sensitive)
- Java 언어; System.out.println() 안에 여러 값 ,로 넣을 수 없음
- 원래 Java 에서는 기본 타입의 값을 클래스 타입 변수에 대입할 수 없고,<br/>
  객체도 기본 타입 변수에 대입할 수 없지만 <br/>
  자동 박싱/언박싱 개념에서는 가능
- 추상 클래스는 new 연산자로 인스턴스 생성 불가

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=4g6CWh3weuY&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=57)
[Reference2](https://www.youtube.com/watch?v=RHi_kkS2noQ&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=58)
[Reference3](https://www.youtube.com/watch?v=nJbaGQtFLTU&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=59)
[Reference4](https://www.youtube.com/watch?v=IEs-pnSXvoU&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=60)
[Reference5](https://www.youtube.com/watch?v=u4i4DMqG8b0&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=61)
[Reference6](https://www.youtube.com/watch?v=meNQOC_Qp3U&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=62)
[Reference7](https://www.youtube.com/watch?v=v_kBdmxktG0&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=63)
[Reference8](https://www.youtube.com/watch?v=fizxPTz7jo0&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=64)
[Reference9](https://www.youtube.com/watch?v=SPQ6brNjOSE&list=PLVsNizTWUw7HZTPU3GpS7nmshXjKKvlbk&index=65)
