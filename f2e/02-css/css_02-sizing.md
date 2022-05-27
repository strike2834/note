# 2. 尺寸

![box-model2](https://i.imgur.com/UQ5tRfs.png)

1.  `height`：高度
2.  `width`：寬度
3.  `padding`：內間隔
4.  `margin`：外間隔

- `padding` 和 `margin` 的值設為 `auto` 時，其值等同 `母元素的長寬度 - 當前元素的長寬度`
- [フロントエンドのプロ直伝！CSS 余白設定の三原則 ( ＋線の引き方 )](https://qiita.com/yama-t/items/da7740769cfc0f8446a0)
- [\[30 道難解的 CSS 排版\] 第 1 道：認識對齊 I](https://ithelp.ithome.com.tw/articles/10213624?sc=hot)

## 避免邊界重疊（Margin Collapsing）

當兩個 block 都有設定上下的 margin，並且這兩個 margin 相鄰時，<br />
最終計算結果會只留下較大邊的 margin，造成 margin collapsing

### 「相鄰」可以再細分為三種情況

1. 於**同一層內相鄰**時，設定 margin 造成的上下 margin 相鄰
2. **父元素**與第一個**子元素**或最後一個子元素，設定 margin 造成的上下 margin 相鄰
3. **兩個元素之間存在空元素**時，此兩個元素設定 margin 造成的上下 margin 相鄰

```html
<!-- 兩個元素的 margin 會重疊，實際上只剩下 16px 的 margin -->
<section>
  <!-- 同一層內相鄰 -->
  <div class="block mb-16">margin-bottom: 16px</div>
  <div class="block mt-16">margin-top: 16px</div>
  <!-- 父元素與子元素 -->
  <div class="block mb-16 mt-16">
    <div class="block mt-16">parent and child both margin-top: 16px</div>
    <div class="block mb-16">parent and child both margin-bottom: 16px</div>
  </div>
  <!-- 中間存在空元素 -->
  <div class="block mb-16">margin-bottom: 16px</div>
  <div></div>
  <div class="block mt-16">margin-top: 16px</div>
</section>

<style>
  .mt-16 {
    margin-top: 16px;
  }

  .mb-16 {
    margin-bottom: 16px;
  }
</style>
```

- Codepen：[Margin Collapsing](https://codepen.io/f6bfb5/pen/NWRoRNB)

### 如何解決 margin collapsing

通用解：可以改為使用 `padding`，或是設定父元素為 `block` 以外的 model<br />
（發生於兄弟身上時則指其共通的父元素，於父子身上時則指該父元素）

第 2 種情況可以替父元素設置 `overflow: hidden`、`padding`、`border` 或 `float` 來解決<br />
（但 `float` 需要設定其寬度與另外加上 `clearfix` 元素）

### 不會發生 margin collapsing 的情況

- 水平相鄰的元素（左右 margin）
- root 元素
- 兩個 block 由 `padding`、`border` 或 inline box、clearance 隔開
- `float` 元素的兄弟、父子
- `position: absolute;` 元素的兄弟、父子

### 參考資料

- [Css 系列 - 如何避免邊界重疊 ( Margin Collapsing )](https://github.com/marshal604/blog/issues/6)
- [Day23 CSS：Collapsing margins](https://ithelp.ithome.com.tw/articles/10225741)
- [話說 Margin-collapse 是什麼呢？](https://ithelp.ithome.com.tw/articles/10219975)

## 單位

- [一次搞懂 CSS 字體單位：px、em、rem 和 %](https://www.oxxostudio.tw/articles/201809/css-font-size.html)
- [CSS: em, px, pt, cm, in…](https://www.w3.org/Style/Examples/007/units.zh_HK.html)
- [CSS Ruler](https://katydecorah.com/css-ruler/)
- 速算：`100%` = `1em` = `1rem` = `16px` = `12pt`
- 螢幕內容列印時的單位轉換：`Pixel` → `inch` → `dot`
- 螢幕內容顯示時的單位轉換：相對單位 → `px` → （ppi） → `inch` → 絕對單位<br />
  （`1inch` = `2.54cm` = `25.4mm` = `72pt` = `6pc`）

1.  `px`（pixel，像素）：絕對值<br />
    ├ `pixel` 是種圖像元素單位，沒有具體的長寬值，實際尺寸隨顯示器的解析度與寬度改變<br />
    └ 於同一顯示器裡，像素的尺寸不會隨著瀏覽器視窗長寬或是網頁內容改變
2.  `%`：相對值，參照 `母元素`，視其母元素為 100%
3.  `em`：相對值，參照 `當前元素`，視當前元素的字體大小為 1em
4.  `rem`：相對值，參照 html 根元素 `<html>`，視根元素的字體大小為 1rem<br />
    └ 瀏覽器的預設字體大小為 `16px`，因此通常 `1rem` = `16px`
5.  `vw`：相對值，參照 `瀏覽器畫面寬度`，視畫面寬度為 100vw<br />
    └ 語法上省略了中間的 `%` 符號，其中的 `v` 為從 viewport（視口）而來，
6.  `vh`：相對值，參照 `瀏覽器畫面高度`，視畫面寬為 100vh
7.  `vmax`：相對值，目前 `vw` 和 `vh` 兩者之中比較大的值
8.  `vmin`：相對值，目前 `vw` 和 `vh` 兩者之中比較小的值
9.  `ex`：相對值，等同於第一個可用字體裡的「x 文字的高度」<br />
    └ 但在不包含 x 文字的字體之中亦會定義此單位，通常用於以文字為重的設計中
10. `calc()`：可在表達式中進行計算，指定較為複雜的動態數值<br />
    └ 上述的單位皆可用於此計算中
11. `max()`：選取表達式中最小的值<br />
    │ 例如 `width: min(1vw, 4em, 80px);` 的最大寬度是 80px，<br />
    └ 當視口小於 800px 或 1em 小於 20px 時，就會選擇更小的值。
12. `min()`
13. `clamp()`

### 關於 `%` 參照基準的一些小細節

- [What does 100% mean in CSS?](https://wattenberger.com/blog/css-percents)

我們會很直覺地認為，當一個元素使用 `%` 指定 `height` 或 `width` 時，參考的基準點就是母元素的對應屬性<br />
（換句話說，`height: 50%` 看起來是母元素高度的一半，而 `width: 25%` 是母元素寬度的四分之一）。

但當我們用在 `margin-top`（和 `margin-bottom`）時，會發現 `margin` 與 `padding` 參照的<br />
都是**母元素的寬度**，而不是依據方向決定取用高度或寬度。

以及 `transform` 裡的 `translate` 使用 `%` 時，會參照的是**元素自身的寬度或高度**，<br />
例如 `transform: translate(0%, 100%)` 會向下移動等同元素自身高度的距離。

總合這些特性可以得知，當我們想要垂直置中一個元素，並且不想要因為其大小改變而跑版時，<br />
我們會設置 `top: 50%; left: 50%;`<br />
（元素以左上角為錨點，移動母元素一半的長寬＝母元素的中心處），<br />
再使用 `transform: translate(-50%, -50%)`<br />
（往回移動元素自身一半的長寬，補回因為基準點在左上而需要的距離差）來達成。
