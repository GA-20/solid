# Open-Closed Principle

It states that software entities should be open for extension but closed for modification. This means that you should be able to add new functionality to a component without having to modify its existing code.

## Example

```js
// Bad example

class Shape {
  constructor(type) {
    this.type = type;
  }

  draw() {
    if (this.type === "circle") {
      console.log("Drawing a circle");
    } else if (this.type === "square") {
      console.log("Drawing a square");
    }
  }
}

const circle = new Shape("circle");
```

```js
// Good example

class Shape {
  draw() {
    throw new Error("draw method must be implemented");
  }
}

class Circle extends Shape {
  draw() {
    console.log("Drawing a circle");
  }
}

class Square extends Shape {
  draw() {
    console.log("Drawing a square");
  }
}

const circle = new Circle();
circle.draw();

const square = new Square();
square.draw();
```
