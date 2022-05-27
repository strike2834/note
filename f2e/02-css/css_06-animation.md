# 6. 動畫／變形

## animation 動畫

CSS 的動畫共有 8 個 properties，而其中名稱與總播放時間為必須的，這 8 個 properties 分別為：

1. `animation-name`：此動畫的名稱
2. `animation-duration`：動畫完整播放所需時間，預設值為 0
3. `animation-timing-function`：動畫的速度曲線<br />
   └ 預設值為 ease（起始結束減速，中途加速）
4. `animation-delay`：動畫開始的時間點，預設值為 0<br />
   └ 可設為負值，負值意味動畫立即開始，並且提早結束
5. `animation-iteration-count`：動畫播放次數，預設值為 `1`<br />
   └ 可設為 `n（正整數）`或 `infinite`
6. `animation-direction`：動畫播放順序，預設值為 normal（正向播放）<br />
   ├ `normal`<br />
   ├ `reverse`<br />
   ├ `alternate`：奇數次正向播放，偶數次反向播放<br />
   └ `alternate-reverse`
7. `animation-play-state`：動畫播放狀態，預設值為 running（播放）<br />
   ├ `paused`<br />
   └ `running`
8. `animation-fill-mode`：動畫播放開始前或結束後的狀態，預設值為 none（回到初始狀態）<br />
   ├ `none`：動畫結束後立即回至開始前的狀態<br />
   ├ `forwards`：動畫結束後保持結束時的狀態<br />
   ├ `backwards`<br />
   └ `both`

並可簡寫成 `animation: 動畫名稱 播放時長 開始時間點 速度曲線 次數 順序 開始前結束後狀態 播放狀態（播放或暫停）`<br />
如：`animation: rotation 2s ease 0s 1 alternate none running;`<br />
但若在設定多重動畫等情況下，為了避免覆蓋到其他設定的動畫屬性，則不建議使用縮寫寫法

### animation-duration

- `animation-duration` 必須大於等於 0，負值無效
- 可使用整數或小數點，單位為秒（s）或毫秒（ms）
- 根據人類資訊處理模型，人類感知物件平均所需時間為 230ms（0.23s）<br />
  不同人的最短感知到最長感知時間落在 70ms 到 700ms 前後<br />
  簡單且重覆性高的動態效果（如選單），時間過長（如 600ms = 0.6s）會令人有冗長的感覺<br />
  設定在 250ms = 0.25s 前後較能讓人感受到動態，同時不會有等待的感覺

### animation-timing-function

- `animation-timing-function` 是由貝茲曲線（Cubic Bezier）構成的函數圖型
- CSS 有數個預先定義好的值，如 `linear`（線性）、`ease`（起始結束減速，中途加速）、`ease-in`（漸入）、`ease-out`（漸出）、`ease-in-out`（漸入漸出）...etc.
- Easing 還再分有 8 種強弱關建字：`Sine`、`Quad`、`Cubic`、`Quart`、`Quint`、`Expo`、`Circ`、`Back`，寫於預定函數之中<br />
  其中前 6 種裡 `Sine` 為變化最緩慢，到 `Expo` 變化最劇烈，後 2 種的 `Circ` 的餘韻比 `Expo` 再長一點，`Back` 則是會再反彈
