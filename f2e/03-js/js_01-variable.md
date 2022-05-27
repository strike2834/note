# 儲存資料

## 變數

- case senstive
- 首字符可為任意 unicode 或 `$`、`_`
- 第二字符之後除任意 unicode 或 `$`、`_` 之外，還可為 `0-9`
- 保留字不可用為變數名稱

## 宣告

- `var` 函式作用域
- `let` 區塊作用域，不可重複宣告
- `const` 區塊作用域，不可重複宣告、不可再次賦值

### 變數提升（Hosting）

JavaScript 引擎在解析原始碼時，會先將所有已宣告的變數提升到程式碼的頂部，綁定其所屬作用域但不賦值。

```javascript
console.log(a); // 顯示 undefined
var a = 1;
```

因此上述例子的 `a` 並未宣告與賦值，但會提昇至頂部並進行初始化成 `undefined`，故在執行上不會報錯。

而使用 `let` 與 `const` 宣告的變數則不會初始化，在賦值前的 Temporal Dead Zone 取值則會發生錯誤。

## 命名

- 易於理解的內容名稱
- 不過長或過短
- 不使用容易混淆的名稱
- 開頭使用 `_` 表示具有特殊意義，非必要不使用
- 統一命名風格
- 只使用英文命名
- 習慣用法如下：<br>
  ├ 變數／函式名稱：camelCase<br>
  ├ 類別名稱：PascalCase<br>
  └ 常數：全大寫，字詞間用下底線 `_`

```javascript
let numberOfStudents
const numberOfLegs
function setBackgroundColor()
class Student{}
```

## 資料型別

程式語言裡常見的型別有「動態型別」與「靜態型別」，「靜態型別」語言的變數，於**編譯時**已經確定其型別，<br>
JavaScript 所屬的動態型別，則是於**執行階段變數賦值後**才會擁有型別。

Javascript 內建有七大型別：

| 型別        | 例值                     | 說明                                                                   |
| ----------- | ------------------------ | ---------------------------------------------------------------------- |
| `Null`      | `null`                   | 值為空或不存在                                                         |
| `Undefined` | `undefined`              | 初始值或未定義值                                                       |
| `Boolean`   | `true`、`false`          | 布林值                                                                 |
| `Number`    | 整數 `1` 或浮點數 `3.14` | 儲存根據 IEE 754-2008 標準定義，於 `(2^53 -1)` 到 `2^53 -1` 之間的數字 |

- `Number` 另有三個符號值： `+Infinity` 、 `-Infinity` 、 `NaN` （Not a Number）
- 可以透過 `Number.MAX_VALUE` 或 `Number.MIN_VALUE` 兩個常數，<br />
  以及在 ES6 新增的 `Number.isSafeInteger()` 、 `Number.MAX_SAFE_INTEGER` 、 `Number.MIN_SAFE_INTEGER` 等函式來檢查數字是否位於標準範圍之內

| 型別     | 例值          | 說明                                                      |
| -------- | ------------- | --------------------------------------------------------- |
| `String` | `Hello World` | 文字，以單括號 `'` 或雙括號 `"` 包覆起來的字元            |
| `Object` |               | 資料或函式的組合                                          |
| `Symbol` |               | 此類型的值唯一且不可修改，通常用於做為 Object 的 Key 使用 |

- `Object` 由 `{鍵 (Key) : 值 (Value)}` 或 `new Object()` 宣告
- 透過 `.Key` 或 `['Key']` 存取或操作 `Object` 裡的 property，刪除則需使用 `delete`
- 除了上述三種內建資料型別（ `Boolean` 、 `Number` 、 `String` ）也是 `Object` 之外，<br />
  一些特殊的資料型別例如 `Array` 、 `Date` 、 `Function` 、 `RegExp` 也都屬於 `Object`

### BigInt

- 另外 Chrome 67 有新增 `BigInt`，可儲存超過 `Number` 範圍的值
- 於數值後面加上 `n` 或使用 `BigInt()` 函式轉型即可
  - 例如 `const bigInt = 123456789012345678901234567890n;`
- `Number` 常見的運算子操作都可同樣套用於 `BigInt` 上，但 `BigInt` 類型的值不可與 `Number` 類型的值進行操作，會造成 `TypeError` 錯誤

### `typeof` 運算子

`typeof` 是能檢視一個值型別的運算子。

```javascript
var a;
typeof a; // "undefined"

a = null;
typeof a; // "object"

a = undefined;
typeof a; // "undefined"

a = "string";
typeof a; // "string"

a = 5;
typeof a; // "number"

a = true;
typeof a; // "boolean"

a = { a: 5 };
typeof a; // "object"

a = Symble();
typeof a; // "symble"
```

但是 `typeof a` 並非詢問 `a` 變數的型別，而是詢問「目前在 `a` 中的值的型別是什麼」。JavaScript 的變數單純只是值的容器。

`null` 的類型是 `object`，這是由於歷史原因造成的。1995 年的 JavaScript 語言第一版，只設計了五種資料類型（物件、整數、浮點數、字串和布林值），沒考慮 `null`，只把它當作 `object` 的一種特殊值。後來 `null` 獨立出來，作為一種單獨的資料類型，為了兼容以前的代碼，`typeof null` 傳回 `object` 就沒法改變了，所以是一個萬年 Bug。

我們可以利用 `null` 會被 `typeof` 檢測為 `object` 並且會轉為 `false` 的結果來驗證值是否為 `null。`

```javascript
var a = null;

if (!a && typeof a === "object") {
  console.log("null");
}
```
