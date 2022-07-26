# Defensive CSS

- [CSSによるレイアウトの崩れやおかしな挙動を解決するテクニックのまとめ -Defensive CSS](https://coliss.com/articles/build-websites/operation/css/defensive-css.html)

## 讓 Flexbox 元素換行

- 當容器只使用 `display: flex;`，元素會在縮減至小於容器寬度後超出
- 須加上 `flex-wrap: wrap;`

## 預留足夠空間

- 例如大標右邊有互動按鈕，在容器縮小後兩者會擠在一塊
- 替大標加上右方空間，例如 `margin-right`

## 避免過長文字擠壓

```css
  .username {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
```

## 避免圖片因容器而扭曲

```css
  .card__thumb {
    object-fit: cover;
  }
```

## 避免多重捲動

- 當捲動 modal 至底部後，會連同 `body` 頁面一同移動
- scroll chaining

```css
  .modal__content P{
    overscroll-behavior-y: contain;
    overflow-y: auto;
  }
```

## 替 CSS 變數加上 fallback

- 例如 `var(--actions-width)` 若是透過 JavaScript 取得，失敗則會變為 `none`

```css
  .message__bubble {
    max-width: calc(100% - var(--actions-width, 70px));
  }
```

## 避免固定寬高導致跑版

- 改為使用 `min-height` 與 `min-width` 取代 `height` 與 `width`

## 防止背景無限重複

- 背景圖片預設為重複顯示
- `background-repeat: no-repeat;`

## 垂直情況的響應式排版

- 例如側邊欄的 Menu 與 Footer 在高度小於容器後會造成兩者重疊

```css
  @media (min-height: 600px) {
    .aside__secondary {
      position: sticky;
      bottom: 0;
    }
  }
```

## 調整 `justify-content: space-between`

- 使用 flexbox 的 `justify-content: space-between` 時，元素過少會造成間隔過大
- 使用 `gap` 進行調整

## 配合圖片上方的文字

- 當於圖面上配置文字時，若圖片讀取失敗，可能會造成文字難以讀取
- 替圖片元素加上背景色

```css
  .card__img {
    background-color: grey;
  }
```

## 於 CSS Grid 使用固定值時要注意

```css
  .wrapper {
    display: grid;
    grid-template-columns: 250px 1fr;
    gap: 1rem;
  }
```

此例於窗口過小時會導致排版，故須加上響應式：

```css
  @media (min-width: 600px) {
    .wrapper {
      display: grid;
      grid-template-columns: 250px 1fr;
      gap: 1rem;
    }
  }
```

## 只於必要情況顯示捲軸

- `overflow-y: auto;`

## 保留捲軸空間

- `scrollbar-gutter: stable;`

## 保留 flexbox 容器的寬度邊界

- 當 flexbox 容器裡有超出寬度的元素，即使設定 `overflow-wrap: break-word` 也沒有效果
- 這是因為子元素的寬度預設為 `auto`
- 須替該元素設定 `min-width: 0;`
- 高度亦同，須設定 `min-height: 0;`

## 保留 CSS Grid 容器的寬度邊界

- CSS Grid 的子元素的寬度同樣會是 `auto`
- 可以使用 `minmax()`、替子元素加上 `min-width`、替子元素加上 `overflow: hidden`
- 防禦性的 CSS 推薦使用 `minmax()`

```css
  @media (min-width: 1020px) {
    .wrapper {
      display: grid;
      grid-template-columns: minmax(0, 1fr) 248px;
      /* 設定為 minmax(0, 1fr) 而非 1fr */
      grid-gap: 40px;
    }
  }
```

## 區別 `auto-fit` 與 `auto-fill` 的使用

- 使用 `minmax()` 時，如何區分 `auto-fit` 與 `auto-fill` 的使用相當重要
- `auto-fit` 會將可使用的空間全部填滿，並延伸 grid 元素的空間
- `auto-fill` 不會延伸 grid 元素的空間，保留可使用的空間
- 例如只有一個元素時，`auto-fit` 就會讓該元素填滿整個容器，使用 `auto-fill` 便能維持相同寬度

## 圖片寬度

- 推薦將所有圖片元素設為 `max-width: 100%;`

## CSS Grid 的子元素無法使用 `position: sticky` 時

```css
  aside {
    align-self: start;
    /* 需要重新設定 align-self */
    position: sticky;
    top: 1rem;
  }
```

## 不建議把跨瀏覽器的樣式寫在一起

例如：

```css
  input::-webkit-input-placeholder,
  input:-moz-placeholder {
    color: #222;
  }
```

根據 w3c 整個樣式都會無效，應改寫為：

```css
  input::-webkit-input-placeholder {
    color: #222;
  }
  
  input:-moz-placeholder {
    color: #222;
  }
```