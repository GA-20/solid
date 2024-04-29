# Liskov Substitution Principle

The Liskov Substitution Principle (LSP) states that any instance of a derived class should be substitutable for an instance of its base class without affecting the correctness of the program.

In other words, a derived class should behave like its base class in all contexts. In more simple terms, if class A is a subtype of class B, you should be able to replace B with A without breaking the behavior of your program.

The importance of the LSP lies in its ability to ensure that the behavior of a program remains consistent and predictable when substituting objects of different classes. Violating the LSP can lead to unexpected behavior, bugs, and maintainability issues.

## Example

```js
// Bad example
class Vehicle {
  startEngine() {
    // Start the engine
  }
}
class ElectricCar extends Car {
  startEngine() {
    throw new Error("Electric cars don't have engines");
  }
}

const car = new ElectricCar();
car.startEngine(); // Error: Electric cars don't have engines
```

```js
// Good example
class Vehicle {
  startEngine() {
    // Start the engine
  }
}

class Car extends Vehicle {
  startEngine() {
    // Start the engine of the car
  }
}
```
