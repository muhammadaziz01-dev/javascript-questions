<div align="center">
  <img height="60" src="https://img.icons8.com/color/344/javascript.png">
  <h1>JavaScript Savollari</h1>
</div>
<p align="center"> Oddiydan murakkabgacha: JavaScript bo‘yicha qanchalik yaxshi bilimga ega ekanligingizni tekshirib ko‘ring, bilimlaringizni bir oz yangilang yoki kodlash bo‘yicha intervyularga tayyorlaning!<br> Ushbu repoda muntazam ravishda yangi savollar qo'shib boraman.<br/> Bu faqat qiziqarli maqsadlar uchun, omad tilayman!</p>


---

###### 1. Natija qnday chiqadi

```javascript
function sayHi() {
  console.log(name);
  console.log(age);
  var name = 'Aziz';
  let age = 22;
}

sayHi();
```

- A: `Aziz` va `undefined`
- B: `Aziz` va `ReferenceError`
- C: `ReferenceError` va `22`
- D: `undefined` va `ReferenceError`

<details><summary><b>Javob</b></summary>
<p>

#### Javob: D

Funksiya ichida name o‘zgaruvchisi `var` kalit so‘zi yordamida e'lon qilingan. `var` bilan e'lon qilingan o‘zgaruvchilar avvaldan xotirada`undefined` qiymat bilan joylashtiriladi `(hoisting)`. Shuning uchun, o‘zgaruvchiga qiymat berilguncha, uning qiymati `undefined` bo‘ladi.

`let` yoki `const` bilan e'lon qilingan o‘zgaruvchilar ham xotirada joylashtiriladi, ammo ular `temporal dead zone` (ma'lum vaqt davomida o‘zgaruvchidan foydalanib bo‘lmaydigan holat) ichida bo‘ladi. Ularni qiymat bilan boshlashdan oldin ishlatishga urinilsa, `ReferenceError` xatosi chiqadi.
</p>
</details>

---

###### 2. Natija qnday chiqadi

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
```

- A: `0 1 2` va `0 1 2`
- B: `0 1 2` va `3 3 3`
- C: `3 3 3` va `0 1 2`

<details><summary><b>Javob</b></summary>
<p>

#### Javob: C

`setTimeout` funksiyasi orqali bajariladigan kod asosiy sikldan keyin ishga tushadi. Birinchi siklda `i` o‘zgaruvchisi `var` yordamida e'lon qilingan va bu o‘zgaruvchi global bo‘ladi. Sikl tugaganda, `i` qiymati `3` bo‘ladi va hamma chaqiruvlar bir xil qiymatni ko‘rsatadi (`3`).

Ikkinchi siklda `let` ishlatilgan, bu esa o‘zgaruvchini blok doirasida cheklaydi. Har bir iteratsiya uchun yangi `i` qiymati yaratiladi, va har bir `setTimeout` o‘zining alohida qiymatini ko‘rsatadi (`0, 1, 2`).

</p>
</details>

---

###### 3. Natija qnday chiqadi

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

- A: `20` va `62.83185307179586`
- B: `20` va `NaN`
- C: `20` va `63`
- D: `NaN` va `63`

<details><summary><b>Javob</b></summary>
<p>

#### Javob: B

`diameter` oddiy funksiya bo‘lib, undagi `this` kalit so‘zi `shape` obyektini ko‘rsatadi. Natijada, `this.radius` `10` bo‘lib, `diameter()` natijasi `20` chiqadi.

`perimeter` esa arrow function bo‘lib, undagi `this` tashqi (global) doirani ko‘rsatadi. Global doirada `radius` degan o‘zgaruvchi yo‘q, shuning uchun `this.radius` qiymati `undefined`, natija esa `NaN` bo‘ladi.

</p>
</details>

---

###### 4. Natija qnday chiqadi

```javascript
+true;
!'Aziz';
```

- A: `1` va `false`
- B: `false` va `NaN`
- C: `false` va `false`

<details><summary><b>Javob</b></summary>
<p>

#### Javob: A

`+true` - bu `true` qiymatini raqamga o‘zgartiradi, va bu `1` bo‘ladi.
`!'Aziz'` - bu `Aziz` qatorini mantiqiy qiymatga o‘zgartiradi (truthy), va keyin inkor qiladi. Truthy qiymatning inkori `false`.

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

- A: `mouse.bird.size` noto‘g‘ri
- B: `mouse[bird.size]` noto‘g‘ri
- C: `mouse[bird["size"]]` noto‘g‘ri
- D: Hammasi to'gri

<details><summary><b>Javob</b></summary>
<p>

#### Javob: A

Obyektlar ichidagi kalitlar qator ko‘rinishida bo‘ladi. `mouse[bird.size]` birinchi `bird.size` qiymatini (`small`) oladi va `mouse["small"]` ga aylantiradi, natija `true`.

Lekin `mouse.bird.size ishlamaydi` , chunki `mouse` obyektida `bird` degan kalit yo‘q. Natijada `Cannot read property "size" of undefined` xatosi chiqadi.

</p>
</details>

---

###### 6. Natija qnday chiqadi

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

JavaScriptda obyektlar `reference` orqali o‘zaro bog‘lanadi. `d = c` deganda, `d` va `c` bir xil obyektga ishora qiladi. Shuning uchun, `c.greeting`ni o‘zgartirish, `d.greeting` qiymatini ham o‘zgartiradi.

<img src="https://i.imgur.com/ko5k0fs.png" width="200">

Bitta ob'ektni o'zgartirsangiz, ularning hammasini o'zgartirasiz.

</p>
</details>

---

###### 7. Natija qnday chiqadi

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

`new Number()` is a built-in function constructor. Although it looks like a number, it's not really a number: it has a bunch of extra features va is an object.

When we use the `==` operator (Equality operator), it only checks whether it has the same _value_. They both have the value of `3`, so it returns `true`.

However, when we use the `===` operator (Strict equality operator), both value _va_ type should be the same. It's not: `new Number()` is not a number, it's an **object**. Both return `false.`

</p>
</details>

---

###### 8. Natija qnday chiqadi

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

The `colorChange` function is static. Static methods are designed to live only on the constructor in which they are created, va cannot be passed down to any children or called upon class instances. Since `freddie` is an instance of class Chameleon, the function cannot be called upon it. A `TypeError` is thrown.

</p>
</details>

---

###### 9. Natija qnday chiqadi

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
2. `window.greetign = {}`, `frames.greetign = {}` va `self.greetign` in browsers.
3. `self.greetign` in web workers.
4. `globalThis.greetign` in all environments.

In order to avoid this, we can use `"use strict"`. This makes sure that you have declared a variable before setting it equal to anything.

</p>
</details>

---
