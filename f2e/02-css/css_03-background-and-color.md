# 3. 背景、色彩

## 背景

1.  `background-color`
2.  `background-image`
3.  `background`<br />
    ├ `background: color image attachment repeat poition / size`<br />
    ├ 各值都可忽略，僅 `background-position` 與 `background-size` 擁有相依關係<br />
    │ 有 `background-position` 時，可以不必加上 `/`<br />
    │ 有 `background-size` 時，一定要加上 `/` 以及 `background-position`<br />
    ├ `linear-gradient(顏色漸變方向角, 色碼 1, 色碼 2);`<br />
    └ `radial-gradient(ellipse 或 circle, 顏色 1, 顏色 2) ;`
4.  [`background-position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-position)

### 疊加效果

1. `filter`：設定套用於此元素的濾鏡效果
2. `backdrop-filter`：設定套用於此元素背後的所有元素的濾鏡效果
3. `mix-blend-mode`：設定此元素如何與此元素的背景和直屬父元素的內容混合
4. `background-blend-mode`：設定此元素的背景圖片和背影顏色如何混合

## 色彩

- [エンジニアのための配色まとめ](https://qiita.com/maccotsan/items/d51c992a20385427e689)
- [プログラマが知っているとよい色使い ( 安全色 ) とカラーユニバーサルデザイン](https://qiita.com/kaizen_nagoya/items/cb7eb3199b0b98904a35)
- [RGB、HSL、Hex 網頁色彩碼，看完這篇全懂了](http://csscoke.com/2015/01/01/rgb-hsl-hex/)
- [Web 開發者需要瞭解的基礎色彩理論](https://juejin.im/post/5c6caee26fb9a049df24a4df)
- [Beginning Graphic Design: Color](https://www.youtube.com/watch?v=_2LLXnUdUIc)

### 三原色

- RGB
- 以 R 在上方順時鐘排列

### 第二次色

- 印表機的 CMYK（藍、洋紅、黃）三色
- 由 RGB 中間色產出的混合色
- 以 C 在下方同呈順時鐘排列

### 色相環

- 色相 Hue<br />
  ├ 顏色<br />
  └ 0 度為 R（紅）色，120 度為 G（綠）色，240 度為 B（藍）色
- 飽和度 Saturation<br />
  ├ 顏色的強度，即顏色的濃淡、鮮豔度<br />
  └ 不同於明度於飽和度降低後，為接近灰色而不是黑色。
- 明度 Lightness<br />
  ├ 顏色從黑到白的明暗程度<br />
  └ 一般 HSL 色彩的 L 預設值會為 50%，調暗往 0% 調整，調亮往 100% 調整。

HSL 色彩寫法為 `HSL (色相角度不加單位 0~360, 色彩飽和度 0~100%, 色彩亮度 0~100%)`。

### 十六進位色彩

- [Hex colors](https://www.colorhexa.com/)

### 色彩調和

- [色彩懶人包](https://www.facebook.com/100002580605815/posts/1985346691561332/?d=n)
- 單色系公式（Monochromatic）<br />
  使用飽和度與明度創造變畫，一定能創造出和諧的配色組合
- 類似色系（Analogous）<br />
  運用色相環上鄰近的顏色配對<br />
  例如紅橘或冷色調的藍綠
- 補色系（Complementary）<br />
  色相環上位於相對面位置的兩個顏色，例如藍橘或經典的紅綠，<br />
  避免過於單調可以加入明暗或濃淡的變化
- 補色分割法（Split Complementary）<br />
  使用互補色左右兩邊的顏色來做搭配，提供同程度的對比但更多的顏色組合
- 三等色法（Triadic）<br />
  色相環上正三角型的三個顏色，組合通常非常顯眼，特別適用三原色或二次顏色時，需小心使用
- 矩形配色法（Tetradic）<br />
  互用兩組補色做配對，有一為主色時能達到最好效果

### 易看的色彩

- [色による「見やすさ」のデザイン](http://creator.dwango.co.jp/13693.html)
- [伝わるデザイン - 配色](https://tsutawarudesign.com/miyasuku5.html)
- [印刷物の可読性に対する背景色及び年齢・照度の影響](https://www.jstage.jst.go.jp/article/jcsaj/41/3+/41_163/_pdf)
- [視認性・可読性の確保](https://www.webcolordesign.net/color_point/usability/readable_color.html)
- [視認性と可読性](http://creator-index.com/2015/01/729/)
- [Colour Contrast Analyser (CCA)](https://developer.paciellogroup.com/resources/contrastanalyser/)
- [同彩度でも配色次第で文字色を反転させる境目が違う気がする](https://twitter.com/shin_5_9/status/1289752572480196608)

### 網頁安全色

- [Web セーフカラー　カラーコード一覧](https://qiita.com/yuma_h/items/13989334fc7a6d016ea5)

## 邊框

### `border`

- 邊框線
- `border: border-width border-style color;`<br />
  ├ 順序無強制限制<br />
  ├ -width: `<length>`, `thin`, `medium`, `thick`<br />
  ├ -style: `solid`, `none`, `hidden`, `dashed`, `dotted`, `double`, `groove`, `ridge`, `inset`, `outset`<br />
  └ color: `rgb()`, `rgba()`, `hsl()`, `hsla()`, `<hex-color>`, `<named-color>`, `currentcolor`
- 可以搭配 `border-radius` 做出圓角框線效果

<div class="ml-2rem w-fit p-8 bd bdrs">圓角框線效果</div>

<style>
.ml-2rem {
  margin-left: 2rem;
}

.w-fit {
  width: fit-content;
}

.p-8 {
  padding: 8px; 
}

.bd {
  border: 1px solid black; 
}

.bdrs {
  border-radius: 16px; 
}
</style>

- `border` 本身具有空間，在使用時須注意計算<br />
  ├ 用於動畫時，可以設定為 `hidden`，或是設定初始顏色為透明色解決空間問題<br />
  └ 因為四邊 `border` 會彼此交疊，此特性可用於無長寬的虛擬元素來製作圖形
- [CSS だけで三角・矢印を作る方法](https://design.webclips.jp/css-arrow/)

  ```css
  .message-box::after {
    content: "";
    border: 10px solid transparent;
    border-top-color: #00cc99;
  }
  ```

- 對話框效果：

<div class="bubble01">對話框效果範例 1</div>

<style>
  .bubble01 {
    position: relative;
    display: inline-block;
    width: 200px;
    text-align: center;
    color: #fff;
    padding: 25px;
    margin-left: 2rem;
    background-color: #f39800;
    border-radius: 5px;
  }
  .bubble01:before {
    content: "";
    position: absolute;
    display: block;
    z-index: 1;
    border-style: solid;
    border-color: #f39800 transparent;
    border-width: 10px 10px 0 10px;
    bottom: -10px;
    left: 50%;
    margin-left: -10px;
  }
</style>

```css
.bubble01 {
  position: relative;
  display: inline-block;
  width: 200px;
  text-align: center;
  color: #fff;
  padding: 25px;
  background-color: #f39800;
  border-radius: 5px;
}
.bubble01:before {
  content: "";
  position: absolute;
  display: block;
  z-index: 1;
  border-style: solid;
  border-color: #f39800 transparent;
  /* 只有上、右、左有邊框（空間），左右邊框為透明色
  因此最後會變為尖端朝下的小三角形 */
  border-width: 10px 10px 0 10px;
  bottom: -10px;
  left: 50%;
  margin-left: -10px;
}
```

<div class="bubble02">對話框效果範例 2</div>

<style>
.bubble02 {
  position: relative;
  display: inline-block;
  width: 200px;
  text-align: center;
  color: #fff;
  padding: 25px;
  margin-left: 2rem;
  background-color: #f39800;
  border-radius: 5px;
}

.bubble02:before {
  content: "";
  position: absolute;
  display: block;
  z-index: 1;
  border-style: solid;
  border-color: #f39800 transparent;
  border-width: 20px 20px 0 0;
  bottom: -20px;
  left: 50%;
  margin-left: -10px;
}
</style>

```css
.bubble02 {
  position: relative;
  display: inline-block;
  width: 200px;
  text-align: center;
  color: #fff;
  padding: 25px;
  background-color: #f39800;
  border-radius: 5px;
}

.bubble02:before {
  content: "";
  position: absolute;
  display: block;
  z-index: 1;
  border-style: solid;
  border-color: #f39800 transparent;
  /* 只有上、右有邊框（空間），左、下無邊框，右邊框為透明色
  因此最後會變為直角在左上的等邊三角形 */
  border-width: 20px 20px 0 0;
  bottom: -20px;
  left: 50%;
  margin-left: -10px;
}
```

### `outline`

- 外框線
- `outline: outline-width outline-style color;`<br />
  └ 順序無強制限制
- `outline` 不佔有空間
- 只有矩形外觀，無法改變視覺效果

### `box-shadow`

- 陰影
- `box-shadow: horizonalOffset verticalOffset blurRadius optionalSpreadRadius color`
- `box-shadow` 也不佔有空間
