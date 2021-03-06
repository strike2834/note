# Svelte 筆記

## What is Svelte？

- Svelte 是套秉持「Write less code」精神，為了建構 UI 而生的 **JavaScript 編譯器**
- 不同於 Vue 和 React 等框架在瀏覽器上執行處理，Svelte 先在編譯階段就完成建構
- Svelte 不採用 Virtual DOM diff，使用原生 JS 直接修改 DOM
- 擁有相對優秀的執行速度與檔案大小表現

## 安裝

### 前置需求

- Node.js
- npm

### 下載樣板

```bash
# download template
npx degit sveltejs/template svelte-app
# install dependencies
cd svelte-app
npm install
# start rollup
npm run dev
```

- `npx` 是 npm 在 v5.2.0 之後內建的指令，提供暫時性執行某個 npm 套件的功能
- `degit` 是一套能供使用者直接取用現存 project 樣板的套件
- 也可用 `npm i -g degit` 安裝後直接呼叫 `degit`

## 撰寫 Svelte

### 基礎語法

- svelte 與其它框架相同，使用獨有的 `.svelte` 副檔名撰寫
- 每個檔案為獨立的 component，包含 Javascript、CSS 和 HTML
  - 架構和傳統 HTML 相去不大
  - JS 和 CSS 分別寫在 `<script></script>`、`<style></style>` 標籤裡
  - HTML 元素直接撰寫於其下方

```html
<script>
  /* js gones here */
</script>

<style>
  /* styles goes here */
</style>

<!-- markup (zero or more items) goes here -->
```

- 變數可直接於 `<script>` 中常規宣告，並使用 `{}` 代入／顯示變數
  - 亦可使用於 attribute 的雙括號中：`<p class="primary-{bar}">Some text</p>`
- 與屬性同名的變數
  - 如 `<img src={src} alt="A man dances.">`
  - 可省略成 `<img {src} alt="A man dances.">`
- 匯入 component 亦同樣於 `<script>` 中引入即可使用
  - `import Nested from './Nested.svelte';`
- CSS 樣式作用域僅該 component
  - svelte 會自動用 hash 命名，因此不必擔心命名衝突

```js
import App from "./App.svelte";

const app = new App({
  target: document.body,
  props: {
    // we'll learn about props later
    answer: 42,
  },
});

<App />;
```

- svelte 可使用 `@html` 從 JS 中傳入 HTML 內容進行渲染
  - e.g. `<p>{@html string}</p>`
  - 但 svelte 沒有進行任何過濾處理，會有 XSS 攻擊的風險 d
    <br>需確保此內容來自可信任的來源

### Reactivity

- 「Reactivity」意指指派值時會觸發的相關行為，類似 Vue 的 `computed`
- svelte 以 `$:` 宣告 reactivity 內容
- component 的狀態改變時，會自動更新 `$:` 後面的行為內容到 DOM 上
  <br>e.g. `$: doubled = count * 2;`
  - 以 `$:` 宣告的變數不需再加上 `let` 等宣告
- `$:` 裡的行為亦可使用如 `console.log()` 等函式監看數值變化
- reactivity 只會於賦值時觸發
  - 如 Array 的 `push` 和 `splice` 不會觸發更新
    <br>因此 `push` 要改寫成 `numbers = [...numbers, numbers.length + 1];`
    <br>並且賦值變數（等號左邊的變數）必須為 `$:` 宣告的更新變數

```js
$: obj;
// 若是二段式的賦值，並不會觸發更新
const foo = obj.foo;
foo.bar = "baz";
// 除非在最後加上 obj=obj
obj = obj;
```

- 想於 Reactivity 裡進行多段處裡時，加上 `{}` 即可

```javascript
let length = "5";
let lengthNum;
$: {
  lengthNum = parseInt(length);
  console.log(lengthNum);
}
```

#### Reactivity 搭配非同步處理

