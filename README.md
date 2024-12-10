<div align="center">
  <img height="60" src="https://img.icons8.com/color/344/javascript.png">
  <h1>JavaScript Savollari</h1>
</div>
<p align="center"> Oddiydan murakkabgacha: JavaScript bo‘yicha qanchalik yaxshi bilimga ega ekanligingizni tekshirib ko‘ring, bilimlaringizni bir oz yangilang yoki kodlash bo‘yicha intervyularga tayyorlaning!<br> Ushbu repoda muntazam ravishda yangi savollar qo'shib boraman.<br/> Bu faqat qiziqarli maqsadlar uchun, omad tilayman!</p>


---

###### 1. Natija qanday chiqadi

```javascript
function sayHi() {
  console.log(name);
  console.log(age);
  var name = 'Aziz';
  let age = 22;
}

sayHi();
```

- A: `Aziz` and `undefined`
- B: `Aziz` and `ReferenceError`
- C: `ReferenceError` and `22`
- D: `undefined` and `ReferenceError`

<details><summary><b>Javob</b></summary>
<p>

#### Javob: D

Within the function, we first declare the `name` variable with the `var` keyword. This means that the variable gets hoisted (memory space is set up during the creation phase) with the default value of `undefined`, until we actually get to the line where we define the variable. We haven't defined the variable yet on the line where we try to log the `name` variable, so it still holds the value of `undefined`.

Variables with the `let` keyword (and `const`) are hoisted, but unlike `var`, don't get <i>initialized</i>. They are not accessible before the line we declare (initialize) them. This is called the "temporal dead zone". When we try to access the variables before they are declared, JavaScript throws a `ReferenceError`.

</p>
</details>

---

###### 2. Natija qanday chiqadi

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
```

- A: `0 1 2` and `0 1 2`
- B: `0 1 2` and `3 3 3`
- C: `3 3 3` and `0 1 2`

<details><summary><b>Javob</b></summary>
<p>

#### Javob: C

Because of the event queue in JavaScript, the `setTimeout` callback function is called _after_ the loop has been executed. Since the variable `i` in the first loop was declared using the `var` keyword, this value was global. During the loop, we incremented the value of `i` by `1` each time, using the unary operator `++`. By the time the `setTimeout` callback function was invoked, `i` was equal to `3` in the first example.

In the second loop, the variable `i` was declared using the `let` keyword: variables declared with the `let` (and `const`) keyword are block-scoped (a block is anything between `{ }`). During each iteration, `i` will have a new value, and each value is scoped inside the loop.

</p>
</details>

---

###### 3. Natija qanday chiqadi

```javascript
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius,
};

console.log(shape.diameter());
console.log(shape.perimeter());
```

- A: `20` and `62.83185307179586`
- B: `20` and `NaN`
- C: `20` and `63`
- D: `NaN` and `63`

<details><summary><b>Javob</b></summary>
<p>

#### Javob: B

Note that the value of `diameter` is a regular function, whereas the value of `perimeter` is an arrow function.

With arrow functions, the `this` keyword refers to its current surrounding scope, unlike regular functions! This means that when we call `perimeter`, it doesn't refer to the shape object, but to its surrounding scope (window for example).

Since there is no value `radius` in the scope of the arrow function, `this.radius` returns `undefined` which, when multiplied by `2 * Math.PI`, results in `NaN`.

</p>
</details>

---

###### 4. Natija qanday chiqadi

```javascript
+true;
!'Aziz';
```

- A: `1` and `false`
- B: `false` and `NaN`
- C: `false` and `false`

<details><summary><b>Javob</b></summary>
<p>

#### Javob: A

The unary plus tries to convert an operand to a number. `true` is `1`, and `false` is `0`.

The string `'Aziz'` is a truthy value. What we're actually asking, is "Is this truthy value falsy?". This returns `false`.

</p>
</details>

---

###### 5. Qaysi biri to‘g‘ri?

```javascript
const bird = {
  size: 'small',
};

