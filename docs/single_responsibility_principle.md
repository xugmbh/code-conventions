## Single Responsibility Principle (SRP)

The single responsibility principle (SRP) is a concept that any single object in object-oriented programm ing (OOP) should be made for one specific function.

<small style="color: red">Press down to see examples.</small>



### Bad practice:


```ts
class BadUserService {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  saveUser() {
    // Save user data to the database
    console.log(`Saving user: ${this.name}`);
    // ...
  }

  sendNotification(message) {
    // the whole implementation here.
    console.log(`Sending notification to ${this.email}: ${message}`);
  }
}
```



## Good practice:

```ts
class GoodUser {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  saveUser() {
    // Save user data to the database
    console.log(`Saving user: ${this.name}`);
    // ...
  }
}

class NotificationService {
  sendNotification(user, message) {
    // Send a notification to the user
    console.log(`Sending notification to ${user.email}: ${message}`);
    // ...
  }
}
```