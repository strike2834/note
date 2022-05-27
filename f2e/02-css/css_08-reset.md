# 8. Reset

由於 W3C 制定 HTML 與 CSS 規格時，沒有強制制定各家瀏覽器預設的 HTML tag 的 CSS 樣式，隨著各家瀏覽器的出現與改朝換代，常會出現同一個網頁在不同瀏覽器上出現差異，或是有相容性問題，因此有了為了解決這些問題的 CSS Reset，除了早期很常見的 Eric Meyer 版本之外，其他也有如 `Normalize.css` 之類的不同實作方式。CSS Reset 的使用亦須視情況而定，例如 Bootstrap 這類的 CSS 框架本身就已經有 `Normalize.css`，不需要再另外引入。

1.  [reset.css](https://meyerweb.com/eric/tools/css/reset/)<br />
    └ 將 margin 和 padding 全設為 0，並自行修改設定
2.  [normalize.css](http://necolas.github.io/normalize.css/)<br />
    └ 軟性統一瀏覽器規範、修正 Bug，提高可用性
3.  [sanitize.css](https://csstools.github.io/sanitize.css/)
4.  [ress.css](https://github.com/filipelinhares/ress)<br />
    └`link rel='stylesheet' href='https://unpkg.com/ress/dist/ress.min.css'`
5.  [A Modern CSS Reset](https://hankchizljaw.com/wrote/a-modern-css-reset/)
6.  [destyle.css](https://www.npmjs.com/package/destyle.css)

## Debug

有兩種好的 debug 框線做法：

1.  用 `outline`（用法和 `border` 一模一樣，但 `outline` 不佔空間）
2.  用 `box-shadow`
