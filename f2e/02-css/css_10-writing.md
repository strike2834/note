# 10. 版型檢查

- [CSS 筆記、建議與指導方針總整理](https://github.com/doggy8088/CSS-Guidelines)
- [cssreference.io](https://cssreference.io/)
- [CSS Style Guides](https://dailydevlinks.com/css-style-guides/)
- [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)
- [Google が推奨する HTML/CSS のスタイルガイドについて](https://www.wan55.co.jp/column/detail/id=485)
- [文件、規範參考 - Material Design](https://wcc723.github.io/design/2018/10/20/design-guide/)
- [Google Material Design 正體中文版](https://wcc723.gitbooks.io/google_design_translate/content/index.html)
- [CSSLint の全 32 個のルールをサンプルコードを書きながら解説しました](https://qiita.com/oh_rusty_nail/items/12e5783a9630a6905b1e)

1.  類別階層不超過四層為原則
2.  不使用 ID，一律使用 class
3.  使用 OOCSS 建立類別工具庫
4.  使用 SMACSS 來建立 Sass 結構
5.  排版結構以 BEM 來開發
6.  導入 BS4 的 Grid System
7.  使用 Sass for 來管理擴充元件
8.  一率採用小駝峰式命名
9.  導入第三方插件在 Sass import vendor
10. 使用 REM 單位
11. 佈局使用 flexbox 進行元件設計

## 網頁兼容性

1.  跨瀏覽器（Chrome、Firefox、Edge）
2.  螢幕解析度（1920、1440、1280、1024、768、414、320）

## 可讀性

1.  class（`-`）或（`_`）自訂規則，注重大小駝峰寫法
2.  縮排與註解規則

## 擴充性

1.  具有元件化設計觀念（BEM、SMACSS 或自訂規則）
2.  不輕易影響主體架構（JS hooks）

## 重用性

1.  自訂 class 可在多處使用（OOCSS）
2.  無重複套用多餘 CSS

## 維護性

1.  整體結構是否清晰易懂（Sass import）
2.  整體風格一致性

## [移动开发之设计稿转换页面单位尺寸](https://blog.csdn.net/ww0908/article/details/72730267)

1.  設計稿的單位是 `px`，一般是 750px。
2.  `px`、`rem` 混用，`rem` 的 html `font-size` 用 16px。
3.  750px 的設計圖以 375 px 量長寬，<br />
    例如設計圖裡有一元素寬度是 100px，<br />
    那麼可得到寬度是 `(100px / 2) / 16px` = 3.125rem。
4.  根據裝置寬度不同，設定不同的 html 的 `font-size`。

## [為什麼使用 960px 切版？](https://qiita.com/terrierscript/items/fe6cc48ab98ffd6c55e2)

- 大多寬度上限是 1200px
- 容易讓廣告之類的側邊欄限制在 300px 左右
- 960px 更方便讓 grid system 計算

## [よりよい CSS を書くための、CSS / Sass (SCSS) 30 のルールとその理由](https://zenn.dev/kagan/articles/1aa466bb6ef8eb)
