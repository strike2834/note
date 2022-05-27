# 進階

## this

- `this` 是 JavaScript 的一個關鍵字
- `this` 是 function 執行時，自動生成的一個內部物件
- 隨著 function 執行場合的不同，`this` 所指向的值，也會有所不同
- 在大多數的情況下，`this` 代表的就是呼叫 function 的物件（Owner Object of the function）<br />
  亦即 function 執行時所屬的物件，而非 function 本身
- 脫離物件的 `this` 基本上沒有任何意義
- 沒有意義的 `this` 會根據**嚴格模式**以及**環境**賦予一個預設值
- 嚴格模式底下預設就是 `undefined`，非嚴格模式在瀏覽器底下預設值是 `window`
- 要看 this，就看這個函式「怎麽」被呼叫<br />
  例如 `addEventListener` 底下的 `this` 會是「觸發事件的元素」<br />
  但裡頭的 callback function 中的 `this` 會因為 Default Binding 而指向 `window`
- 可以用 `call`、`apply` 與 `bind` 指定 this 的值<br />
  或是 arrow function 強制綁定 `this`、使用一個變數儲存 `this` 當做參考值

```javascript
"use strict";
function hello(a, b) {
  console.log(this, a, b);
}

hello.call("yo", 1, 2); // 第一個參數值即為 this
hello.apply("hihihi", [1, 2]); // apply 以 Array 的方式傳進參數
// 這兩種方式皆為呼叫 function 的函式

const myHello = hello.bind("my");
myHello(); // bind 則是會回傳一個新的 function
// 並且在調用 bind 後值就不會改變了
```

- [What's THIS in JavaScript ? [上]](https://kuro.tw/posts/2017/10/12/What-is-THIS-in-JavaScript-%E4%B8%8A/)
- [淺談 JavaScript 頭號難題 this：絕對不完整，但保證好懂](https://blog.techbridge.cc/2019/02/23/javascript-this/)
- [重新認識 JavaScript: Day 20 What's "THIS" in JavaScript (鐵人精華版)](https://ithelp.ithome.com.tw/articles/10193193)

## Closure

閉包（Closure）是利用變數作用域的特性，加上一層 function 以限制儲存環境的變數值作用範圍，避免污染 global 環境，且此變數不會因為 function 執行完畢後而消失

```javascript
// without closure
var count = 0;

function counterTick() {
  return ++count;
}

console.log(counterTick()); // 1
console.log(counterTick()); // 2

// with closure
function counter() {
  var count = 0;

  function counterTick() {
    return ++count;
  }
  return counterTick;

  // also could be written as arrow function
  return () => ++count;
}

var countFunc = counter();

console.log(countFunc()); // 1
console.log(countFunc()); // 2
```

- [所有的函式都是閉包：談 JS 中的作用域與 Closure](https://blog.techbridge.cc/2018/12/08/javascript-closure/)

## Hoisting

Hoisting（提升）是指一個變數或函式在宣告前就被使用，JavaScript 就會在使用之前再進行一次宣告，而變數只會單純宣告不會給定值，因此執行結果通常會是 `undefined` ，具體上如下例

```javascript
var x = 1;

var doSomething = function (y) {
  var x; // 此行非原本撰寫的程式
  // 是由於下面使用的 x=100 裡的 x 未經宣告
  console.log(x); // 而被 JavaScript 提升至執行序的先頭
  // 概念上類似移動至此函式的最上方進行宣告
  // 因此函式內部的 console.log 會是 undefined
  x = 100;
  return x + y;
};

console.log(doSomething(50)); // 150
console.log(x); // 1
```

函式則分有存入變數及直接定義的兩種宣告方式，存入變數的函式宣告由於與變數同樣只有宣告被提升，因此會出現 `TypeError` 錯誤，直接定義的函式則會連同內容一起被提升

```javascript
square(2);

// 傳入變數式
// 執行結果會為 TypeError: square is not a function
var square = function (number) {
  return number * number;
};

// 直接定義式
// 執行結果為正常輸出
function square(number) {
  return number * number;
}
```

若有同名的定義函式和變數使用，由於函式的優先權較高，執行結果會是定義函式

`let` 和 `const` 一樣也有 Hoisting 行為，但這兩種宣告不會被初始化成 `undefined` ，並且在賦值之前就存取這兩種宣告的值時，會直接拋出錯誤

當初加入 Hoisting 設計的原因是為了達成函式相互歸遞（mutual recursion），以及避免必須以類 ML 語言的順序撰寫（avoid painful bottom-up ML-like order）

實際運作上是 JavaScript 會於執行 function 時產生一個 Execution Contexts 執行環境（同理亦有 global EC），將所有需要的資訊存在裡面，裡頭會有個對應的 Variable Object 用以存放宣告的變數、函式和傳入的變數，在執行的時候到 VO 裡頭查找，並依參數、函式和變數的順序放入其中

參數傳進 VO 時直接放入，沒有值的話會初始化為 `undefined` ；function 傳進 VO 時新增一屬性放入建立 function 完後的回傳值（可類比為指向此 function 的指標），已有同名屬性時進行覆蓋；變數傳進 VO 時新增一屬性並賦值為 `undefined` ，已有同名屬性時則不會修改該值

`let` 和 `const` 多做了一個檢查，皆是在「提升之後」和「賦值之前」的「執行期間」內（Temporal Dead Zone）被存取就會拋出錯誤，亦即 Hoisting 的原理實質上是執行時序的調動，而非程式碼的編修

- [我知道你懂 hoisting，可是你了解到多深？](https://blog.techbridge.cc/2018/11/10/javascript-hoisting/)

## 浮點數計算

- [Floating Point Math](https://0.30000000000000004.com/)

## API Mocking

- [用 API mocking 讓前端不再苦苦等待](https://drive.google.com/file/d/1OOV55pClWtNBBM7StU7wepH39-UZb0lM/view)
- [EffectiveJavaScript](https://github.com/DeepJavaScript/EffectiveJavaScript)
