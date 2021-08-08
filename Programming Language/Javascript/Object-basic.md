## [객체 기본]

### _객체_

- 배열도 객체의 일종 (typeof 로 확인 가능)
- {키1: 값, 키2: 값}
- 키 => 식별자 규칙 적용 <br/>
  1. 숫자로 시작 X <br/>
  2. 특수 기호는 $와 \_만 허용
- 객체의 속성 접근 방법 <br/>
  1. object['키']
  2. object.키 <------ 많이 사용!
- 객체의 속성에 대한 값 변경

### _속성과 메서드_

- 속성
- 메서드 (객체 내부의 함수) <br/>
  ex) const dog = { bark: function() {} } <br/>
  => dog.bark() 로 호출 가능
- 익명 함수 vs 화살표 함수 <br/>
  익명 함수; 메서드 내에서 this. 키워드를 사용하면 자기 자신을 의미<br/>
  화살표 함수; this. 키워드 사용하면 window 객체가 지정됨 (this 바인딩 X)
- 익명 함수 내에서만 this. 키워드 사용하자! <br/>
  JS; 객체 자기 자신 나타낼 때 무조건 this. 사용!

#

## [객체 속성 추가와 제거]

### _객체에 정적으로 속성 추가하기_

- 처음 만들 때 같이 만드는 것
- 객체의 키와 값을 정적으로 생성

### _객체에 동적으로 속성 추가하기_

- 나중에 만드는 것
- 객체 만들어진 이후에 추가적으로 속성 부여
- 객체의 키와 값을 동적으로 생성 <br/>
  객체.속성 = 값 <br/>
  객체['속성'] = 값
- 객체의 키와 값을 동적으로 제거 <br/>
  delete 객체.속성 <br/>
  delete 객체['속성']

#

## [기본 자료형과 객체 자료형, 프로토타입]

### _기본 자료형_

- 스택에 값 저장
- 숫자
- 문자열
- 불
- 이론적으로 속성과 메서드 가질 수 없음 (추가 불가)
- new 연산자를 이용하면 기본 자료형을 객체 자료형으로 만듬 <br/>
  ex) new Number(), new Boolean(), new String() <br/>
  속성과 메서드 추가 가능 <br/>
  기본 자료형으로 연산하는 것도 모두 가능
- 기본 자료형의 승급 <br/>
  기존에 존재하는 속성과 메서드는?? <br/>
  => 기본 자료형도 뒤에 .을 찍고 속성과 메서드를 쓰면 <br/>
  일시적으로 객체 자료형으로 변경해서 속성과 메서드 사용 가능

### _객체 자료형_

- 스택과 힙 연결해서 활용 (속성과 메서드 가짐)
- 함수
- 배열
- 객체
- 속성과 메서드 가질 수 있음 (추가 가능)

### _프로토타입_

- 일시적으로 입게 되는 옷 느낌 <br/>
  ex) String.prototype.value = 10
- 기본 자료형에 추가적으로 속성/메서드 집어 넣고 싶을 때 활용 가능
- 객체와 객체 공유 모델
- 클래스의 등장으로 프로토타입 중요성 낮아짐
- 어떤 문자열 내부에 어떤 문자열이 포함 되어 있는지 확인 메서드 <br/>
  메서드는 내부에서 this를 활용하므로 익명 함수로 만들어야 함

```html
<script>
  String.prototype.contain = function (다른문자열) {
    return this.indexOf(다른문자열) >= 0;
  };

  const a = '문자열';
  a.contain('문');
</script>
```

큰 프로젝트에서 일일이 문자열.indexOf(다른문자열) >= 0 사용하면 귀찮음 <br/>
=> 한번만 프로토타입에 정의해주면 간단하게 사용 가능 (+ 의미 명확) <br/>
=> 협업 시 활용하기에는 안 좋을 수 있음

#

## [다양한 메서드 맛보기]

### _Number 객체_

- toFixed(n) 메서드; 소수점 n번째 자리까지 자를 수 있음 <br/>
  문자열 자료형으로 나옴
- Number.isNaN() 메서드; 매개변수에 NaN 오면 true return
- Number.isFinite() 메서드; 유한하면 true return <br/>
  cf) 10 / 0 => Infinity, typeof(Infinity) => "number"

### _String 객체_

- trim() 메서드; 앞 뒤 공백 제거
- split() 메서드; separator (구분자) 기준으로 잘라서 list로 만듬 <br/>
  cf. input.trim().split('\n').map((line) => line.split(','))) // 2차원 배열

### _Math 객체_

