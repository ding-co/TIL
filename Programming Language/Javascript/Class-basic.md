## [클래스 도입]

### _추상화_

- 현실에 있는 객체는 많은 속성을 가지고 있음 <br/>
  => 따라서 어떤 대상에서 나에게 필요한 것만 추출해내는 것 (추상화)
- 필요하다고 생각하는 부분만 추출

### _학생 성적 관리 프로그램_

```js
// 클래스 이전(1): 자료
const students = [
  { 이름: '구름', 국어: 87, 영어: 98, 수학: 88, 과학: 90 },
  { 이름: '별이', 국어: 92, 영어: 98, 수학: 96, 과학: 88 },
  { 이름: '겨울', 국어: 76, 영어: 96, 수학: 94, 과학: 86 },
  { 이름: '바다', 국어: 98, 영어: 52, 수학: 98, 과학: 92 },
];

// 클래스 이전(2): 연산
let output = '이름\t총점\t평균\n';
for (const student of students) {
  const 총점 = student.국어 + student.영어 + student.수학 + student.과학;
  const 평균 = 총점 / 4;
  output += `${student.이름}\t${총점}\t${평균}\n`;
}
console.log(output);

// 클래스 이전(3): 연산 -> 함수
const get총점 = (student) => {
  return student.국어 + student.영어 + student.수학 + student.과학;
};
const get평균 = (student) => {
  return get총점(student) / 4;
};

let output = '이름\t총점\t평균\n';
for (const student of students) {
  output += `${student.이름}\t${get총점(student)}점\t${get평균(student)}점\n`;
}
console.log(output);

// 클래스 이전(4): 자료 + 연산 => 객체
for (const student of students) {
  student.get총점 = function () {
    return this.국어 + this.영어 + this.수학 + this.과학;
  };
  student.get평균 = function () {
    return this.get총점() / 4;
  };
}

let output = '이름\t총점\t평균\n';
for (const student of students) {
  output += `${student.이름}\t${get총점(student.get총점())}점\t${get평균(
    student.get평균()
  )}점\n`;
}
console.log(output);
```

```js
// 동사 + 목적어 -> 명령문
// 프로그램의 규모가 복잡해지면 함수가 어떤 자료와 연결되는지 알기 힘듦
// ex) get총점()

// 주어 + 동사 + 목적어 -> 평서문
// 어떠한 자료가 어떤 함수를 적용할 수 있는지 빠르게 인지 가능
// ex) student.get총점()

// 명령문 -> 평서문
// 프로그래밍의 큰 패러다임 변화

// 클래스 이전(5): 객체 지향 프로그래밍 언어
// 객체 -> 자료 + 함수 함께 있는 것 지향
// 객체 지향 프로그래밍
```

```js
// 클래스 이전(5): 객체를 만드는 함수
// 객체 표현 부분, 객체 사용 부분 명확히 분리됨
// 속성, 메서드 한 부분에서 관리 가능 -> 유지보수성 높아짐
function createStudent(이름, 국어, 영어, 수학, 과학) {
  return {
    이름: 이름,
    국어: 국어,
    영어: 영어,
    수학: 수학,
    과학: 과학,
    get총점: function () {
      return this.국어 + this.영어 + this.수학 + this.과학;
    };
    get평균() {
      return this.get총점() / 4;
    };
  };
};

const students = [
  createStudent('구름', 87, 98, 88, 90);
  createStudent('별이', 92, 98, 96, 88);
  createStudent('겨울', 76, 96, 94, 86);
  createStudent('바다', 98, 52, 98, 92);
]

let output = '이름\t총점\t평균\n';
for (const student of students) {
  output += `${student.이름}\t${student.get총점()}점\t${student.get평균()}점\n`;
}
console.log(output);
```

```js
// 클래스 이전(6): 프로토타입과 클래스
// 효율적인 객체 지향 프로그래밍 위한 목적
// 클래스 기반 객체 지향 언어 승리... (프로토타입 입지 줄어듦..)

// 프로토타입 기반 객체 지향 언어
// 중복으로 생성되는 부분을 공유 함수로 생성해 공유 공간에 저장해서 사용

// 객체 지향 기반 -> 캡슐화, 상속 등 기능 추가
```

<br/>

## [클래스 문법 기본]

