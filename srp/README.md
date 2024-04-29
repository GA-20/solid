# Single Responsibility Principle

The Single Responsibility Principle (SRP) states that a class should have only one reason to change, or in other words, it should have only one responsibility.

If a class has too many responsibilities, it can become hard to understand, maintain, and modify.

Changes to one responsibility can inadvertently affect another responsibility, leading to unintended consequences and bugs. By following SRP, we can create code that is more modular, easier to understand, and less prone to errors.

```js
// Bad example
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  save() {
    // Save user to database
  }

  sendEmail() {
    // Send email to user
  }
}
```

In the example above, the `User` class has two responsibilities: saving the user to the database and sending an email to the user. This violates the SRP because the class has more than one reason to change.

```js
// Good example
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }
}

class UserRepository {
  save(user) {
    // Save user to database
  }
}

class EmailService {
  sendEmail(user) {
    // Send email to user
  }
}

const user = new User("John Doe", "john@doe");
const userRepository = new UserRepository();
const emailService = new EmailService();

userRepository.save(user);
emailService.sendEmail(user);
```
