# 瀏覽器事件

JavaScript 起初是為了瀏覽器而創造，因此還有一系列針對瀏覽器運用的物件，<br />
藉此達成如操作或取得網頁上的元素，或是自訂互動等功能，<br />
而日後發展出伺服器用的 Node.js 時，也有因執行環境有不同的物件或事件。

- [DOM Events](https://domevents.dev/)

## Bubbling and Capture

其中例如點擊事件，若我們有一個三層巢狀的元素，每個元素各有一個點擊事件，<br />
點擊最內層的元素，將會由內至外連續觸發三層元素的事件，<br />
這個過程稱作「冒泡（Bubbling）」。

```html
<form onclick="alert('form')">
  FORM
  <div onclick="alert('div')">
    DIV
    <p onclick="alert('p')">P</p>
  </div>
</form>
```

「捕獲（Capture）」則是反過來，會從 `Window` 一路往下走到目標元素，<br />
DOM 事件標準裡定義了事件傳播的 3 個階段：「捕獲階段」、「目標階段」、「冒泡階段」。

```html
<form>
  FORM
  <div>
    DIV
    <p>P</p>
  </div>
</form>

<script>
  for (let elem of document.querySelectorAll("*")) {
    // adding Capture event listener
    elem.addEventListener(
      "click",
      (e) => alert(`Capturing: ${elem.tagName}`),
      true
    );
    // event bubbling
    elem.addEventListener("click", (e) => alert(`Bubbling: ${elem.tagName}`));
  }
</script>
```

## Event Delegation

如果想避免冒泡，可以使用 `event.stopPropagation()`。

```html
<form onclick="alert(`the bubbling doesn't reach here`)">
  <button onclick="event.stopPropagation()">Click me</button>
</form>
```

但阻止冒泡可能會導致預料之外的行為，且冒泡和捕獲讓我們能簡化大量需要類似處裡的元素，<br />
例如點擊一個 9x9 表格裡的元素，可以不必每個子元素逐格單獨處理，而由母元素表格統一處理。<br />
這稱作「事件委託（Event Delegation）」

```html
<table>
  <tr>
    <th colspan="3">
      <em>Bagua</em> Chart: Direction, Element, Color, Meaning
    </th>
  </tr>
  <tr>
    <td class="nw">
      <strong>Northwest</strong><br />Metal<br />Silver<br />Elders
    </td>
    <td class="n">...</td>
    <td class="ne">...</td>
  </tr>
  <tr>
    ...2 more lines of this kind...
  </tr>
  <tr>
    ...2 more lines of this kind...
  </tr>
</table>

<script>
  let selectedTd;

  table.onclick = function (event) {
    let target = event.target.closest("td");

    if (!td) return;
    if (!table.contains(td)) return;
    if (target.tagName != "TD") return;

    highlight(target);
  };

  function highlight(td) {
    if (selectedTd) {
      selectedTd.classList.remove("highlight");
    }
    selectedTd = td;
    selectedTd.classList.add("highlight");
  }
</script>
```

## MutationObserver

- [JavaScript 是如何工作的：使用 MutationObserver 跟踪 DOM 的变化](https://blog.fundebug.com/2019/01/10/understand-mutationobserver/)
- [How JavaScript works: tracking changes in the DOM using MutationObserver | by Alexander Zlatkov | SessionStack Blog](https://blog.sessionstack.com/how-javascript-works-tracking-changes-in-the-dom-using-mutationobserver-86adc7446401)
- [DOM 变动观察器（Mutation observer）](https://zh.javascript.info/mutation-observer)

### 簡介

`MutationObserver` 會在指定的 DOM 出現變化，例如增減節點、變更屬性、修改文字時回傳通知。

### 使用

想要使用 `MutationObserver` 之前，我們需要先建立一個 instance，並且傳入一個 function 讓它每次偵測到變化時調用。

```javascript
const mutationObserver = new MutationObserver(function (mutations) {
  mutations.forEach(function (mutation) {
    console.log(mutation);
  });
});
```

建立好的物件有三個 methods：

- `observe`：開始監聽變化，需要兩個參數—— 你想觀測的 DOM 節點和設定用的物件
- `disconnect`：停止監聽變化
- `takeRecords`：回傳 callback 啟動之前的最後一次修改

這裡有個開始監聽變化的例子：

```javascript
// Starts listening for changes in the root HTML element of the page.
// 第一個傳入參數為監察目標，可改為如 document.querySelector("body")
mutationObserver.observe(document.documentElement, {
  attributes: true,
  characterData: true,
  childList: true,
  subtree: true,
  attributeOldValue: true,
  characterDataOldValue: true,
});
```

當我們調用了 `mutationObserver.observe(...)` 開始監聽，網頁上的 DOM 出現變化時，我們就能在控制台裡看到 mutations 陣列裡的各個 [MutationRecord](https://developer.mozilla.org/zh-TW/docs/Web/API/MutationObserver#MutationRecord) 的記錄。

當工作完成，我們想要停止觀察 DOM，可以調用相關 method：

```javascript
// Stops the MutationObserver from listening for changes.
mutationObserver.disconnect();
```

在 `MutationObserver` 出現之前，人們用來觀測網頁元件變化的方法有：

- Polling
- MutationEvents
- CSS animations

Polling：最簡單也最簡潔的方法，使用瀏覽器的 `setInterval` WebAPI 定期檢查是否發生任何變化，但這種方法會明顯地降低網路應用／網站的效能。

MutationEvents：於 2000 年加入的 [Mutation events API](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Mutation_events)，由於它在每次 DOM 變化都會被調用，同樣導致效能問題，目前 `MutationEvents` API 已經被棄用。

CSS animations：這是個有些特怪異的方案，基本上的概念是一個有 CSS 動畫的元素加進 DOM 中時，動畫開始就會觸發 animationstart 事件，當我們再對這個事件加上 handler，就能掌握元素加進 DOM 中的確切時間。

```html
<div id="container-element"></div>
```

```css
@keyframes nodeInserted {
  from {
    opacity: 0.99;
  }
  to {
    opacity: 1;
  }
}

#container-element * {
  animation-duration: 0.001s;
  animation-name: nodeInserted;
}
```

需要先檢查 `event.animationName` 是否是我們所想要的動畫。

```javascript
var insertionListener = function (event) {
  // Making sure that this is the animation we want.
  if (event.animationName === "nodeInserted") {
    console.log("Node has been inserted: " + event.target);
  }
};

