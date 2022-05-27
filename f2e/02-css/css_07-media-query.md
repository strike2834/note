# 7. 媒體查詢

針對不同裝置，套用不同的樣式與適合閱讀的文字大小。

## RWD

```css
@media screen and (條件) and (條件) ... {
  // 判斷式，用在 screen 螢幕的媒體
}
```

以手機頁面呈現為優先設計，先在手機頁面中將圖片設定為 100%，<br />
平板或桌機尺寸再用 `display: flex` 或其他方式做排版。

如果先寫桌機版再用複寫的設定到手機版，對手機耗電量大，效能比較不好，<br />
所以都建議先從手機尺寸設計版面。

- 常用相關關鍵字<br />
  ├ all<br />
  ├ screen<br />
  ├ print<br />
  ├ Queries<br />
  ├ and<br />
  ├ not<br />
  └ only

```css
@media (max-width: 575.99px) {
  ...;
}
@media (min-width: 576px) and (max-width: 767.99px) {
  ...;
}
@media (min-width: 768px) and (max-width: 991.99px) {
  ...;
}
@media (min-width: 992px) and (max-width: 1199.99px) {
  ...;
}
@media (min-width: 1200px) {
  ...;
}
```

[Day22：小事之 Media Query](https://ithelp.ithome.com.tw/articles/10196578)

- 設定檢視區（Viewport）<br />
  `<meta name="viewport" content="width=device-width, initial-scale=1.0">`<br />
  使用 CSS3 Media queries @media 針對不同寬度的瀏覽器提供適合的頁面樣式
- 盡量使用相對寬度
- 使用流動性/比例式網格系統
- 五大外觀設計模式
  1. 主體為流動（mostly fluid）
  2. 欄內容下排（column drop）
  3. 版面配置位移（layout shifter）
  4. 微小調整（tiny tweaks）
  5. 畫布外空間利用（off canvas）
- 使用相對比例的響應式大小圖片與影片
- 使用 video 元素來載入、播放影片
- 使用多種格式的影片，以便在多種行動平台上播放
- 正確設定影片大小，確保你的影片不會超出容器
- 無障礙設計很重要：請為 video 元素新增 track 子元素

```html
<video controls>
  <source src="chrome.webm" type="video/webm" />
  <source src="chrome.mp4" type="video/mp4" />
  <p>Sorry, 您的瀏覽器並不支援 video 元素喔</p>
</video>
```
