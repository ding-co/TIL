## [상속 기본 문법]

```html
<script>
  class Rectangle {
    constructor(width, height) {
      this.width = width;
      this.height = height;
    }

    getArea() {
      return this.width * this.height;
    }

    getPerimeter() {
      return 2 * (this.width + this.height);
    }
  }

  class Square {
    constructor(width) {
      this.width = width;
    }

    getArea() {
      return this.width * this.width;
    }

    getPerimeter() {
      return 4 * this.width;
    }
  }

  const rect = new Rectangle(20, 10);
  console.log(`넓이: ${rect.getArea()}`);
  console.log(`둘레: ${rect.getPerimeter()}`);

  // 상속 배경: 비슷한 클래스 계속 만드는 것은 코드 낭비, 유지 보수 힘듦
  const square = new Square(10);
  console.log(`넓이: ${square.getArea()}`);
  console.log(`둘레: ${square.getPerimeter()}`);
</script>
```

```html
<script>
  // 상속 문법 (한 클래스의 모든 기능 -> 다른 클래스에게 상속)
  // Rectangle (주는 클래스, 부모/슈퍼 클래스)
  // Square (받는 클래스, 자식/서브 클래스)
  class Square extends Rectangle {
    constructor(width) {
      // 생성자 추가적으로 정의할 때 앞에서 호출
      // super (부모 생성자)
      super(width, width);
    }
  }

  const square = new Square(10);
  console.log(`넓이: ${square.getArea()}`);
  console.log(`둘레: ${square.getPerimeter()}`);
</script>
```

#

### [Note]

- 코드의 재사용을 쉽게 해주는 기능 => 상속

#

### [Reference]

[Reference1](https://www.youtube.com/watch?v=1n8pyohAFj0&list=PLBXuLgInP-5kxpAKy2DNXoebCse2grHjl&index=63)