- 亦可自行定義貝茲曲線的數值：`cubic-bezier(n1, n2, n3, n4)`，其值需為介於 0 至 1 之間的小數或整數
- 實際效果可以參照 [Easing 函數](https://easings.net/) 或是 [cubic-bezier(.17,.67,.83,.67)](https://cubic-bezier.com/#.17,.67,.83,.67)
- 除了貝茲曲線圖型外，亦可使用 [`steps()`](http://ghmagical.com/article/0gU2Wefas7hn) 做出跳躍的效果
- [【CSS アニメーション】transition のイージングに ease-in や ease-out を適当に設定するのはやめましょう - Qiita](https://qiita.com/s-kato/items/d5d1ceee9e2a28e02e6e)

## @keyframes

`animation` 只能定義單次的動畫，如果我們想要做出一連串的動畫變化效果，
也就是所謂的時間軸和關鍵影格時，我們就需要 `@keyframes`。時間軸有兩種寫法：

1. `from` -> `n%` -> `to`
2. `0%` -> `n%` -> `100%`<br />
   └ 基本上 `from` = `0%`，`to` = `100%`

```css
div:hover {
  animation: chloe 2s infinite;
}

@keyframes chloe {
  0% {
    // 也可以寫成 from {...}
    border-radius: 50%;
  }
  100% {
    // 也可以寫成 to {...}
    border-radius: 0%;
  }
}
```

亦可透過 Chrome DevTools 調整，要注意在 `@keyframes` 裡面寫 `!important` 是沒有效果的。

- [完整解析 CSS 動畫 ( CSS Animation )](https://www.oxxostudio.tw/articles/201803/css-animation.html)
- [CSS アニメーション 入門](https://qiita.com/soarflat/items/4a302e0cafa21477707f)
- [CSS アニメーションを使いこなすために知っておきたい 5 つのこと](http://qiita.com/nekoneko-wanwan/items/e8114c6e34d2950a7b28)
- [CSS プロパティのアニメーション](https://developer.mozilla.org/ja/docs/Tools/Performance/Scenarios/Animating_CSS_properties)
- [CSS アニメーションについて深く知る](https://qiita.com/yuki153/items/9aac0e5c8d7230a7bbe2)
- [[CSS アニメーション]三 ( 卍^o^ ) 卍 ← こいつのこれ → 卍を回したい](https://qiita.com/mame_hashbill/items/98118f4e7721a1ac30c9)

## transition 轉場

- `transition: 屬性 轉換時間 延遲執行動畫的時間 速度;`<br />
  └ 預設值為 `transition: all 300ms 0s ease;`
- `transition-property`：指定變動的參數
- `transition-duration`：開始至結束
- `transition-delay`：準備至開始
- `transition-timing-function`：指定 Easing

## transform

- [【CSS3】 Transform ( 変形 ) 関連のまとめ - Qiita](https://qiita.com/7968/items/eddfeb4b424d7c2d2d34)
- `transform` 可以用來移動、旋轉、縮放或傾斜元素
- 與 `transition` 或 `@keyframes` 一同使用可做出互動動畫效果
- 想同時套用多個效果時，使用空格連接即可<br />
  ├ `transform: translateX(20px) translateY(20px) rotate(30deg);`<br />
  ├ 套用的順序亦會互相影響，例如先套用傾斜和套用傾斜可能會有不同結果<br />
  └ 若個別記述多個 `transform` 時，只有最後一個會有效果
- `translate`：移動<br />
  ├ `translate(X軸移動距離, Y軸移動距離)`<br />
  ├ `translateX(X軸移動距離)`<br />
  ├ `translateY(Y軸移動距離)`<br />
  ├ `translateZ(Z軸移動距離)`<br />
  ├ `translate3d(X軸移動距離, Y軸移動距離, Z軸移動距離)`
- `rotate`：旋轉，使用 `deg` 單位<br />
  ├ `rotate(旋轉角度)`<br />
  ├ `rotateX(X軸旋轉角度)`<br />
  ├ `rotateY(Y軸旋轉角度)`<br />
  ├ `rotateZ(Z軸旋轉角度)`<br />
  └ `rotate3d(X軸旋轉向量, Y軸旋轉向量, Z軸旋轉向量, 旋轉角度)`
- `scale`：縮放，以 `1` 為比例基準<br />
  ├ `scale(數值, 數值)`<br />
  ├ `scaleX(數值)`<br />
  ├ `scaleY(數值)`<br />
  ├ `scaleZ(數值)`<br />
  └ `scale3d(數值, 數值, 數值)`
- `skew`：傾斜，使用 `deg` 單位<br />
  ├ `skew(X軸傾斜角度, Y軸傾斜角度)`<br />
  ├ `skewX(X軸傾斜角度)`<br />
  ├ `skewY(Y軸傾斜角度)`<br />
  ├ 由於計算方式的關係，`skew` 的順序不同會出現不同結果<br />
  ├ 範例：使用 `skew()` 做出斜邊效果<br />
  └ 想得出相同結果，建議改用 `matrix()`

<div class="emphasis-skew-border">
    Content here<br />
    content here<br />
    content here
</div>

<style>
  .emphasis-skew-border {
    position: relative;
    width: 160px;
    padding: 10px 20px;
    font-size: 20px;
    z-index: 0;

    color: #2e8def;
    background: #333333;
    border-bottom: 3px solid #2e8def;
  }

  .emphasis-skew-border:after {
    content: "";
    position: absolute;
    display: block;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    z-index: -1;

    background: #333333;
    border-bottom: 3px solid #2e8def;
    border-right: 20px solid #2e8def;

    transform-origin: bottom left;
    -ms-transform: skew(-30deg, 0deg);
    -webkit-transform: skew(-30deg, 0deg);
    transform: skew(-30deg, 0deg);
  }
</style>

```html
<div class="emphasis-skew-border">
  Content here<br />
  content here content here
</div>

<style>
  .emphasis-skew-border {
    position: relative;
    width: 160px;
    padding: 10px 20px;
    font-size: 20px;
    z-index: 0;

    color: #2e8def;
    background: #333333;
    border-bottom: 3px solid #2e8def;
  }
  .emphasis-skew-border:after {
    content: "";
    position: absolute;
    display: block;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    z-index: -1;

    background: #333333;
    border-bottom: 3px solid #2e8def;
    border-right: 20px solid #2e8def;

    transform-origin: bottom left;
    -ms-transform: skew(-30deg, 0deg);
    -webkit-transform: skew(-30deg, 0deg);
    transform: skew(-30deg, 0deg);
  }
</style>
```

### matrix

- `matrix`：結合上述四種變形的記述方式，亦是這幾種變形的實際實作方式
  - 使用 6 個參數的矩陣，進行轉換計算（即矩陣乘法）
  - `Matrix = translate * rotate * scale * skew`
  - `matrix(a, b, c, d, e, f)`
  - 數學上的對應記述為：
  ```
  a c e       x     a*x + c*y + e
  b d f   *   y  =  b*x + d*y + f
  0 0 1       1      0  +  0  + 1
  ```
- 轉換後的水平位置：`x(prevCoordSys) = ax + cy + e`
- 轉換後的垂直位置：`y(prevCoordSys) = bx + dy + f`
  - ex. `transform: matrix(1, 0, 0, 1, 100, 100);`
- 轉換後的水平縮放：`s*x = ax + cy + e`，`s` 為比例
- 轉換後的垂直縮放：`s*y = bx + dy + f`，`s` 為比例
  - ex. `transform: matrix(3, 0, 0, 0.5, 0, 0);`
  - `matrix(cosθ, sinθ, -sinθ, cosθ, 0, 0)`
- 轉換後的水平旋轉：`x(prevCoordSys) = x*cosθ - y*sinθ + 0`
- 轉換後的垂直旋轉：`y(prevCoordSys) = x*sinθ + y*cosθ + 0`
  - ex. `transform: matrix(0.866025,0.500000,-0.500000,0.866025,0,0);`
  - `matrix(1, tan(θy), tan(θx), 1, 0, 0)`
- 轉換後的水平傾斜：`x(prevCoordSys) = x + y*tan(θx) + 0`
- 轉換後的垂直旋轉：`y(prevCoordSys) = x*tan(θy) + y + 0`
  - ex. `transform: matrix(1,0,0.75,1,0,0);`

### matrix3d

- `matrix3d`：使用 16 個參數，以各列序優先排序<br />
  ├ `matrix3d(a1, b1, c1, d1, a2, b2, c2, d2, a3, b3, c3, d3, a4, b4, c4, d4)`<br />
  ├ `a1 b1 c1 d1 a2 b2 c2 d2 a3 b3 c3 d3` 標記線性轉換<br />
  ├ `a4 b4 c4 d4` 標記套用轉換<br />
  ├ 數學上的對應記述為：
  ```
    a1 b1 c1 d1       x       a1*x + b1*y + c1*z + d1
    a2 b2 c2 d2   *   y   =   a2*x + b2*y + c2*z + d2
    a3 b3 c3 d3       z       a3*x + b3*y + c3*z + d3
    a4 b4 c4 d4       1       a4*x + b4*y + c4*z + d4
  ```
- `transform-origin`：設定變形的錨定基準點<br />
  ├ `transform-origin: X軸位置 Y軸位置`<br />
  └ 2D 預設值為 `50% 50%`，3D 為 `50% 50% 0`
- `transform-style`：設定變形空間<br />
  ├ `flat`：2D 空間，此為預設值<br />
  ├ `preserve-3d`：3D 空間，想使用 3D 變形需設定此參數<br />
  └ 此屬性不會繼承，所有子元素皆需個別設定
- `perspective`：設定元素的透視距離，僅可套用於子元素上，單位為 `px`<br />
  └ `perspective: 遠近值`
- `perspective-origin`：指定 `perspective` 透視點，預設值為元素中心<br />
  ├ `perspective-origin: X軸位置 Y軸位置`<br />
  └ 可使用具單位的值，或 `left`、`center`、`right`、`top`、`center`、`bottom` 等位置單詞
- `transform: perspective()`：效果和 `perspective` 相同<br />
  ├ 但此設定會套用至所有已變形的 3D 空間子元素<br />
  └ 而 `respective` 是設定該元素的視覺深度
- `backface-visibility`：由於 HTML 元素有前後堆疊關係，即使在前方的元素變形（ex. `rotateY(180deg)`）仍然會蓋過後方的元素<br />
  └ 將此屬性設為 `hidden` 能讓位居前方的元素轉為背向時隱藏，預設為 `visible`

### clip-path

- `clip-path` 可以用來裁切元素，決定其顯示的形狀樣式
- 可以使用既有的 SVG 網址，或是內建的圖形 function 指定形狀
- `clip-path: <clip-source> | [ <basic-shape> || <geometry-box> ] | none`<br />
  ├ `clip-source`：SVG 圖形的 URL<br />
  ├ `basic-shape`：基礎圖形 function<br />
  │ 有 `circle`、`ellipse`、`polygon`、`inset` 等圖形可使用<br />
  │ 各個 function parameter 等詳細內容請參照 [CSS Shapes 規範](https://www.w3.org/TR/css-shapes-1/#typedef-basic-shape) 或 [CSS Shape Functions](https://oreillymedia.github.io/Using_SVG/guide/css-shapes.html)<br />
  ├ `geometry-box`：搭配 `basic-shape` 使用的設定參數，提供圖形參照用的盒模型設定<br />
  └ 例如使用 `margin-box`, `border-box`, `padding-box`, `content-box`...etc. 決定參照點
- 範例：`polygon(point1x point1y, point2x point2y, point3x point3y, point4x point4y)`<br />
  ├ 此例將第一個點的 `y` 向下平移了 `calc(var(--clip-padding) * 2`<br />
  └ 剩餘三點則為原本的角落端點，因此最終形狀為一個單斜邊四邊形

<div class="clip-path"></div>

<style>
:root {
    --width: 100vw;
    --full-width: 100vw;
    --magic-number: 0.09719;
    --skew-padding: calc(var(--width) * var(--magic-number));
    --clip-padding: calc(var(--full-width) * var(--magic-number));
}

.clip-path {
  position: relative;
  background-image: linear-gradient(
      rgba(0, 0, 0, 0.05) 50%,
      0,
      transparent 100%
    ), linear-gradient(-135deg, #0cc, #066);
  background-size: 0.5em 0.5em, 100% 100%;
  padding: calc(
      (var(--clip-padding) * 2) - (var(--clip-padding) - var(--skew-padding))
    ) 0 4em;
  clip-path: polygon(
    0% calc(var(--clip-padding) * 2),
    100% 0%,
    100% 100%,
    0% 100%
  );
  -webkit-clip-path: polygon(
    0% calc(var(--clip-padding) * 2),
    100% 0%,
    100% 100%,
    0% 100%
  );
}
</style>

```css
/* 
  CSS Tutorial: Create Diagonal Layouts Like It's 2020
  https://9elements.com/blog/pure-css-diagonal-layouts/ 
*/
.clip-path {
  position: relative;
  margin-top: calc((var(--clip-padding) * -1) - 2px);
  background-image: linear-gradient(
      rgba(0, 0, 0, 0.05) 50%,
      0,
      transparent 100%
    ), linear-gradient(-135deg, #0cc, #066);
  background-size: 0.5em 0.5em, 100% 100%;
  padding: calc(
      (var(--clip-padding) * 2) - (var(--clip-padding) - var(--skew-padding))
    ) 0 4em;
  clip-path: polygon(
    0% calc(var(--clip-padding) * 2),
    100% 0%,
    100% 100%,
    0% 100%
  );
  -webkit-clip-path: polygon(
    0% calc(var(--clip-padding) * 2),
    100% 0%,
    100% 100%,
    0% 100%
  );
}
```
