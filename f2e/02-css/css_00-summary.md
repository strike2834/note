# CSS 緒論

CSS（Cascading Style Sheets）是描述 HTML 或 XML 等文件外觀的樣式表語言。<br>
CSS 會定義文件裡的結構元素如何呈現在螢幕、語音閱讀或各種媒介上。

- [CSS Reference - A free visual guide to CSS](https://cssreference.io/)
- [Can I use... Support tables for HTML5, CSS3, etc](https://caniuse.com/)

## [現代 CSS 常見的基礎技術](https://qiita.com/arowM/items/e1af320e2755461649a0#%E7%8F%BE%E4%BB%A3%E7%9A%84%E3%81%AA%E4%BD%BF%E3%81%84%E3%81%8B%E3%81%9F%E3%81%AE%E5%9F%BA%E7%A4%8E)

1.  套用的對象差異：單頁網頁／網頁應用程式
2.  支援的瀏覽器差異
3.  分離文章構造與表現手法
4.  不使用行內樣式
5.  不使用表現手法命名 class
6.  使用 psuedo-class, wai-aria, custom data attribute 處理不同狀態下的樣式
7.  使用 modern reset, vender prefix 處理瀏覽器差異
8.  使用 transition, animation 處理動畫

### 層級

1.  基本層：一般就是 reset.css 或 normalize.css
2.  框架層：處理網頁整體框架的 css<br />
    └ 左右欄、全屏、上下左右區塊，有什麼東西都沒差
3.  元件層：處理單個 UI 元件的 css<br />
    └ 一個小按鈕，在哪裏都沒差
4.  狀態層：處理單個 UI 元件的狀態<br />
    └ 錯誤的樣子，按鈕也會出現錯誤的樣子，箱子也會。.
5.  模板層：只處理模板的 css，專屬於這個設計的 css<br />
    └ 一個小按鈕，在某個模板，我的按鈕比較不一樣

## 參考文章

- [竹白筆記本 - HTML & CSS 整理](https://hackmd.io/@chupai/Byo_VJu84/)
- [前端新手村](https://ithelp.ithome.com.tw/articles/10196272)
- [CSS SECRETS 筆記](https://hackmd.io/vs5zeSweTt-0AHM9iyyY_w?both)
- [Sass 學習筆記](https://hackmd.io/@chupai/BJASrHh9V/)
- [CSS 專家密技](https://github.com/AllThingsSmitty/css-protips/tree/master/translations/zh-TW)
- [CSS 黑魔法小技巧](https://github.com/jawil/blog/issues/29)
- [30 seconds of CSS](https://30-seconds.github.io/30-seconds-of-css/)
- [CSS Debugging Tips and Tricks](https://css-tricks.com/debugging-tips-tricks)
- [前端切版資源整理 - Dean 的前端 & 設計部落格](https://deanocean.github.io/2020/12/03/2020-12-03-%E5%89%8D%E7%AB%AF%E5%88%87%E7%89%88%E8%B3%87%E6%BA%90%E6%95%B4%E7%90%86/)
