# Interface Segregation Principle

The Interface Segregation Principle (ISP) focuses on designing interfaces that are specific to their client's needs. It states that no client should be forced to depend on methods it does not use.

The principle suggests that instead of creating a large interface that covers all the possible methods, it's better to create smaller, more focused interfaces for specific use cases. This approach results in interfaces that are more cohesive and less coupled.

## Example

```ts
// Bad Example

interface Worker {
  work(): void;
  eat(): void;
  sleep(): void;
}

class Human implements Worker {
  work() {
    console.log('Working...');
  }

  eat() {
    console.log('Eating...');
  }

  sleep() {
    console.log('Sleeping...');
  }
}

class Robot implements Worker {
  work() {
    console.log('Working...');
  }

  eat() {
    // Do nothing
  }

  sleep() {
    // Do nothing
  }
}
```

In the example above, the `Worker` interface contains methods that are not relevant to all the classes that implement it. The `Robot` class, for example, does not need the `eat` and `sleep` methods.

A better approach would be to create separate interfaces for each type of worker:

```ts
// Good Example

interface Workable {
  work(): void;
}

interface Feedable {
  eat(): void;
}

interface Sleepable {
  sleep(): void;
}

class Human implements Workable, Feedable, Sleepable {
  work() {
    console.log('Working...');
  }

  eat() {
    console.log('Eating...');
  }

  sleep() {
    console.log('Sleeping...');
  }
}

class Robot implements Workable {
  work() {
    console.log('Working...');
  }
}
```


