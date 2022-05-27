# 11. CSS 命名與設計模式

- [1 段上の CSS 設計・コーディングの概念図 ( HCDC モデル図 )](https://qiita.com/croco_works/items/3f0f7407db5f263d2562)
- [HCDC による分析と考察／CSS 設計のモデル図が出来るまで](https://qiita.com/croco_works/items/9a0698097fba2312b9ad)
- [漫談 CSS 架構方法 - 以 OOCSS, SMACSS, BEM 為例](https://www.slideshare.net/kurotanshi/css-oocss-smacss-bem)
- [CSS 不是我們想像的這麼簡單！](https://speakerdeck.com/kurotanshi/css-bu-shi-wo-men-xiang-xiang-de-zhe-mo-jian-dan-tai-bei-chang)
- [CSS のクラス名を決めるときに使うリストをつくりました](https://qiita.com/manabuyasuda/items/dbb76ed36970bec95470)
- [Naming -名前付け- - Qiita](https://qiita.com/Koki_jp/items/f3d3e824f98d182d4100)
- [CSS のクラス名を書く前に最低限知っておくべきルール＆BEM を改良してみた - Qiita](https://qiita.com/taka555/items/6c39f3fe7fca834aa448)
- [各 CSS 設計手法を取り入れる上でのメリット・デメリットをまとめてみた](https://qiita.com/nezurika/items/a964e21d3596b0ee4c9a)
- [CSS 設計完全ガイドで学んだ PRE_CSS を Elm で堅牢に実装する](https://qiita.com/ababup1192/items/9a305c95cdf4d93fd32a)
- [脱・ Atomic Design - HTML+CSS コーディングの粒度分類法 ( HTML Parts )](https://qiita.com/croco_works/items/e34d1b0c0e50b37031d7)
- [1 年前に素人が FLOCSS 使って直面した疑問/失敗に対し、PRECSS を学んで解消 / 前進できた話 - Qiita](https://qiita.com/SYM_simu/items/9d653155fd98e12a641c)

## OOCSS（模組化 CSS，Object Oriented CSS）

### 兩大原則

- 結構與外觀分離 Separate Structure and Skin
- 容器與內容分離 Separate Container and Content

```css
#button {
  width: 200px;
  height: 50px;
  padding: 10px;
  border: solid 1px #ccc;
  box-shadow: rgba (0, 0, 0, 0.5) 2px 2px 5px;
}

#box {
  width: 400px;
  overflow: hidden;
  border: solid 1px #ccc;
  background: linear-gradient (#ccc, #222);
  box-shadow: rgba (0, 0, 0, 0.5) 2px 2px 5px;
}

#widget {
  width: 500px;
  min-height: 200px;
  overflow: auto;
  border: solid 1px #ccc;
  background: linear-gradient (#ccc, #222);
  box-shadow: rgba (0, 0, 0, 0.5) 2px 2px 5px;
}

.button {
  width: 200px;
  height: 50px;
}

.box {
  width: 400px;
  overflow: hidden;
}

.widget {
  width: 500px;
  min-height: 200px;
  overflow: auto;
}

.skin {
  border: solid 1px #ccc;
  background: linear-gradient (#ccc, #222);
  box-shadow: rgba (0, 0, 0, 0.5) 2px 2px 5px;
}
```

## [SMACSS](http://smacss.com/)（Scalable & Modular Architecture for CSS）

- Categorization 將結構分類
- Naming rules 命名規則
- Decoupling CSS from HTML CSS 與 HTML 分離

### 1. Base

- CSS Reset
- CSS Normalize
- 在 Base 類別裡不應使用 !important

```css
/* Base */

html {
  background-color: #fff;
}

body,
form {
  padding: 0;
  margin: 0;
}

a {
  text-decoration: none;
}

h1,
h2,
h3 {
  margin: 1em 0;
}
```

### 2. Layout

- Header
- Sidebar
- Content

```css
/* Layout */

# header {
  width: 960px;
  margin: 0 auto;
}

.l-article {
  ...;
}

.l-grid {
  ...;
}

.l-grid > li {
  ...;
}
```

### 3. Module

- 頁面上可單獨存在並且可重複使用的元件
- 定義 Module 時應避免使用 id 或標記名稱做選擇器
- 子模組以原模組名稱加 dash（`-`）作為名稱。如: `.mod-header`, `.mod-body`

例如：

- Tabs
- Customized List
- Button

```html
<div class="fld">
  <span>Folder name</span>
</div>
```

```css
/* The Folder Module */
.fld > span {
  padding-left: 20px;
  background: url (icon.png);
}
```

```html
<div class="fld">
  <span>Folder Name</span>
    <span> ( 32 items ) </span>
</div>

<div class="fld">
  <span class="fld-name">Folder Name</span>
    <span class="fld-items> ( 32 items ) </span>
</div>
```

### 4. State

- 與 Layout, Module 搭配
- 表示 Layout 或 Module 的狀態變化
- 由 class 定義
- 命名規則是 `.is-*` 開頭

例如：

- Disabled State
- Default State
- Active State
- Default State

```css
/* State */
.is-hidden {
  display: none;
}

.is-error {
  font-weight: 700;
  color: #f00;
}

.is-tab-active {
  border-bottom-color: transparent;
}
```

### 5. Theme

- 定義網站主視覺
- 類似 Layout，但影響的是網站整體視覺的變化。
- class 名稱通常以 `.theme-*` 做開頭

## BEM（Block-Element-Modifier）

- 拋棄語意式命名，改以工具功能、性質命名。

### 命名結構

- 以 Block 起始
- Element 接續（中間使用 2 個底線連結）
- Modifier 做結（中間使用 2 個橫線連結）。
- `block__element--modifier`

### 1. Block

可獨立再利用的內容，即前端框架裡的元件，例如 card 便是個好的 Block 例子。

避免如 shopping-list 這類具體的名字，
<br />命名為 check-list 這類一般性的名稱，能夠在各種情況下再利用。
<br />例如命名為 check-list 後便能同時在 shopping-list 和 TODO List 裡使用。

- 在頁面上獨立存在並可重複使用的元件
- 如同 SMACSS 的 Module, Layout
- 每個 Block 都是獨立存在的

```css
.button .b-button .text-field .b-text-field .heading .b-heading .menu .b-menu;
```

### 2. Element

只存在於 Block 裡的內容，例如 `card__title` 或 `card__text`、`card__button`。

Element 只允許一層巢狀。也就是說，規範上是不可命名為 `card__button__text`的。
<br />但可以將 button 定義為新的 Block，並命名為 `button__text`。

- 為 Block 的一部份（子組件）
- 無法獨立於 Block 之外
- 有些 Block 可能沒有 Element

```css
.button__icon .text-field__label .heading__title .menu__item;
```

### 3. Modifier

用於修飾 Block 或 Element，因此必定存在做為基底的 class。
<br />以 card 為例：card card--featured. card class 本身有 padding 和 border, card--featured class 只改變背景顏色。

- 用來定義 Block 或 Element 的狀態或屬性
- 類似 SMACSS 的 State
- 同一個 Block 或 Element 可以允許多組 modifier 同時存在

```css
.button_active .text-field_editable .heading_align_top .menu__item_promo;
```

### [Chainable BEM modifiers](https://qiita.com/yasuhiro-yamada/items/25b170d2b56005bf413e)

由 Jordan Lewis 所提出的 BEM 改寫方式，簡略為 `-命名空間-值`，
<br />例如：`-color-red`, `-size-large`，同一個命名空間不可賦予兩個以上的值。

```html
<!-- Large green button -->
<button class="btn -color-green -size-large"></button>
```

```scss
.btn {
  font-size: 20px;
  background-color: grey;

  &.-color-green {
    background-color: green;
  }

  &.-size-large {
    font-size: 30px;
    padding: 10px;
  }
}
```

由伺服器端或 JavaScript 進行狀態修改的 class 則加上 `is-`。

- [BEM, CSS 設計模式](https://chupainotebook.blogspot.com/2019/05/bemcss.html)
- [BEM を使うべき 5 つの理由 ( なぜ BEM が G.R.E.A.T といえるのか )](https://frasco.io/5-reasons-to-use-bem-f5ca38f748a1)
- [[BEM 設計]うわああああ三 ( 卍^o^ ) 卍ってならない BEM の書き方をワイヤーフレーム使って整理するぞ ( その 1 )](https://qiita.com/mame_hashbill/items/bf541f795533b40e3cdc)
- [[BEM 設計]うわああああ三 ( 卍^o^ ) 卍ってならない BEM の書き方をワイヤーフレーム使って整理するぞ ( その 2 )](https://qiita.com/mame_hashbill/items/81267a7ec498ff113a3b)
- [うわあああああああ三 ( 卍^o^ ) 卍ってなってたどりついた私的な BEM の使い方](https://qiita.com/mame_hashbill/items/972b124a9a476cf8b326)
- [naming BEM sub blocks [duplicate]](https://stackoverflow.com/questions/22723290/naming-bem-sub-blocks)
- [BEM Naming](http://getbem.com/naming/)
- [BEM Key concepts](https://en.bem.info/methodology/key-concepts/)
- [一番詳しい CSS 設計規則 BEM のマニュアル](https://qiita.com/Takuan_Oishii/items/0f0d2c5dc33a9b2d9cb1)
- [[HTML/SCSS] BEM 設計をワイヤーフレームを使って解説してみる](https://qiita.com/mame_hashbill/items/c5b09461d7acfce047fa)
- [flocss](https://github.com/hiloki/flocss)

## FLOCSS

## PRECSS

## Atomic CSS 樣式原子化

- [Atomic Design を分かったつもりになる](https://design.dena.com/design/atomic-design-%E3%82%92%E5%88%86%E3%81%8B%E3%81%A3%E3%81%9F%E3%81%A4%E3%82%82%E3%82%8A%E3%81%AB%E3%81%AA%E3%82%8B/)
- [フロントエンドのコンポーネント設計に立ち向かう](https://qiita.com/seya/items/8814e905693f00cdade2)

## HTML Parts

- [脱・Atomic Design - HTML+CSS コーディングの粒度分類法（HTML Parts）](https://qiita.com/croo_works/items/e34d1b0c0e50b37031d7)
