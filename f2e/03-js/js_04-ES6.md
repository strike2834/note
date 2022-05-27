# ES6

- [2016 年から 2019 年までの JavaScript の全て](https://qiita.com/rana_kualu/items/6bcc99226be741348c34)

## 1. Default Parameters

更快速的 function 參數給定預設值：

```javascript
var link = function (height = 50, color = "red", url = "https://example.com") {
  // ...
};
```

## 2. Template Literals

允許透過語法 `${val}` 將變數嵌入至字串中：

```javascript
var name = `Your name is ${first} ${last}.`;
```

## 3. Multi-line Strings

允許使用 \`（backticks）接受多行字串指定：

```javascript
var name = `first line
second line`;
```

## 4. Destructing Assignment

```javascript
object[a, b, …rest] = [1, 2, 3, 4, 5];
console.log(a);    // 1
console.log(b);    // 2
console.log(rest); // [3, 4, 5]

var o = {p: 42, q: true};
var {p, q} = o;
console.log(p); // 42
console.log(q); // true
```

## 5. Object Literals

```javascript
function getCar(make, model, value) {
 return {
   // with property value shorthand
  // syntax, you can omit the property
  // value if key matches variable
  // name
  make, // same as make: make
  model, // same as
  model: model
  value, // same as value: value
  // computed values now work with
  // object literals
  ['make' + make]: true,
  // Method definition shorthand syntax
  // omits `function` keyword & colon
  depreciate() {
    this.value -= 2500;
  }
 };
}
let car = getCar('Kia', 'Sorento', 40000);
```

## 6. Arrow Function

箭頭函式亦會更改物件裡的 this 指向行為，從原本的指向呼叫者改為指向其所屬物件

```javascript
(param1, param2, ..., paramN) => { statements }
(param1, param2, ..., paramN) => expression
// 等於 : => { return expression; }

// 只有一個參數時, 括號才能不加:
(singleParam) => { statements }
singleParam => { statements }

// 若無參數, 就一定要加括號:
() => { statements }
```

## 7. Promise

```javascript
var wait1000 = () =>
  new Promise((resolve, reject) => {
    setTimeout(resolve, 1000);
  });

wait1000()
  .then(function () {
    console.log("Yay!");
    return wait1000();
  })
  .then(function () {
    console.log("Wheeyee!");
  });
```

## 8. Let & Const, Block-Scoped

- `let` 和 `const` 的作用域從之前 `var` 的函式變成了離此變數最近的 `{}` 區塊範圍內
- `let` 不可重覆宣告，執行時會吐出錯誤
- `const` 宣告時即須初始化，並且不可修改

```javascript
function letExample(value) {
  if (value) {
    let letValue = value;
    console.log("inside block", letValue);
    // [SyntaxError] redeclaration of letValue would be a SyntaxError
    let letValue = "foo";
  }
  try {
    // [SyntaxError] Accessing letValue is a Reference Error because it
    // was defined w/in if-block
    console.log(letValue);
    // if we get here, it means that the JS engine didn't
    // throw an exception, which means that the engine
    // (or transpiled code) did not faithfully reproduce
    // how let should work
    console.log("let not faithfully handled");
  } catch (e) {
    // e is a ReferenceError
    console.log("letValue not accessible", e);
  }
}
letExample(2);
```

## 9. Classes

ES6 透過 prototype 和 function 實作出了類 inheritance 結構的 class，但仍和傳統 Java、Python 的 class 有些差別

```javascript
class Cat {
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(this.name + ' makes a noise.');
  }
}
class Lion extends Cat {
  speak() {
    super.speak();
    console.log(this.name + ' roars.);
  }
}
```

## 10. Module

```javascript
// Export
export var port = 3000;
export function getAccounts(url) {
  // ...
}

// Import
import { port, getAccounts } from "module";
console.log(port);
```
