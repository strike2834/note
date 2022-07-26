- [IE11とさよならしたら全力で使えるHTML/CSSまとめ【40個以上】](https://deep-space.blue/web/2263)

## 視覺、排版

- `backdrop-filter`
  - 模糊背景
  - `backdrop-filter: blur(20px) brightness(150%)`
- blend-mode
  - `mix-blend-mode`
  - `background-blend-mode`
- `conic-gradient`
  - 圓錐狀漸層
- `filter`
- `clip-path`
  - `shape-outside`
- `text-orientation`
- `text-stroke`
- `background-clip: text`
- `text-emphasis`
- `text-decoration`
- Variable fonts

## 響應式

- Grid Layout
- `line-clamp`
  - 隱藏超過指定行數內容
- `min()`, `max()`, `clamp()`
- `<picture>`
  - 依據環境顯示不同圖片
- `<wbr>`
  - 指定換行處

## 動畫

- `scroll-snap`
- `position: sticky`
  - `position: static` + `position: fixed`
- SVG SMIL animation
- APNG

## 便利屬性

- SVG `vector-effect: non-scaling-stroke`
  - 縮放 SVG 圖片時維持 stroke 粗細不變
- `<a>` download
  - 不開啟分頁直接下載內容
- `<details>`, `<summary>`
- `object-fit`, `object-position`
- `justify-content: space-evenly`
- `width: fit-content`
- `place-items`, `place-content`
- `display: contents`
  - 隱藏容器，並提昇底下的子元素
- `display: flow-root`
  - 解除子元素的 `float`
- `::marker` pseudo-element
- `:any-link` selector
  - 等同 `:link` 與 `:visited`
- CSS Variables
- list argument of `:not()`
- `:is()`
- `all`, `unset`, `revert`, `initial`
  - `all`: 設定所有屬性，例如指定為 `initial`
    - `all: initial;`
  - `initial`: 設為預設值
    - `font-weight: initial;`
  - `unset`: 若有繼承則設為繼承值，無則設為預設值
    - `font-weight: unset;`
  - `revert`: 設為使用者終端的設定值
    - `font-weight: revert;`
- Media query
  - `prefers-reduced-motion`
  - `prefers-color-scheme`
  - `interaction media features`
- `@support`
- `env()`

## 表格

- input type: `date`, `time`, `color` 與 `<meter>`
- 屬性: `minlength`, `capture` `inputmode`, `form`
  - `minlength`: 指定傳送內容的最小長度
  - `capture`: 於手機上改為啟動鏡頭
  - `inputmode`: 更改手機上的輸入鍵盤
  - `form`: 將 form tag 外的元素視為 form 的一部分
- `caret-color`: 輸入錨線的顏色
- `:read-only`
- `:in-range`, `:out-of-range`
- `:focus-within`
- `:default`
- `::placeholder`

## 其他

- `will-change`
- `font-display`
- `rel=noopener`
- Subresource Integrity
- ping 屬性