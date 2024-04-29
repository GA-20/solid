# Dependency Inversion Principle

The Dependency Inversion Principle (DIP) states that high-level modules should not depend on low-level modules, but both should depend on abstractions. Abstractions should not depend on details – details should depend on abstractions.

This principle aims to reduce coupling between modules, increase modularity, and make the code easier to maintain, test, and extend.

## Example

```ts
// Bad Example

class Light {
  turnOn() {
    console.log("Light turned on");
  }

  turnOff() {
    console.log("Light turned off");
  }
}

class Switch {
  private light: Light;

  constructor() {
    this.light = new Light();
  }

  toggle() {
    if (this.light) {
      this.light.turnOff();
      this.light = null;
    } else {
      this.light = new Light();
      this.light.turnOn();
    }
  }
}
```

In the example above, the `Switch` class directly depends on the `Light` class, which makes it hard to test and extend. If we want to add a new type of light, we would have to modify the `Switch` class.

A better approach would be to introduce an abstraction between the `Switch` and `Light` classes:

```ts
// Good Example

interface Switchable {
  turnOn(): void;
  turnOff(): void;
}

class Light implements Switchable {
  turnOn() {
    console.log("Light turned on");
  }

  turnOff() {
    console.log("Light turned off");
  }
}

class CeilingFan implements Switchable {
  turnOn() {
    console.log("Ceiling fan turned on");
  }

  turnOff() {
    console.log("Ceiling fan turned off");
  }
}

class Switch {
  private switchable: Switchable;

  constructor(switchable: Switchable) {
    this.switchable = switchable;
  }

  toggle() {
    if (this.switchable) {
      this.switchable.turnOff();
      this.switchable = null;
    } else {
      this.switchable = new Light();
      this.switchable.turnOn();
    }
  }
}

const lightSwitch = new Switch(new Light());
lightSwitch.toggle();

const fanSwitch = new Switch(new CeilingFan());
fanSwitch.toggle();
```

In the example above, the `Switch` class depends on the `Switchable` interface, which allows us to decouple the `Switch` class from the `Light` class. Now, we can easily add new types of lights without modifying the `Switch` class.
