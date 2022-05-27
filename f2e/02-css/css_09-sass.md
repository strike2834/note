# 9. Sass

SASS（Syntactically Awesome Style Sheets）是一種 CSS 的預處理器，<br />
擴充了 CSS 原本的特性，可以使用各種更簡潔的寫法，提高管理與撰寫的便利性，<br />
再透過編譯轉換成 CSS 檔案，例如下列各種功能：

- variables
- nesting（`&`）
- mixins
- functions
- operations
- `@include`
- `@extend`
- `@content`

目前變數也可以直接寫在原生 CSS 裡，並且除了常見的數值單位或純數值之外，也可以儲存關鍵字、字串或圖片網址，或是用於 `box-shadow` 或 `color` 這種具有一系列屬性的值，並且可以套用進各種 CSS function，但變數無法用來儲存動畫，仍然需要搭配如 Houdini 裡的 [CSS Properties and Values API](https://drafts.css-houdini.org/css-properties-values-api/) 來實作。

```scss
:root {
  --min: 1rem;
  --max: 4rem;
  --clamped-font-size: clamp(var(--min), 2.5vw, var(--max));

  --bullets: circle;
  --casing: uppercase;

  /* image from an external URL (PNG in this case) */
  --image-from-somewhere: url(https://codersblock.com/assets/images/logo.png);

  /* image from embedded data (SVG in this case) */
  --image-embedded: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 512 512'%3E%3Cpath d='M8 256c0 136.966 111.033 248 248 248s248-111.034 248-248S392.966 8 256 8 8 119.033 8 256zm248 184V72c101.705 0 184 82.311 184 184 0 101.705-82.311 184-184 184z'%3E%3C/path%3E%3C/svg%3E");
}

p {
  font-size: var(--clamped-font-size);
}

ul {
  list-style-type: var(--bullets);
  text-transform: var(--casing);
}

.a {
  background-image: var(--image-from-somewhere);
}

.b::after {
  content: var(--image-embedded);
}
```

## [7+1 Sass 設計模式](https://sass-guidelin.es/#the-7-1-pattern)

```
sass/
│
├ base/
│ ├ _reset.scss # Reset/normalize
│ ├ _typography.scss # Typography rules
│ └ ... # Etc…
│
├ components/
│ ├ _buttons.scss # Buttons
│ ├ _carousel.scss # Carousel
│ ├ _cover.scss # Cover
│ ├ _dropdown.scss # Dropdown
│ └ ... # Etc…
│
├ layout/
│ ├ _navigation.scss # Navigation
│ ├ _grid.scss # Grid system
│ ├ _header.scss # Header
│ ├ _footer.scss # Footer
│ ├ _sidebar.scss # Sidebar
│ ├ _forms.scss # Forms
│ └ ... # Etc…
│
├ pages/
│ ├ _home.scss # Home specific styles
│ ├ _contact.scss # Contact specific styles
│ └ ... # Etc…
│
├ themes/
│ ├ _theme.scss # Default theme
│ ├ _admin.scss # Admin theme
│ └ ... # Etc…
│
├ utils/
│ ├ _variables.scss # Sass Variables
│ ├ _functions.scss # Sass Functions
│ ├ _mixins.scss # Sass Mixins
│ └ _helpers.scss # Class & placeholders helpers
│
├ vendors/
│ ├ _bootstrap.scss # Bootstrap
│ ├ _jquery-ui.scss # jQuery UI
│ └ ... # Etc…
│
│
└ `main.scss` # Main Sass file
```

除了 SASS 之外，也有 LESS、Stylus 等等各種不同 CSS 預處理器語言。

## 編譯成 css

1. 於專案目錄底下建立 css 與 scss 資料夾
2. 安裝編譯套件：`npm install -D node-sass`
3. 在 `./package.json` 加上 `{ "scripts": { "sass": "node-sass scss/style.scss css/style.css" }}`<br />
   └ 執行 `npm run sass` 就會進行編譯<br />
   可再加上 `-output-style expanded` 可視化輸出 CSS 結構<br />
   └ 或 `-source-map true` 在使用開發工具時改為參照 Sass 檔案
4. 刪除多餘的檔案：`npm install -D rimraf`<br />
   │ 在 `./package.json` 加上 `{ "scripts": { "build": "npm run clean && npm run sass", "sass": "...", "clean": "rimraf css" }}`，<br />
   └ 執行 `npm run build` 就會先 clean 再編譯 sass
5. 監視自動編譯：`{ "scripts": { "watch": "npm run sass -- --watch", "build": "...", "sass": "...", "clean": "..." }}`<br />
   └ 執行 `npm run watch`
6. 加上前綴詞：`npm install -D postcss-cli autoprefixer`<br />
   │ 在 `./package.json` 加上 `{ "scripts": {}, "browserslist: [ ">= 1%", "ie >= 10"] }`<br />
   │ 指定對應國內 1% 以上使用率的瀏覽器和 IE10<br />
   └ 詳細的對應瀏覽器可以參照 https://browsersl.ist/
7. 在 `./package.json` 加上 `{ "scripts": { "watch": "...", "build": "npm run clean && npm run sass && npm run autoprefix", "clean": "...", "sass": "...", "autoprefix": "post css --use autoprefixer --map false --output css/style.css css/style.css" }, "browserslist": [ "..." ]}`<br />
   └ `npm run build` 就會以 clean -> sass -> autoprefixer 的順序執行

- [決断力を消耗しない Sass 開発環境構築](https://speakerdeck.com/bcrikko/set-up-sass-development-environment)
