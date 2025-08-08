# 📘 JavaScript & Node.js Interview Prep Guide

---

## 📂 DATA STRUCTURES

### 🔹 General Concepts

* What are different data structures?
* Explain linked list and how to insert/delete a node from it?
* Suppose there are 5 elements in singly linked list, and you only have a reference to the 3rd element. How will you delete it?
* How to implement stack using queues?

### 🔹 Stack Use Cases

* Undo/Redo in text editors
* Compiler's syntax checks
* Arithmetic expression evaluation
* Backtracking algorithms
* Reversing a word

### 🔹 Queue Use Cases

* CPU and Disk scheduling
* Printer queues
* Asynchronous data transfer
* Real-life queues (e.g. ticket counters)

---

## 🎨 DESIGN PATTERNS

### 🔹 Basics

* What is a design pattern?
* Types of design patterns: Creational, Structural, Behavioral
* Examples of design patterns you've encountered

🔗 Reference: [https://sourcemaking.com/design\_patterns](https://sourcemaking.com/design_patterns)

---

## 💻 JAVASCRIPT CONCEPTS

### 🔹 `this` Keyword

```js
function test() {
  console.log(this);
}
test();
```

1. Output in strict mode?
2. Output without strict mode?

```js
const object = {
  message: 'Hello, World!',
  getMessage() {
    const message = 'Hello, Earth!';
    return this.message;
  }
};
console.log(object.getMessage());
```

### 🔹 Arrow Functions vs Regular

```js
const object = {
  who: 'World',
  greet() { return `Hello, ${this.who}!`; },
  farewell: () => `Goodbye, ${this.who}!`
};
console.log(object.greet());
console.log(object.farewell());
```

🔗 Reference: [https://dmitripavlutin.com/javascript-this-interview-questions/](https://dmitripavlutin.com/javascript-this-interview-questions/)

### 🔹 call, apply, bind

```js
var james = {
  name: "James Smith",
  hello: function(thing) {
    console.log(this.name + " says hello " + thing);
  }
}
var steven = { name: "Steven Smith" };
james.hello("world");
steven.hello("world"); // will throw
```

### 🔹 Object Handling

* Ways to create objects
* Object.create vs Object.assign
* Shallow copy vs Deep copy

```js
var baseObject = { value : "car" };
var assignObject = Object.assign({}, baseObject);
var createObject = Object.create(baseObject);
```

### 🔹 Types in JavaScript

* Primitive: String, Number, Boolean, Null, Undefined, Symbol
* Non-Primitive: Object, Array, Function
* Operators: for...in vs for...of
* filter vs map vs forEach
* Object.keys / Object.values
* Prototypal inheritance
* `==` vs `===`

### 🔹 Function Concepts

* Function types
* Currying
* Higher-order functions
* First-class functions

---

## 🔒 CLOSURES, SCOPE & HOISTING

### 🔹 Closures

```js
function closure() {
  let counted = 0;
  return {
    count: function () { counted++; },
    getTheCount: function () { return "Counted till " + counted; }
  };
}
```

### 🔹 Hoisting

```js
var a = 1;
function b() {
  a = 10;
  function a() {}
}
b();
console.log(a);
```

---

## ⚙️ ARCHITECTURE & EVENT LOOP

### 🔹 Event Loop Basics

* Event loop phases
* Timers vs setImmediate vs process.nextTick
* Thread pool size (default is 4)
* Use of `cluster` module

🔗 Docs: [https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/)

### 🔹 Example:

```js
setTimeout(() => {
  console.log('timeout');
}, 0);

setImmediate(() => {
  console.log('immediate');
});
```

---

## 🐞 DEBUGGING

* How to debug Node.js (e.g., `node inspect`, `console.log`, VSCode debugger)
* How to approach failing APIs
* Debugging production issues

---

## 📦 NPM & DEPENDENCY MANAGEMENT

### 🔹 Basics

* What is NPM?
* `npm ci` vs `npm install`
* Publishing a package
* Module resolution algorithm

### 🔹 Files

* `package.json`: metadata + dependency ranges
* `package-lock.json`: exact versions

### 🔹 Commands

* `npm install` vs `npm i --production`
* `npm i <pkg>@version`
* `^` = minor updates, `~` = patch updates
* Versioning: MAJOR.MINOR.PATCH

---

## 🔐 AUTHENTICATION & AUTHORIZATION

### 🔹 Concepts

* Authentication vs Authorization
* Auth Methods: Session, Token, OAuth2
* JWT (Header.Payload.Signature)

```js
jwt.sign(payload, secret, options);
jwt.verify(token, secret);
```

### 🔹 Logout with JWT

* Option 1: Expire tokens via DB blacklist
* Option 2: Reduce token lifespan + use refresh tokens
