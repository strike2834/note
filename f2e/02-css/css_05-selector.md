# 5. 選取器

## 選取器類別

1. `*`：全體選擇器 universal selector
2. `div`：type 選取器
3. `.chrisClass1`：class 選取器
4. `#chrisID`：ID 選取器
5. attribute 屬性選取器
6. `selector[attritube=vaule]`：presence and value selectors 指定屬性選擇器<br />
   ├ `[attribute~=value]` 選定多個以空格隔開的 attribute 其中之一的值為 value 的元素<br />
   └ `[attribute|=value]` 選定接在 `-`（U+002D）或者單獨的 attribute 值為 value 呃元素，常用於選定語言子碼
7. substring matching attribute selectors 局部屬性選擇器<br />
   ├ `[attribute^='value']` 選定 attribute 值以 value 開頭／前綴的元素<br />
   ├ `[attribute$='value']` 選定 attribute 值以 value 結尾／後綴的元素<br />
   └ `[attribute*='value']` 選定 attribute 值中包含 value 的元素
8. psuedo-class 選取器 `:`<br />
   ├ 同樣屬於 class 的一種<br />
   ├ 可說是 CSS 本身提供的分類<br />
   └ 優先權同 class

### psuedo-class 選取器

- 錨點虛擬類別<br />
  ├ `:link`：尚未點擊<br />
  ├ `:hover`：滑鼠碰觸<br />
  ├ `:active`：點擊當下<br />
  ├ `:focus`：取得焦點<br />
  ├ `:visited`：點擊過後<br />
  │ 由於虛擬類別的優先權同於 class<br />
  │ 會遇到後者覆寫前者的規則問題<br />
  │ 在撰寫順序上需注意應為：<br />
  ├ 1. `a`<br />
  │ 2. `a: visited`<br />
  │ 3. `a: hover`<br />
  └ 4. `a: active`
- 狀態虛擬類別<br />
  ├ `:checked`<br />
  ├ `:unchecked`<br />
  ├ `:enabled`<br />
  └ `:disabled`
- 序列虛擬類別<br />
  ├ `:empty`<br />
  └ `:not()`
- `*-child`<br />
  ├ `:first-child`：第一個子元素<br />
  ├ `:last-child`：最後一個子元素<br />
  ├ `:nth-child(數字)`：第幾個子元素（從 1 數起，不是從 0）<br />
  ├ `:nth-child(2n)`：偶數的子元素（2 的倍數）<br />
  ├ `:nth-child(2n+1)`：奇數的子元素<br />
  ├ `:nth-last-child(數字)`：從後面數來第幾個子元素<br />
  └ `:only-child`：父元素內只有一個子元素
- `*-of-type`<br />
  ├ `:first-of-type`：同一種元素的第一個<br />
  ├ `:last-of-type`：同一種元素的最後一個<br />
  ├ `:nth-of-type(數字)`：同一種元素裏頭的第幾個<br />
  ├ `:nth-last-of-type(數字)`：同一種元素從後面屬過來第幾個<br />
  └ `:only-of-type`：只有這種元素

9. `::`：psuedo-element 選取器

- 應用於裝飾性的物件上
- `:: before（:before）`<br />
  在原本的元素「之前」加入內容，以 `display: inline-block` 的屬性存在
- `:: after（:after）`<br />
  在原本的元素「之後」加入內容，以 `display: inline-block` 的屬性存在
- `:: before（:before）` 與 `:: after（:after）` 一定要有 `content` 的屬性
- `content` 屬性可使用的值有：<br />
  ├ `none`<br />
  ├ `normal`<br />
  ├ `string`<br />
  ├ `url`<br />
  ├ `counter`<br />
  ├ `attr`<br />
  ├ `open-quote`<br />
  ├ `close-quote`<br />
  ├ `no-open-quote`<br />
  └ `no-close-quote`

10. 其它的偽元素選取器：

- `::selection`
- `::first-line（: first-line）`
- `::first-letter（: first-letter）`
- `::cue（: cue）`
- `::backdrop`
- `::placeholder`
- `::marker`
- `::spelling-error`
- `::grammar-error`

11. `:root`

- 通常用於存放 CSS 變數用
- 使用 `var(變數名稱)` 套用
- 變數以 `--` 開頭命名，ex: `--primary-color`

```css
:root {
  --width: 100vw;
  --max-width: 100vw;

  @media (min-width: 42em) {
    --width: 42rem;
  }
}
```

## 選取器運算子

- [CSS Selector 速見表](https://codepen.io/nana8/full/aXQgoj)
- `+` 選擇緊鄰元素<br />
  ├ 也就是第 2 個元素緊接於第 1 個元素之後，並且兩者擁有相同母元素<br />
  ├ `A + B`<br />
  └ 例：`h2 + p` 會選擇所有緊鄰於 `<h2>` 之後的 `<p>`
- `~` 選擇兄弟元素，<br />
  ├ 也就是第 2 個元素在第 1 個元素後方任意位置，並且兩者擁有相同母元素<br />
  ├ `A ~ B`<br />
  └ 例：`p ~ span` 會選擇所有在 `<p>` 元素之後的 `<span>`元素
- `>` 選擇直接子元素<br />
  ├ `A > B`<br />
  └ 例：`ul > li` 僅會選擇 `<ul>` 元素巢狀內第一層的 `<li>` 元素
- `\s` 選擇所有子元素<br />
  ├ `A B`<br />
  └ 例：`div span` 會選擇所有 `<div>` 內的 `<span>` 元素

## 選取器的權重

選取器具有權重，瀏覽器會依其決定要顯示的樣式<br />
相同權重但是後寫的 css，會覆蓋先寫的 css<br />
當一個元素同時有兩個選擇器，權重高的優先生效

## 基本權重

基本權重由高至低為：

- `!important`
- `inline style`
- `id`
- `class`／`psuedo-class`（偽類）／`attribute`（屬性選擇器）
- `Element`
- `*`

| 元素                                               | 權重                                |
| -------------------------------------------------- | ----------------------------------- | ------ |
| `Element`                                          | 所有的 Element 的權重都是 `0-0-0-1` |
| `class`                                            | 每一個 class 的權重都是 `0-0-1-0`   |
| `psuedo-class`                                     | 和 attribute 權重相同               |
| `id`                                               | 每一個 id 的權重都是 `0-1-0-0`      | <br /> |
| `inline style attribute`（寫在 html 行內的 style） | 權重為 `1-0-0-0`                    |
| `!important`                                       | 可以蓋過所有的權重                  |
