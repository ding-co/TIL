## [클래스 속성]

### _클래스 기본 복습_

```html
<script>
  // 정사각형을 나타내는 객체
  class Square {
    constructor(length) {
      this.length = length;
    }
    getArea() {
      return this.length * this.length;
    }
    getPerimeter() {
      return 4 * this.length;
    }
  }

  const square = new Square(10);
  console.log(square.getArea());
  console.log(square.getPerimeter());
</script>
```

### _private 속성 배경_

```html
<script>
  // 정사각형을 나타내는 객체
  class Square {
    constructor(length) {
      if (length < 0) {
        throw '길이는 0 이상이어야 합니다.';
      }
      this._length = length;
    }
    getArea() {
      return this._length * this._length;
    }
    getPerimeter() {
      return 4 * this._length;
    }
  }

  const square = new Square(10);
  console.log(square.getArea());
  console.log(square.getPerimeter());

  square.length = -10;
  console.log(square.getArea());
  console.log(square.getPerimeter());
</script>
```

### _private 속성 만들기_

```html
<script>
  // 정사각형을 나타내는 객체
  class Square {
    // private 속성: 클래스 내부에서만 접근 가능한 속성
    #length;

    constructor(length) {
      if (length < 0) {
        throw '길이는 0 이상이어야 합니다.';
      }
      this.#length = length;
    }
    getArea() {
      return this.#length * this.#length;
    }
    getPerimeter() {
      return 4 * this.#length;
    }
  }

  const square = new Square(10);
  console.log(square.getArea());
  console.log(square.getPerimeter());

  square.#length = -10;
  console.log(square.getArea());
  console.log(square.getPerimeter());
</script>
```

### _Getter & Setter_

```html
<script>
  // 정사각형을 나타내는 객체
  class Square {
    // private 속성: 클래스 내부에서만 접근 가능한 속성
    #length;

    constructor(length) {
      if (length < 0) {
        throw '길이는 0 이상이어야 합니다.';
      }
      this.#length = length;
    }
    getArea() {
      return this.#length * this.#length;
    }
    getPerimeter() {
      return 4 * this.#length;
    }
    setLength(length) {
      if (length < 0) {
        throw '길이는 0 이상이어야 합니다.';
      }
      this.#length = length;
    }
    getLength() {
      return this.#length;
    }
  }

  const square = new Square(10);
  console.log(square.getArea());
  console.log(square.getPerimeter());

  console.log(square.getLength());
  square.setLength(20);
  console.log(square.getLength());
</script>
```

### _Getter & Setter 속성_

- 속성은 행동이 아닌데 왜 메서드로 접근?

```html
<script>
  // 정사각형을 나타내는 객체
  class Square {
    // private 속성: 클래스 내부에서만 접근 가능한 속성
    // 클래스를 더 안전하게 사용 가능!
    #length;

    constructor(length) {
      if (length < 0) {
        throw '길이는 0 이상이어야 합니다.';
      }
      this.#length = length;
    }

    get area() {
      return this.#length * this.#length;
    }

    get perimeter() {
      return 4 * this.#length;
    }

    set length(length) {
      if (length < 0) {
        throw '길이는 0 이상이어야 합니다.';
      }
      this.#length = length;
    }

    get length() {
      return this.#length;
    }
  }

  const square = new Square(10);
  console.log(square.area);
  console.log(square.perimeter);

  console.log(square.length);
  square.length = 20;
  console.log(square.length);
</script>
```

## [static 속성과 메서드]

- static 속성과 매서드 개요

```html
<script>
  // 만들어진 Square 객체의 개수를 알고 싶을 때
  class Square {
    static count = 0;
    static test() {}

    constructor(length) {
      Square.count += 1;
    }
  }

  console.log(Square.count);
  new Square();
  new Square();
  new Square();
  console.log(Square.count);
</script>
```

- private 메서드

```html
<script>
  // private 메서드
  class Square {
    #a;

    #test() {
      console.log('private test() 메서드입니다.');
    }

    constructor() {
      this.#test();
    }
  }

  new Square();
</script>
```

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=0e0mmWZUTcY&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=61)
[Reference2](https://www.youtube.com/watch?v=A3_F05OclV4&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=62)