- [Async reactive declarations · Issue #2118 · sveltejs/svelte](https://github.com/sveltejs/svelte/issues/2118)

##### Reactive Statements

```svelte
<script>
let package_name = 'svelte';
let download_count = 0;
$: fetch('https://api.npmjs.org/downloads/point/last-week/' + package_name)
	.then(response => response.json())
	.then(data => download_count = data.downloads || 0);

// Updating `package_name` will asynchronously update `download_count`
</script>

```

##### Derived Stores

```svelte
<script>
import { writable, derived } from 'svelte/store';

const package_name = writable('svelte');
const download_count = derived(
	package_name,
	($package_name, set) => {
		fetch('https://api.npmjs.org/downloads/point/last-week/' + $package_name)
			.then(response => response.json())
			.then(data => set(data.downloads));

		return () => {
			// We override the `set` function to eliminate race conditions
			// This does *not* abort running fetch() requests, it only prevents
			// them from overriding the store.
			// To learn about canceling fetch requests, search the internet for `AbortController`
			set = () => {}
		}
	}
);

// Updating `$package_name` will asynchronously update `$download_count`
</script>

```

### Props（屬性傳遞）

- 想使用 props 傳入值時，需於 component 中的變數前加上 `export`
  - e.g. `export let answer;`
    <br>※此為 svelte 用法，與 Javascript 中的 `export` 用法不同
  - 亦可於宣告時指定預設值`export let answer = 'a mystery';`
- 就可將值傳入 component 中：`<Nested answer={answer}>`
- 亦可使用 `{...pkg}` 將物件傳進 component 的 props 內
  - e.g. `<Info {...pkg}/>`

### 區塊功能

#### 分歧

- svelte 提供了各種區塊語法，分歧區塊可依條件決定是否要 render 內容
- 各區塊皆以 `#` 開頭，以 `/` 結尾，以 `:` 連接
  - e.g. `{#if condition}` 開頭，`{/if}` 結尾

```
{#if x > 10}
  <p>{x} is greater than 10</p>
{:else if 5 > x}
  <p>{x} is less than 5</p>
{:else}
  <p>{x} is between 5 and 10</p>
{/if}
```

#### 遞迴

- 遞迴區塊可以遞迴陣列或 array-like 型態的資料
  - `{#each 變數 as 區域變數, index}` 開頭，`{/each}` 結尾
  - 其中可使用如 `{區域變數.值}` 顯示內容
- 也可先解構內容後再顯示
  - `{#each 變數 as { 值1, 值2 }} ... {/each}`
- 替 item 加上 key：`{#each things as thing (thing.id)}`

#### 非同步處理

```
<script>
  export id;
  const api = fetch(`/post/${id}`).then(res => res.json());
</script>

{#await api}
  <p>...waiting</p>
{:then response}
  <p>The response is {response}</p>
{:catch error}
  <p style="color: red">{error.message}</p>
{/await}
```

### 事件綁定

- bind event：`<div on:mousemove={handleMousemove}></div>`
  - 也可使用 inline 寫法：`<div on:click={() => console.log("clicked");}></div>`
- svelte 也實作了自動註冊和銷毀事件的處理，省去撰寫的麻煩
- bind event 亦可使用修飾子，以 `|` 加在 even 的後方：
  - `<div on:click|preventDefault={handleClick}>`
  - `preventDefault`
  - `stopPropagation`
  - `passive`
  - `capture`
  - `once`
  - `self`

#### Event dispatcher

- svelte 亦提供了客製化事件的功能

`Event.svelte`：

```html
<script>
  import { onMount, createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  onMount(() => {
    setTimeout(() => dispatch("completed", { elapsedTime: 3000 }), 3000);
  });
</script>
```

`App.svelte`：

```html
<script>
  import Event from "./Event.svelte";
  let completed = false;
  let name = "world";
  let once = false;
  function handleClick(e) {
    console.log("clicked");
  }
</script>

<Event on:completed={() => completed = true}></Event>

{#if completed}
  <span>Finished</span>
{/if}
```

### 資料綁定

- bind data（`v-model`）
  - `<input bind:value={name}>`
  - 會將值同步更新回變數，或將值反應到 `input` 上
  - 也可以用來套用 DOM 屬性
    - 例如：`<input type="checkbox" bind:checked={isChecked} />`
    - 或是：`<input type="radio" bind:group={selected} vale={1} />`
- bind DOM 元素
  - `<input type="text" bind:this="{inputNode}" />`
- bind class

  - `class:active={active}`
  - 當陳述為 true 時才綁定該 class
    - 當 class 與變數同名時，可以省略掉後方的括弧：`class:active`
    - 亦可於括號中撰寫陳述式
      <br/>例如：`class:active={status == 'playing'}`

  ```html
  <script>
    let active = false;
  </script>
  <style>
    .btn {
      padding: 1em;
      border-radius: .5em;
    }

    .active {
      background-color: #d7003a;
    }
  </style>
  <button class="btn" class:active={active} on:click={() => active = !active}>
    Click me
  </button>
  ```

### [生命週期](https://svelte.dev/docs#svelte)

- 初始化：`beforeUpdate` -> `onMount` -> `afterUpdate`
- 元件更新：`beforeUpdate` -> `afterUpdate`
- 元件銷毀：`onDestroy`
- `onMount`：在 Svelte 元件掛載時呼叫
  - SSR 模式不會呼叫
  - 回傳函式則會在 unmount／銷毀時呼叫
- `beforeUpdate`：狀態更新後、元件更新前執行
  - 會在 `onMount` 之前執行
    - 因此如 `bind` 之類於 `onMount` 階段執行的處理就會報錯
    - 以及這時狀態資料可能會更新，但還沒反應到 DOM 上
- `afterUpdate`：狀態更新後、元件更新後執行
- `onDestroy`：元件銷毀時執行

```javascript
import { onMount } from "svelte";
onMount(() => {
  // execution here
});
```

### [Store](https://svelte.dev/docs#svelte_store)

- 統一保存資料管理狀態
- Store 用於資料經常變動，並且需要跨元件使用時
- Svelte 提供了 3 個 function，設定資料的可存取範圍，
  <br/>分別為 `readable()`、`writable()`、`derived()`
- 將想存於 store 的值以此 function 宣告即可，例如 `const count = writable(0);`
- 以及 1 個 `subscribe()` 方法，用以處理元件的生命週期問題

#### `writable()`

- 可以使用 `update()` 或 `set()` 從外部修改 store 的值
- `import { writable } from 'svelte/store'`

```javascript
const countdown = writable(10);
countdown.update((currentValue) => {
  return 9;
});
countodnw.set(9);
```

#### `subscribe()`

- 所有的 svelte store 都有個 `subscribe` 方法
- 當值更新時會進行通知，以及處理元件的生命週期問題
- 呼叫後會回傳一個 unsubscribe 函數，可以搭配生命週期的 `onDestroy` 使用，避免 memory leak 問題（※）

※：Svelte 的教學裡對這部份沒有太多著墨，相關概念應該是來自於 RxJS，需要這樣做的原因是，假如主應用中 `元件 A` 需要存取 store（等同於 RxJS 中的 `subscribe`？），當使用者切換到另一個頁面，原本的 `元件 A` 會銷毀並切換為 `元件 B`，但 `元件 A` 的資料取用行為還存在（instance 依然存在），就會造成 memory leak 與無法預期的行為，因此需要 `unsubscribe`

- [angular - Angular/RxJs When should I unsubscribe from \`Subscription\` - Solve Old Bugs](https://oldbug.net/q/2ZThe/Angular-RxJs-When-should-I-unsubscribe-from-Subscription)
- [\[Angular\] RxJs unsubscribe 的時機](https://yuugou727.github.io/blog/2019/06/22/when-to-unsubscribe/)
- [Why It's Important to Unsubscribe from RxJS Subscription](https://netbasal.com/why-its-important-to-unsubscribe-from-rxjs-subscription-a7a6455d6a02)
- [ueler/angular-rxjs-unsubscribe](https://github.com/ueler/angular-rxjs-unsubscribe)

`store.js`

```javascript
import { writable } from "svelte/store";

export const count = writable(0);
```

`Incrementer.svelte`

```html
<script>
  import { count } from "./stores.js";

  function increment() {
    count.update((n) => n + 1);
  }
</script>

<button on:click="{count.increment}">+</button>
```

`App.svelte`

```html
<script>
  import { onDestroy } from "svelte";
  import { count } from "./stores.js";
  import Incrementer from "./Incrementer.svelte"; // 對 store 進行存取操作的 component

  let count_value;

  const unsubscribe = count.subscribe((value) => {
    count_value = value;
  });

  onDestroy(unsubscribe);
</script>

<h1>The count is {count_value}</h1>
<Incrementer />
```

##### Auto-subscription

- 也可以在變數名稱前方加上 `$`，Svelte 就會自動 subscribe 此 store，同時處理 unsubscribe 邏輯
- `<span>{$countdonw}</span>`

```html
<script>
  import { count } from "./stores.js";
  import Incrementer from "./Incrementer.svelte";

  let count_value;

  const unsubscribe = count.subscribe((value) => {
    count_value = value;
  });
</script>

<h1>The count is {$count}</h1>
<Incrementer />
```

#### `readable()`

- 只能從內部元件使用 `set()` 修改，外部元件只能取得資料的 store
- 例如滑鼠的所在位置，或是使用者的地理座標
- 第一個參數為預設值，第二個參數為修改資料的 function
- `import { readable } from 'svelte/store'`

  ```javascript
  chatSub = readable([], (set) => {
    let chatList = [];
    set([]...chatList, chat]);
  })
  ```

#### `derived()`

- 接收 1 至多個 store 並且進行加工
- `import { derived } from 'svelte/store'`;
- 類似 Vue 的 `computed`？

```html
<script>
  import { derived } from "svelte/store";
  const list = readable(["Do homework", "sleep", "programming"]);
  const ids = writable([1, 2]);

  const selectedList = derived([list, ids], ([list, ids], set) => {
    set(list.filter((val, i) => ids.inclueds(i)));
  });
</script>

{$selectedList}
```

### [Context](https://svelte.dev/docs#setContext)

- Context 用於資料幾乎不會變動或跨元件溝通時
- 沒有 reactive 效果（e.g. subscribe, unsubscribe）
- 需要在 svelte 元件中使用才有效果
- 只作用在 svelte 的元件樹中
- svelte 會去尋找距離元件最近的 context

`App.svelte`

```html
<script>
  import Profile from "./Profile.svelte";
  import { setContext } from "svelte";
  const user = setContext("user", {
    name: "Kalan",
    age: 25,
  });
</script>

<Profile />
```

`Profile.svelte`

```html
<script>
  import { getContext } from "svelte";
  const user = setContext("user");
</script>

<h2>{user.name}</h2>

<p>{user.age}</p>
```

### [motion 機制](https://svelte.dev/docs#svelte_motion)

svelte 提供了「motion」機制處理數值動態的呈現

#### Tweened

例如下例：

```html
<script>
  import { writable } from "svelte/store";

  const progress = writable(0);
</script>

<style>
  progress {
    display: block;
    width: 100%;
  }
</style>

<progress value="{$progress}"></progress>

<button on:click="{() => progress.set(0)}">0%</button>

<button on:click="{() => progress.set(0.25)}">25%</button>

<button on:click="{() => progress.set(0.5)}">50%</button>

<button on:click="{() => progress.set(0.75)}">75%</button>

<button on:click="{() => progress.set(1)}">100%</button>
```

修改進度條的數值後，進度條會馬上跳到指定的進度
<br>如果改為使用 motion 裡的 `Tweened` 取代 `writable`：

```html
<script>
  import { tweened } from "svelte/motion";
  import { cubicOut } from "svelte/easing";

  const progress = tweened(0, {
    duration: 400,
    easing: cubicOut,
  });
</script>
...
```

進度條的值變更後，就會有中間進度變化的過程了

- `Tweened` 可以使用 `duration` 與 `easing` 定義兩個數值之間的變化
- 介面和 writable store 相同，具有 `subscribe`、`set`、`update` 等方法
- 使用簡記：

```html
<script>
  import { tweened } from "svelte/motion";
  const value = tweened(10, { duration: 3000 });
</script>

{$value}
```

```html
<script>
  import { onMount } from "svelte";
  import { tweened } from "svelte/motion";
  let name = "world";
  let year = tweened(1990, { duration: 1500 });
  onMount(() => {
    setTimeout(() => year.set(2020), 2000);
  });
</script>
{Math.floor($year)}
<h1>Hello {name}!</h1>
```

#### Spring

motion 還有 `Spring` 可以使用 `stiffness`（剛性）和 `damping`（摩擦係數）
<br>替動畫加上輕重緩急，讓物件動態變得更生動

例如以下是一個圖片會追隨滑鼠移動的範例，將 `writable` 改為 `spring` 之後，晃動滑鼠後圖片的移動會變為具有彈簧般的來回變化。

```html
<script>
  import { spring } from "svelte/motion";
  let positionX, positionY;
  let image;
  let imageURL = "";

  let position = spring(
    {
      x: 0,
      y: 0,
    },
    {
      stiffness: 0.1,
      damping: 0.5,
    }
  );

  function handleMousemove(e) {
    position.set({
      x: e.clientX - image.width / 2,
      y: e.clientY - image.height / 2,
    });
  }
</script>

<style>
  img {
    position: aboslute;
    width: 350px;
    cursor: move;
  }
</style>

<img
  bind:this="{image}"
  on:mousemove="{handleMousemove}"
  src="{imageURL}"
  style="{`transform: translate(${$position.x}px, ${$position.y}px);`}"
/>
```

### [transition 機制](https://svelte.dev/docs#svelte_transition)

- svelte 內建有 `fade`、`blur`、`fly`、`slide`、`scale`、`draw`、`crossfade` 等轉場／動態效果函式
- 使用 `<transition:轉場名稱>` 套用至元素上
- 亦可使用 `<in:轉場名稱 out:轉場名稱>` 單獨指定開始和結束要套用的轉場效果
- transition 採用將獨自的語法計算轉換成原生 css 動畫，因此較不會有效能問題
- 亦可搭配 svelte 的其它語法運用
- `draw` 與其它 function 較為不同，專門用於 SVG 圖形

#### transition 設定

- 這些轉場函式有兩個通用參數：
  - `delay`：延遲多久開始 transition
  - `duration`：transition 持續多久
- 各個動畫亦有獨自參數可以設定

  - e.g. `<h1 in:fade out:fly={{ x: 0, y: 50 }}>I'm Transition!</h1>`

  ```html
  <script>
    import { fade, fly } from "svelte/transition";
  </script>

  {#if condition}
  <div transition:fade>I'm Transition!</div>
  <div in:fade out:fly>I'm Transition!</div>
  {/if}
  ```

#### easing function 緩動函數

替移動加上緩急，讓動靜看起來更真實且活潑：

```html
<script>
  import { fade, fly } from "svelte/transition";
  import { elasticOut } from 'svelte/easing';
  let condition = false;

  setTimeout(() => condition = true, 250);
  setTimeout(() => condition = false, 2250);
</script>

{#if condition}
<div in:fade out:fly={{ x: 0, y: 100, easing: ealsticOut }}>
  I'm Transition!
</div>
{/if}
```

#### 自訂轉場函式

```html
  <script>
    let condition = false
    function rotate(node, params) {
      console.loog(params);
      const duration = 1000;

      return {
        duration,
        easing: cubicOut,
        css: t => `
          transform: rotate(${params.range * t}deg);
        `
      }
    }

    setTimeout(() => condition = true, 10)
  </script>

  {#if condition}
    <h1 transition:rotate={{ range: 180 }}>I'm Transition</h1>
  {/if}
```

#### 套用動畫效果到「未轉場」的元素上

svelte 還有 [animate](https://svelte.dev/docs#svelte_animate) 中所提供的 FLIP（First, Last, Invert, Play）function
<br>會計算元素的舊位置與新位置之間的距離後，套用到動畫效果上
<br>例如一個列表的資料有所改變，`flip` 會讓「沒有轉場」的元素也套用動畫效果

```html
<script>
  import { quintOut } from "svelte/easing";
  import { crossfade } from "svelte/transition";
  // 引入 animate 的 FLIP
  import { flip } from "svelte/animate";

  const [send, receive] = crossfade({
    duration: (d) => Math.sqrt(d * 200),

    fallback(node, params) {
      const style = getComputedStyle(node);
      const transform = style.transform === "none" ? "" : style.transform;

      return {
        duration: 600,
        easing: quintOut,
        css: (t) => `
          transform: ${transform} scale(${t});
          opacity: ${t}
        `,
      };
    },
  });
</script>

<!-- 使用 animate:flip 加上效果 -->
<label
  in:receive="{{key: todo.id}}"
  out:send="{{key: todo.id}}"
  animate:flip
></label>
```

### 樣板語法（Slot）

- 可以將客製化元件／內容放進子元件中

`Card.svelte`

```html
<style>
  .card {
    width: 300px;
    background-color: #efefef;
    padding: 15px;
  }
</style>
<div class="card">
  <slot>
    <p>Default Text</p>
  </slot>
</div>
```

`App.svelte`

```html
<script>
  import Card from "./Card.svelte";
  let name = "world";
</script>

<Card>
  <h2>Title</h2>
  <p>Body</p>
</Card>
```

- 可以替 slot 命名，讓元件能同時使用多個 slot
- 也可以將變數傳給父元件

`Card.svelte`

```html
<style>
  .card {
    width: 300px;
    background-color: #efefef;
    padding: 15px;
  }

  .image {
    height: 150px;
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
  }
</style>
<div class="card">
  <slot name="card-image" imageURL="{imageURL}">
    <div class="image" style="background-image: url({imageURL});"></div>
  </slot>
  <slot name="card-body">
    <p>Default Text</p>
  </slot>
</div>
```

`App.svelte`

```html
<script>
  import Card from "./Card.svelte";
  let name = "world";
  let title;
  let imageURL;
</script>

<style>
  img {
    max-width: 100%;
  }
</style>

<Card imageURL={''}>
  <img slot="card-image" let:imageURL={imageURL} src={imageURL} />
  <p slot="card-body">
    Body
  </p>
</Card>
```

### 內建 Element

- svelte 會在正確的時間點幫忙處理自訂與銷毀監聽器，省去需要的麻煩
- 可以幫忙處理 SSR 的問題
- `<svelte:self />`：遞迴使用元件
- `<svelte:window />`：操作 window 物件
- `<svelte:body />`：類似 `<svelte:window />`，操作 body
- `<svelte:head />`：操作 head
- `<svelte:component />`：動態引入 svelte 元件
- `<svelte:options />`：對元件分別指定編譯選項

```svelte
<script>
  export let count = 3;
</script>

{#if count > 0}
  <p>countdown ... {count}</p>
  <svelte:self count={count - 1} />
{:else}
  <p>empty</p>
{/if}
```

```svelte
<script>
  let innerWidth;
  $: console.log(innerWidth);
</script>

<svelte:window
  bind:innerWidth={innerWidth}
/>
```

#### Server-Side Rendering

`server.js`

```javascript
<script>
  require("svelte/register"); const express = require('express'); const myApp =
  express(); const App = require("./App.svelte").default; const{" "}
  {(html, css, head)} = App.render({}); myApp.use('/public',
  express.static('./public')); myApp.get('*', (req, res) =>{" "}
  {res.send(`
    <html>
      <head>
        ${head}

        <style>
          ${css.code}
        </style>
      </head>
      <body>
        ${html}
        <script src="/public/build/bundle.js"></script>
      </body>
    </html>`)}
  )
</script>
```

`main.js`

```javascript
import App from "./App.svelte";

const app = new App({
  hydrate: true,
  target: document.body,
});

export default app;
```

`rollup.config.js`

```javascript
  ...
  plugins: [
    svelte({
      hydratable: true,
      ...
    })
  ]
```

## Svelte 生態系

### SASS support

若想使用 SASS 語法撰寫 CSS，需於樣板安裝好後，再安裝 SASS 相依套件

```shell
npm install svelte-preprocess node-sass
```

安裝完成後，開啟 `rollup.config.js`

```javascript
// 於 import 區加入
import preprocess from 'svelte-preprocess`;

/* ... */

// 於 plugin 區加入 preprocess
exprot default {
  /* ... */
  plugins: [
    svelte({
      /* ... */
      preprocess: preprocess()
    }),
  ],
  /* ... */
}
```

這時我們修改 `App.svelte` 裡的樣式部分，於 `<style>` 裡加上 `lang='scss'`：

```html
<script>
  export let name;
</script>

<main>
  <h1>Hello {name}!</h1>
  <p>
    Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn
    how to build Svelte apps.
  </p>
</main>

<style lang="scss">
  $primary-color: #ff3e00;

  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: $primary-color;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
```

執行 `npm run dev`，確認是否成功生效。

若想讓 VSCode 上也支援相關顯示，需要再於根目錄新增或編輯檔案 `svelte.config.js`：

```javascript
// svelte.config.js
const preprocess = require("svelte-preprocess");

module.exports = {
  preprocess: preprocess(),
};
```

### Sapper

- svelte 的網頁框架，類似於 Vue 的 Nuxt.js

#### 安裝

```bash
# for Rollup
npx degit "sveltejs/sapper-template#rollup" my-app

# for webpack
npx degit "sveltejs/sapper-template#webpack" my-app
```

### [Smelte](https://smeltejs.com/?ref=madewithsvelte.com)

- svelte 的 CSS 框架，類似於 Vue 的 Vuetify
- [Sapper で Smelte を利用する - Qiita](https://qiita.com/azukisiromochi/items/969fc9808c931cfadf22)

#### 安裝

```bash
npx degit matyunya/smelte-sapper-template my-app
cd my-app
npm run dev
```

### [Routify](https://routify.dev/)

## 參考文章

- [Docs • Sapper](https://sapper.svelte.dev/docs/)
- [Svelte cheatsheet](https://gist.github.com/peltho/ad6e051b854cd3095f9e7f9d9c550a84)
- [Cheat Sheet - Svelte Society](https://sveltesociety.dev/cheatsheet/)
- [Svelte チュートリアルやってみた - Qiita](https://qiita.com/irico/items/3875c7ee6423cdf09392)
- [Svelte で Web サイトを作ってみて感じた魅力 - Qiita](https://qiita.com/nishinoshake/items/46a64591c6411af68af1#svelte)
- [Svelte のドキュメントを翻訳してみた - Qiita](https://qiita.com/myLifeAsaDog/items/5d3036201f37a98e685d)