document.addEventListener("animationstart", insertionListener, false); // standard + firefox
document.addEventListener("MSAnimationStart", insertionListener, false); // IE
document.addEventListener("webkitAnimationStart", insertionListener, false); // Chrome + Safari
```

`MutationObserver` 相較這些方案提供了更多優勢，包括它涵蓋了 DOM 中的每種可能變化，以及分段啟動的特性，讓它有更好的效能，並且擁有相當優秀的支援性。

## IntersectionObserver

- [example](https://codepen.io/osublake/embed/6fd214ecd74e7091ec7b609bb0270f97?height=450&slug-hash=6fd214ecd74e7091ec7b609bb0270f97&user=osublake&tab-bar-color=%23222&name=cp_embed_2#result-box)

### 簡介

`IntersectionObserver` 會在指定的目標出現在觀察器 (window) 中時，才回傳 `true`，
不同於 jQuery 的 `onscroll` 是在每次捲動時都執行一次監聽。

### 使用

`let observer = new IntersectionObserver(callback, [option]);`

- `callback`: 要執行的動作函式

callback 預設的傳入參數為一陣列

```javascript
[
  {
    // 唯讀變數，目標元素的矩形節點的資訊 (ID、座標、長寬)
    boundingClientRect: {},
    // 目標元素的出現比例
    intersectionRation: 1,
    // 唯讀變數，目標元素與觀察器的相交區域
    intersectionRect: {},
    // 是否出現於觀察器中
    isIntersecting: true,
    // 觀察器的資訊
    rootBounds: {},
    // 目標
    target: 目標的 DOM 節點
  }
];
```

- `option`: 有三個參數可調整

```javascript
{
  root: null,
  rootMargin: "0px 0px 0px 0px",
  threshold: [0]
}
```

- `root`: 可指定某個特定的 element 做為觀察器: `root: documnet.getElementById('container')`，預設值為 `null`，即目前觀看中的視窗。
- `rootMargin`: 四個值依序為上、右、下、左，可放大或縮小的觀察器的範圍，預設值為 `"0px 0px 0px 0px"`。
- `threshold`: 指定目標出現於觀察器內的百分比，到達該值後才執行 callback，可指定多個值如: `[0, 0.25, 0.5, 0.75, 1]` 會在目標出現 0%、25%、50%、75%、100% 的時候都執行一次 callback 函式，預設值為 `[0]`，即目標接觸到觀察器的邊緣便觸發 callback 函式。
- `observer.observe(el)`
- `observer.unobserve(el)`
- `observer.disconnect()`
- [browser-2020](https://github.com/luruke/browser-2020)
- [リソースの読み込みを助けるウェブブラウザ API の世界](https://nhiroki.jp/2021/05/06/resource-loading-apis)