```js
class 클래스이름 {}

// 클래스이름을 활용해서 만든 객체 -> 인스턴스
const 인스턴스 = new 클래스이름();

// 클래스 정의
// 클래스 이름은 대문자로 시작하는 식별자 사용 (관례)
class Student {
  // 클래스 생성자 -> 클래스로 객체를 생성할 때 호출되는 녀석
  constructor(이름, 국어, 영어, 수학, 과학) {
    // 클래스의 속성을 만드는 부분
    // 왼쪽은 클래스의 속성, 오른쪽은 매개변수로 받은 값
    this.이름 = 이름;
    this.국어 = 국어;
    this.영어 = 영어;
    this.수학 = 수학;
    this.과학 = 과학;
  }

  // 클래스의 메서드를 만드는 부분
  getSum() {
    return this.국어 + this.영어 + this.수학 + this.과학;
  }

  getAverage() {
    return this.getSum() / 4;
  }
}

// 클래스로 객체 만들기
const students = [
  // 객체를 생성!
  new Student('구름', 87, 98, 88, 90),
  new Student('별이', 92, 98, 96, 88),
  new Student('겨울', 76, 96, 94, 86),
  new Student('바다', 98, 52, 98, 92),
];

let output = '이름\t총점\t평균\n';
for (const student of students) {
  output += `${
    student.이름
  }\t${student.getSum()}점\t${student.getAverage()}점\n`;
}
console.log(output);
```

```js
// 이유 없이 코드 확장하기 1. 학생 목록도 클래스로
// 학생을 저장하던 배열도 하나의 객체로 만들어서 활용 가능
class StudentList {
  constructor() {
    this.list = [];
  }

  add(student) {
    this.list.push(student);
  }

  printTable() {
    let output = '이름\t총점\t평균\n';
    for (const student of this.list) {
      output += `${
        student.이름
      }\t${student.getSum()}점\t${student.getAverage()}점\n`;
    }
    console.log(output);
  }
}

class Student {
  constructor(이름, 국어, 영어, 수학, 과학) {
    this.이름 = 이름;
    this.국어 = 국어;
    this.영어 = 영어;
    this.수학 = 수학;
    this.과학 = 과학;
  }

  getSum() {
    return this.국어 + this.영어 + this.수학 + this.과학;
  }

  getAverage() {
    return this.getSum() / 4;
  }
}

const students = new StudentList();
students.add(new Student('구름', 87, 98, 88, 90));
students.add(new Student('별이', 92, 98, 96, 88));
students.add(new Student('겨울', 76, 96, 94, 86));
students.add(new Student('바다', 98, 52, 98, 92));

students.printTable();
```

```js
// 이유 없이 코드 확장하기 2. 객체 매개변수
class StudentList {
  constructor() {
    this.list = [];
  }

  add(student) {
    this.list.push(student);
  }

  printTable() {
    let output = '이름\t총점\t평균\n';
    for (const student of this.list) {
      output += `${
        student.이름
      }\t${student.getSum()}점\t${student.getAverage()}점\n`;
    }
    console.log(output);
  }
}

class Student {
  constructor(이름, { 국어, 영어, 수학, 과학 }) {
    this.이름 = 이름;
    this.국어 = 국어;
    this.영어 = 영어;
    this.수학 = 수학;
    this.과학 = 과학;
  }

  getSum() {
    return this.국어 + this.영어 + this.수학 + this.과학;
  }

  getAverage() {
    return this.getSum() / 4;
  }
}

const students = new StudentList();
students.add(new Student('구름', { 국어: 87, 영어: 98, 수학: 88, 과학: 90 }));
students.add(new Student('별이', { 국어: 92, 영어: 98, 수학: 96, 과학: 88 }));
students.add(new Student('겨울', { 국어: 76, 영어: 96, 수학: 94, 과학: 86 }));
students.add(new Student('바다', { 국어: 98, 영어: 52, 수학: 98, 과학: 92 }));

students.printTable();
```

#

### [Note]

- this 키워드 활용하기 위해서는 화살표 함수는 안되고 익명 함수 형식 사용해야함!
- 클래스; 객체를 쉽게 생성할 수 있도록 도와주는 문법
- 클래스 메서드; 모든 객체가 공유해서 사용하는 함수 (공유 함수, 공유 프로시저) <br/>
  딱 한번만 만들어지므로 내부적으로 용량 공간 절약
- 클래스 상속 이용해서 코드 매우 짧아짐 (활용성 매우 높아짐)

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=DiZ4_cotA6s&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=59)
[Reference2](https://www.youtube.com/watch?v=Xdp81bN18Ls&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=60)
