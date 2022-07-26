# ES6

- [2016 年から 2019 年までの JavaScript の全て](https://qiita.com/rana_kualu/items/6bcc99226be741348c34)
- 1. Default Parameters
  - 更快速的給定 function 參數預設值：
  ```javascript
    var link = function (height = 50, color = "red", url = "https://example.com") {
      // ...
    };
  ```
-  2. Template Literals
  - 允許透過語法 `${val}` 將變數嵌入至字串中：
  ```javascript
    var name = `Your name is ${first} ${last}.`;
  ```
-  3. Multi-line Strings
  - 允許使用 \`（backticks）接受多行字串指定：
  ```javascript
    var name = `first line
    second line`;
  ```
- 4. Destructing Assignment
```javascript
    object[a, b, ...rest] = [1, 2, 3, 4, 5];
    console.log(a);    // 1
    console.log(b);    // 2
    console.log(rest); // [3, 4, 5]
    
    var o = {p: 42, q: true};
    var {p, q} = o;
    console.log(p); // 42
    console.log(q); // true
  ```
- 5. Object Literals
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
- 6. Arrow Function
  - 箭頭函式亦會更改物件裡的 this 指向行為，從原本的指向呼叫者改為指向其所屬物件
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
- 7. Promise
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
- 8. Let & Const, Block-Scoped
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
- 9. Classes
  - ES6 透過 prototype 和 function 實作出了類 inheritance 結構的 class
  - 仍和傳統 Java、Python 的 class 有些差別
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
- 10. Module
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

## ES2016

- [ES2016以降のJavaScriptを勉強してないと理解できない記法一覧](https://iwb.jp/javascript-es2016-to-es2022-list/)
- 1. 次方演算子(`**`)
  ```javascript
    console.log(2 ** 3) // is equal to Math.pow(2,3)
    // 8
  ```
- 2. Async function
  - 於 ES2017 新增
  ```javascript
    async function sample() {
      console.log('start')
      await new Promise(s => setTimeout(s, 3000))
      console.log('3 seconds passed after start')
    }
    
    sample()
  ```
  - 於 ES2022 起不必使用 Async function 包住也可使用 await 
  ```javascript
    console.log('start')
    await new Promise(s => setTimeout(s, 3000))
    console.log('3 seconds passed after start')
  ```
- 3. BigInt
  - JavaScript 的數值上限是 9007199254740991 (2**53 - 1, Number.MAX_SAFE_INTEGER)
  - BigInt 可以表現超越此值的數值
  - 於數值後方加上 `n` 即可
  - `const maxSafeInteger = 9007199254640991n`
- 4. Numeric Separators
  - 於 ES2021 可於數值內加入 `_` 區隔
  - 計算過後會將區隔文字除去
  - `const a = 1_000_000_000_000`
- 5. Optional Chain operator (`?.`)
  - 遇到 nullish 時不會回傳錯誤，而會改為回傳 `undefined`
  ```javascript
    const trainer = {
      name: 'Satoshi',
      partner: {
        name: 'Pikachu'
      }
    }
    console.log(trainer.monster.name)
    // Error
    console.log(trainer.monster?.name)
    // undefined
  ```
- 6. Destructing Object
  - 於 ES2018 起 Spread operator 亦可用於 Object 上
  ```javascript
    const trainer = {
      name: 'Satoshi',
      partner: {
        name: 'Pikachu'
      }
    }
    const trainerItems = {
      item1: 'monster ball',
      item2: 'bicycle',
    }
    const trainerStatus = { ...trainer, ...trainerItems }
    console.log(trainerStatus)
    /*
      {
        item1: "monster ball",
        item2: "bicycle",
        name: "Satoshi",
        partner: { name: "Pikachu" }
      }
    */
  ``` 
- 7. Null operator(`??`)
  - 左側結果為 `null` 或 `undefined` 則回傳右邊的值， 反之則回傳左邊的值
  - 由於 `||` 包含 `false`、`''`、`NaN`、`null`、`undefined` 都會回傳右邊的值，此演算子用於只想限定於 `null` 或 `undefined` 的時候
  ```javascript
    const foo = null ?? 'default'
    console.log(foo)
    // 'default'
    const bar = 0 ?? 'default'
    console.log(bar)
    // 0
  ```
- 8. Class field
  - ES2022 起變數宣言可以省略 `constructor()`
  ```javascript
    class Dog {
      // before
      constructor() {
        this.age = 5
      }
      // after
      age = 5
    }
  ```
- 9. Class private field
  - 於變數前方加上 `#` 可宣言為私有領域
  ```javascript
    class Dog {
      #age

      constructor(age) {
        this.#age = age
      }

      showAge() {
        console.log(this.#age)
      }
    }

    const dog = new Dog(7)
    dog.showAge()
    // 7

    // console.log(dog.#age)
    // Error
    // console.log(dog.age)
    // undefined
  ```
- 10. `export * as name from "./foo.js";`
  - ES2020 起可以將匯入的模組再次命名後匯出
