# 非同步處理

- JavaScript 是<ruby>單執行緒<rp>(</rp><rt>single-threaded</rt><rp>)</rp></ruby>的<ruby>同步<rp>(</rp><rt>synchronous</rt><rp>)</rp></ruby>程式語言
  - 在執行程式時會以最後結果中由上至下的順序去操作
  - 一次只能處理一件事
- 如果需要中途做一個不影響整體後續操作，但需要非常久時間的事情
  - JavaScript 就會直接卡死在此好一段時間（造成<ruby>阻塞<rp>(</rp><rt>blocking</rt><rp>)</rp></ruby>問題）
- 因此瀏覽器設計了<ruby>非同步<rp>(</rp><rt>asynchronous</rt><rp>)</rp></ruby>的相關處理來解決這個問題
- 非常概略性地來說，JavaScript 處理非同步的方式是：
  - 一個 `call stack` 存放**正在執行的工作**
  - 一個 `task queue`（亦稱 `callback queue`）存放**需要等待的非同步工作**
    - `task queue` 又分有 `micro task queue`（`job queue`）與 `macro task queue`（`event queue`）
    - 前者處理優先度較高的 queue（e.g. `Promise callback`），後者如 `setTimeout`
  - 以及瀏覽器所提供 `Web APIs` 專門處理 stack 中的非同步工作
    - 例如常見的 `setTimeout` 或是與 API 索取資料等等
- `Web APIs` 會將任務移動到 `task queue`，並繼續執行下一個工作
  - 當 `call stack` 裡的工作都執行完畢後，才繼續處理 `task queue` 裡的工作
  - 這個「監看 `call stack` 是否為空／執行完畢，若是，則丟 `task queue` 的工作進去」的行為稱為 `event loop`
- 優先度：`call stack`＞`micro task queue`＞`macro task queue`

```mermaid
flowchart TD
    subgraph CallStack=執行中
    CST0[非同步工作]-.->CST1
    CST1[同步工作]-.->CST2
    CST2[同步工作]
    end

    subgraph WebAPIs
    WA0[setTimeout]
    WA1[AJAX]
    WA2[Events]
    end

    subgraph TaskQueue=待執行
    TQT0[非同步工作]
    TQT1[非同步工作]-.->TQT0
    TQT2[非同步工作]-.->TQT1
    end

    CallStack=執行中--處理非同步工作-->WebAPIs
    WebAPIs--處理完後會丟到 Task Queue 去-->TaskQueue=待執行
    TQT0 --當 Call Stack 工作全部結束後才丟上去--> CallStack=執行中
```

關於 `event loop` 的詳細講解，可以觀看 Phillip Robert 在 JSConf 上解說的這支影片：

<iframe width="560" height="315" src="https://www.youtube.com/embed/8aGhZQkoFbQ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