- Math.E (자연 상수 값), Math.PI (PI 값), ...
- Math.floor(); 내림, Math.ceil(); 올림, Math.round(); 반올림
- Math.min(); 최솟값, Math.max(); 최댓값 <br/>
  매개값으로 배열을 넣을 경우에는 전개 연산자 활용 <br/>
  ex) Math.min(...[52, 273, 104])
- Math.random(); 0.0 이상 1.0 미만 난수 생성 <br/>
  ex) 0~50 사이 랜덤 정수 => Math.floor(Math.random() \* 50)

#

## [6.2절 마무리]

### _파일 분리 방법_

```html
<head>
  <!-- 한글 꺠지지 않도록 하는 메타 태그 -->
  <meta charset="utf-8" />

  <!-- 파일 분리 방법 -->
  <script src="파일경로"></script>
</head>
```

### _외부 라이브러리 로드_

- 파일로 사용하는 방법
  - 다운로드하여 저장 후, src 경로 지정
- CDN 링크 사용 방법
  - 링크 복사하여 src 경로 지정

#

## [객체의 기본 속성 지정하기]

### _객체 기본값 지정_

- 매개값으로 객체를 넘김 (가독성 위함 + 디버그 용이)
- 객체 기본 매개변수 지정 방법 (5가지) <br/>
  (과거2, 과거3은 빈문자열/0과 같이 false로 변환되는 값이 오지 않을 것이라는 것이 확실해야함!)

  - 과거 1) object.status = object.status !== undefined ? object.status : '이상 없음'
  - 과거 2) object.status = object.status ? object.status : '이상 없음'
  - 과거 3) object.status = object.status || '이상 없음'

  - 현대 1) object = { status: '이상 없음', ...object }
  - 현대 2) fun = function ({name, age, color, status = '이상 없음'}) {
    return
    }

```html
<script>
  const test = function ({ name, age, color, status = '이상 없음' }) {
    return `${name} : ${age} : ${color} : ${status}`;
  };

  console.log(
    test({
      name: '구름',
      age: 7,
      color: '갈색',
    })
  );
</script>
```

```html
<script>
  const test = function (object) {
    const { name, age, color, status } = { status: '이상 없음', ...object };

    return `${name} : ${age} : ${color} : ${status}`;
  };

  console.log(
    test({
      name: '구름',
      age: 7,
      color: '갈색',
    })
  );
</script>
```

#

### [Note]

- JS; 메서드도 속성에 포함됨, 함수 자료형의 속성
- this 바인딩: this를 현재 객체와 연결하는 행위
- 익명 함수; this 바인딩 OK <br/>
  화살표 함수; this 바인딩 X
- 객체 내부의 속성이 정의되지 않으면 undefined 출력
- 조건부 연산자: ?
- 전개 연산자: ...
- delete; 키워드 연산자
- 객체는 힙 영역에 올라감
- 객체의 속성 중 함수 자료형 => 메서드
- 변수를 활용해 객체 속성 접근할 시에 [] (대괄호) 사용
- 객체 표현 연습
- 배열 타입 확인; Array.isArray() 활용
- 함수 자료 확인; typeof() 이용
- JS; 함수를 객체처럼 쓰는 언어 <br/>
  => 함수를 일급 객체(first-class object)로 다룬다
- 구글 검색을 통해 메서드 찾기
- NaN (Not a Number) 자료형; 자료형은 숫자인데 값이 숫자가 아닌 것 <br/>
  ex) Number('안녕') => NaN
- is로 시작하는 메서드는 true or false return
- 다른 개발자가 미리 만들어 놓은 유틸리티 함수/메서드 모음 => 라이브러리
- Lodash 라이브러리 (\_ 이름의 객체); 여러 유틸리티 함수 제공 <br/>
  \_.sortBy(collection, [iterates])
- 시간 유틸리티 라이브러리; Luxon <br/>
  엑셀 스프레드시트; Handson <br/>
  데이터 시각화; d3js, chartjs, threejs
- Math.sin(90) (X) <br/>
  => sin 매개값으로는 라디안 값을 넣어야 함
- asc; 오름차순 정렬, desc; 내림차순 정렬

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=QtDrQ1JMjZM&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=34)
[Reference2](https://www.youtube.com/watch?v=vEG4DY-TlC8&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=35)
[Reference3](https://www.youtube.com/watch?v=8s-GikglO0U&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=36)
[Reference4](https://www.youtube.com/watch?v=LHMoCluD3K8&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=37)
[Reference5](https://www.youtube.com/watch?v=PMGZE_eNJag&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=38)
[Reference6](https://www.youtube.com/watch?v=l4lbRpFPN4A&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=39)