const mouse = {
  name: 'Mickey',
  small: true,
};
```

- A: `mouse.bird.size` is not valid
- B: `mouse[bird.size]` is not valid
- C: `mouse[bird["size"]]` is not valid
- D: All of them are valid

<details><summary><b>Javob</b></summary>
<p>

#### Javob: A

In JavaScript, all object keys are strings (unless it's a Symbol). Even though we might not _type_ them as strings, they are always converted into strings under the hood.

JavaScript interprets (or unboxes) statements. When we use bracket notation, it sees the first opening bracket `[` and keeps going until it finds the closing bracket `]`. Only then, it will evaluate the statement.

`mouse[bird.size]`: First it evaluates `bird.size`, which is `"small"`. `mouse["small"]` returns `true`

However, with dot notation, this doesn't happen. `mouse` does not have a key called `bird`, which means that `mouse.bird` is `undefined`. Then, we ask for the `size` using dot notation: `mouse.bird.size`. Since `mouse.bird` is `undefined`, we're actually asking `undefined.size`. This isn't valid, and will throw an error similar to `Cannot read property "size" of undefined`.

</p>
</details>

---

###### 6. Natija qanday chiqadi

```javascript
let c = { greeting: 'Hey!' };
let d;

d = c;
c.greeting = 'Hello';
console.log(d.greeting);
```

- A: `Hello`
- B: `Hey!`
- C: `undefined`
- D: `ReferenceError`
- E: `TypeError`

<details><summary><b>Javob</b></summary>
<p>

#### Javob: A

In JavaScript, all objects interact by _reference_ when setting them equal to each other.

First, variable `c` holds a value to an object. Later, we assign `d` with the same reference that `c` has to the object.

<img src="https://i.imgur.com/ko5k0fs.png" width="200">

When you change one object, you change all of them.

</p>
</details>

---

###### 7. Natija qanday chiqadi

```javascript
let a = 3;
let b = new Number(3);
let c = 3;

console.log(a == b);
console.log(a === b);
console.log(b === c);
```

- A: `true` `false` `true`
- B: `false` `false` `true`
- C: `true` `false` `false`
- D: `false` `true` `true`

<details><summary><b>Javob</b></summary>
<p>

#### Javob: C

`new Number()` is a built-in function constructor. Although it looks like a number, it's not really a number: it has a bunch of extra features and is an object.

When we use the `==` operator (Equality operator), it only checks whether it has the same _value_. They both have the value of `3`, so it returns `true`.

However, when we use the `===` operator (Strict equality operator), both value _and_ type should be the same. It's not: `new Number()` is not a number, it's an **object**. Both return `false.`

</p>
</details>

---

###### 8. Natija qanday chiqadi

```javascript
class Chameleon {
  static colorChange(newColor) {
    this.newColor = newColor;
    return this.newColor;
  }

  constructor({ newColor = 'green' } = {}) {
    this.newColor = newColor;
  }
}

const freddie = new Chameleon({ newColor: 'purple' });
console.log(freddie.colorChange('orange'));
```

- A: `orange`
- B: `purple`
- C: `green`
- D: `TypeError`

<details><summary><b>Javob</b></summary>
<p>

#### Javob: D

The `colorChange` function is static. Static methods are designed to live only on the constructor in which they are created, and cannot be passed down to any children or called upon class instances. Since `freddie` is an instance of class Chameleon, the function cannot be called upon it. A `TypeError` is thrown.

</p>
</details>

---

###### 9. Natija qanday chiqadi

```javascript
let greeting;
greetign = {}; // Typo!
console.log(greetign);
```

- A: `{}`
- B: `ReferenceError: greetign is not defined`
- C: `undefined`

<details><summary><b>Javob</b></summary>
<p>

#### Javob: A

It logs the object, because we just created an empty object on the global object! When we mistyped `greeting` as `greetign`, the JS interpreter actually saw this as:

1. `global.greetign = {}` in Node.js
2. `window.greetign = {}`, `frames.greetign = {}` and `self.greetign` in browsers.
3. `self.greetign` in web workers.
4. `globalThis.greetign` in all environments.

In order to avoid this, we can use `"use strict"`. This makes sure that you have declared a variable before setting it equal to anything.

</p>
</details>

---