也可以搭配由 Andrew Dillon 開發的 [JS Visualizer 9000](https://www.jsv9000.app/) 觀察可視化後的過程

- [JavaScript 中的同步與非同步（上）：先成為 callback 大師吧！](https://blog.techbridge.cc/2019/10/05/javascript-async-sync-and-callback/)
- [無痛理解 JS | 非同步怎麼運作？](https://5xruby.tw/posts/how-js-synchronous-works/)
- [\[筆記\] 理解 JavaScript 中的事件循環、堆疊、佇列和併發模式（Learn event loop, stack, queue, and concurrency mode of JavaScript in depth）](https://pjchender.blogspot.com/2017/08/javascript-learn-event-loop-stack-queue.html)
- [透過程式範例，熟悉 JS 執行流程的關鍵：Event Loop](https://www.programfarmer.com/articles/javaScript/javascript-browser-event-loop)
- [JavaScript の非同期処理をじっくり理解する (1) 実行モデルとタスクキュー](https://zenn.dev/qnighy/articles/345aa9cae02d9d)
- [JS の非同期処理を理解するために必要だった知識と学習ロードマップ](https://zenn.dev/estra/articles/js-async-programming-roadmap)
- [非同期処理:コールバック/Promise/Async Function](https://jsprimer.net/basic/async/)
- [V8 エンジンによる内部変換コードで async/await の挙動を理解する](https://zenn.dev/estra/articles/asyncawait-v8-converting)

## Callback

- `callback` 是 `Web APIs` 負責處理任務的方式裡頭一種最常見的概念
- 當有需要接在非同步處理後面做的事情
  - 例如 `setTimeout` 只有等待時間的部份是非同步、AJAX 只有取得資料的部份是非同步
- 當時間到了、資料取得了之後，接下來的行為仍然是同步的
  - 就要再寫在一個 function 裡，包在非同步的行為裡面
  - 直到相關的非同步行為結束後，再接著執行這個 function 的行為
- 這種 function 就稱為 `callback function`。

```javascript
// callback function 會包在非同步行為裡
// 當非同步部份處理完後才開始執行
function addAsync(num1, num2, callback) {
  return $.getJSON(
    "https://example.com",
    {
      num1: num1,
      num2: num2,
    },
    callback
  );
}
addAsync(1, 2, (success) => {
  const result = success;
});
```

但當有一連串相關的非同步處理，多次呼叫 callback function 會造成語法內嵌，使得程式碼難以閱讀和維護，亦即所謂的 callback hell：

```javascript
var floppy = require("floppy");

// 不斷層疊的 callback function 導致難以閱讀和理解
floppy.load("disk", function (data) {
  floppy.load("disk", function (data) {
    floppy.load("disk", function (data) {
      floppy.load("disk", function (data) {
        floppy.load("disk", function (data) {
          floppy.load("disk", function (data) {
            floppy.load("disk", function (data) {
              floppy.load("disk", function (data) {
                // do something...
              });
            });
          });
        });
      });
    });
  });
});
```

## Promises

- 為了解決 callback hell 的問題，ES2015 實作了 `Promise API` 提供不同的非同步處理方式
- 我們可以使用 `.then` 將原本不斷層疊的連續行為，改寫成段落串接式的寫法
- 雖然關係上仍然是接連處理，在撰寫和閱讀上有了大幅的差異

```js
function promiseFn(num, time = 500) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      num ? resolve(`${num}, 成功`) : reject("失敗");
    }, time);
  });
}

promiseFn(1)
  .then((res) => {
    console.log(res);
    return promiseFn(2);
  })
  .then((res) => {
    console.log(res);
  });
```

`Promise` 會帶入 `resolve` 和 `reject` 兩個 callback function：

```javascript
new Promise(function (resolve, reject) {
  // asynchronous action here
  if (success) {
    // resolve 回傳成功時的值
    resolve(success_value));
  }
  // reject 回傳失敗時的值
  reject(fail_value);
});
```

`Promise` 有四種狀態：

1. ⏳ `pending`（擱置）：初始狀態，操作未開始執行
2. ✅`fulfilled`（實現）：操作成功完成
3. ❌`rejected`（拒絕）：操作失敗
4. `settled`（解決）：操作已結束

- 當同步操作完成後，`resolve` 會觸發 fulfilled，執行 `.then` 之後的行為
- 失敗時則會由 `reject` 觸發 rejected，執行 `.catch` 之後的行為
- 這兩個 callback function 回傳的也是 promise
- `Promise` 也可以直接呼叫 `resolve` 接受某個值或操作
  - 例如必定會如預期的行為，或是來自不同 Promise API 的 promise
- 亦可呼叫 `reject` 用於偵錯或保持一致性時，拒絕某個值或操作

```javascript
Promise.resolve(foo()).then(bar()).then(lastStep);
```

- 另外還有兩個方法 `.race` 和 `.all` 可以使用，這兩者都是傳入一個陣列
  - `.race` 是傳入陣列中任何一個 promise 物件解決之後，就會往下執行
  - `.all` 則是要傳入陣列中的所有 promise 物件都解決才會往下執行。
- [Javascript Promise example 簡易實作模擬](https://iamian.cc/promise/)

```javascript
const p1 = Promise.resolve(3);
const p2 = 1337;
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("foo"), 1000);
});

Promise.all([p1, p2, p3])
  .then((value) => {
    console.log(value); // [3, 1337, "foo"]
  })
  .catch((err) => {
    console.log(err.message);
  });
```

## Async / Await

- 於 ES7 新增
- Promise 解決了 callback hell 問題，但無法處理條件分歧
- 條件分歧必須改回 callback 寫法，但 Async / Await 解決了狀態管理問題
- 但 Async / Await 並非為了取代 Promise，而是為了與 Promise 搭配運用
- 於 function 前加上 `async`，回傳值會變為 Promise
- 欲使用 Promise 或 function 回傳的 Promise 時，需使用 `await`
  - 如 `let phone = await willGetNewPhone`
  - 或 `let message = await showOff(phone)`
- 可於函式內使用 `try {} catch (error) {}` 攔截未預期行為或錯誤訊息

```javascript
async function getData() {
  const data1 = await promiseFn(1);
  const data2 = await promiseFn(2);
  console.log(data1, data2);
}

getData();
```

<iframe src="https://www.youtube.com/embed/T-_0Pc5P12U" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

```javascript
// 同步與非同步行為同時存在
// 如何輸出 1, 2, 3
const test = async () => {
  console.log(1);
  await setTimeout(() => {
    console.log(2);
  }, 1000);
};
const main = async () => {
  await test();
  console.log(3);
};
main();

// result: 1, 3, 2
// 修改為
const test = async () => {
  console.log(1);
  await new Promise((resolve) => {
    setTimeout(() => {
      console.log(2);
      resolve();
    }, 1000);
  });
};
const main = async () => {
  await test();
  console.log(3);
};
main();

// result: 1, 2, 3
// 不使用 async/await
const test = () => {
  console.log(1);
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log(2);
      resolve();
    }, 1000);
  });
};
const main = () => {
  test().then(() => {
    console.log(3);
  });
};
main();

// result: 1, 2, 3
```

## 中斷處理

## RxJS (Observables)

- [希望是最淺顯易懂的 RxJS 教學](https://blog.techbridge.cc/2017/12/08/rxjs/)
- [30 天精通 RxJS](https://blog.jerry-hong.com/series/rxjs)
- 可以被取消
- 需要時才執行

```js
let Observable = Rx.Observable;
let resultA, resultB, resultC;

function addAsync(num1, num2) {
  const promise = fetch(`http://example.com?num1=${num1}&num2=${num2}`).then(
    (x) => x.json()
  );
  return Observable.fromPromise(promise);
}

addAsync(1, 2)
  .do((x) => (resultA = x))
  .flatMap((x) => addAsync(x, 3))
  .do((x) => (resultB = x))
  .flatMap((x) => addAsync(x, 4))
  .do((x) => (resultC = x))
  .subscribe((x) => {
    console.log("total", x);
    console.log(resultA, resultB, resultC);
  });
```

- `Observable.fromPromise` 會將 Promise 轉換成 observable stream。
- `.do` 和 .`flatMap` 是 Observable 的運算子。
