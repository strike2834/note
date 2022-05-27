# 1. 顯示與定位

CSS 將每個內容元素的外觀架構區分為 `Margin`、`Border`、`Padding`、`Content`，
也就是所謂的 Box Model（盒模型），並藉此實作出需求的版面配置、元素排列效果

## Box Model

- `Margin` 是容器外部（例如與其它容器之間）的留空距離，此空間是透明的
- `Border` 是將內容與 Padding 包圍住的外框
- `Padding` 是從容器到內容部份的留空距離，此空間是透明的
- `Content` 是容器內如文字、圖片等元素的內容部份

![box-model1](https://i.imgur.com/WG75USi.jpg)

![box-model2](https://i.imgur.com/UQ5tRfs.png)

關於詳細的內距與邊框數值計算準則，過往的瀏覽器使用 `border-box`，<br />
元素所設定的長寬（`height`、`width`）會為最終顯示結果，而內距、邊框都會向內計算

之後 W3C（World Wide Web Consortium，全球資訊網協會）制定了新的標準盒模型 `content-box`，<br />
並為目前的瀏覽器預設值，元素中的長寬和內距、邊框、外距皆獨立計算

而盒模型可以透過 `box-sizing` 屬性指定，目前多半還是使用 `border-box`

- [CSS Layouts](http://frontendlabepam.github.io/FL5/css-layouts/css-layouts.html#1)
- [段組みの CSS。](https://lopan.jp/css-layout2/)

## display

`display` 屬性可以指定元素具有何種排版特性

### 1. `block`

- 設定一元素為 `block-level`
- 佔滿整個容器寬度
- 可設定寬高

### 2. `inline`

- 設定一元素為 `inline-level`
- 寬高設定無效
- 可設定 padding 的左右值，上下值無效、無法被撐開

### 3. `inline-block`

- 同時擁有兩種 display 的特性，具有 `block` 的屬性，但不佔滿整個容器
- 可設定寬高，也可與其他元素並排
- 使用 `inline-block` 排板時，標籤如 `a` 或 `li` 之間會有空白字元，
- 需於父元素中設定字元大小為 0，再設定子元素的標籤文字大小。

### 4. `table`

（待）

### 5. `float`

- `float` 值會將該元素帶離原本的 normal flow，改為置於其容器的左方或右方
- 而文字或行內元素會循其區域換行，即常見的文繞圖／多欄編排效果
- 若一元素包含有 float 的子元素，其高度會變為 0（parent element collapsed）<br />
  之後的兄弟元素會因此覆蓋於其上方，造成跑版問題，需搭配 clearfix 處理

1. 無後續的兄弟元素時，設定在父元素上
2. 有後續的兄弟元素時，設定在兄弟元素上
3. 有後續的兄弟元素，亦可設定在父元素的虛擬元素上

```css
/* 
  1. overflow: hidden 
  設定於父元素
*/
.parent {
  overflow: hidden;
}

/* 
  2-1. clear: both 
  設定於鄰於父元素的兄弟元素
*/
.nextNonFloated_Element {
  clear: both;
}

/* 
  2-2. clear: both 
  設定於父元素的虛擬元素上
*/
.parent:after {
  content: "";
  visibility: hidden;
  display: block;
  height: 0;
  clear: both;
}
```

### 6. Flexbox

- 於 CSS3 新增的新排版模型
- 宣告底下的元素為 Flexbox 排版方式<br />
  會以母元素（容器，container）的中心處為基準<br />
  將定位點切為主軸（main axis，預設為橫排／`row`）<br />
  和次軸（cross axis，預設為直排／`column`）

![flexbox axis](https://i.imgur.com/S7QmP6M.png)

#### 容器屬性

- 於母元素／容器上，可以指定想要套用的子元素範圍，以及對齊的形式

##### `justify-content`

- 設定**所有子元素**於主軸（預設為橫排／X 軸）上要如何對齊
- CSS 裡還有 `justify-items` 和 `justify-self` 這兩個屬性，但在 Flexbox 裡沒有效果
- 5 種常用的對齊形式為：<br />
  ├ `flex-start`：對齊於軸線起點處<br />
  ├ `flex-end`：對齊於軸線終點處<br />
  ├ `center`：對齊於軸線中間<br />
  ├ `space-between`：平均分配內容空間，但開頭元素會貼齊於起點、結尾元素會貼齊於終點<br />
  └ `space-around`：平均分配內容空間，間距亦為平均分配

![flexbox justify-content](https://i.imgur.com/HZEA8ce.png)

##### `align-items`

- 設定**單行裡的元素**於次軸（預設為直排／Y 軸）上要如何對齊
- 5 種常用的對齊形式為：<br />
  ├ `flex-start`：對齊於軸線起點處<br />
  ├ `flex-end`：對齊於軸線終點處<br />
  ├ `center`：對齊於軸線中間<br />
  ├ `stretch`：撐滿整個軸線<br />
  └ `baseline`：對齊於內容基線

![flexbox align-items](https://i.imgur.com/exBQCBM.png)

##### `align-content`

- 設定**多行元素**於次軸上要如何對齊<br />
  └ `align-content` **只在多行內容才有效果**，控制的是**所有行**的對齊方式
- 6 種常用的對齊形式為：<br />
  ├ `flex-start`：對齊於軸線起點處<br />
  ├ `flex-end`：對齊於軸線終點處<br />
  ├ `center`：對齊於軸線中間<br />
  ├ `space-between`：平均分配內容空間，但開頭行會貼齊於起點、結尾行會貼齊於終點<br />
  └ `space-around`：平均分配內容空間，間距亦為平均分配<br />
  └ `stretch`：撐滿整個軸線

![flexbox align-content](https://i.imgur.com/SY0Cqju.png)

##### 容器設定

- `flex-direction`：設定容器主軸<br />
  ├ `row`：橫排<br />
  ├ `row-reverse`：橫排、反轉順序<br />
  ├ `column`：直排<br />
  └ `column-reverse`：直排、反轉順序

![flexbox flex-direction](https://i.imgur.com/BhhRsSp.png)

- `flex-wrap`：設定容器內容是否於寬度超過時換行<br />
  ├ `nowrap`：不換行<br />
  ├ `wrap`：換行<br />
  └ `wrap-reverse`：換行時反轉順序

![flexbox flex-wrap](https://i.imgur.com/ndWssPi.png)

- `flex-direction`、`flex-wrap` 可簡寫於 `flex-flow` 屬性內

#### 內容屬性

- `flex-grow`：分配剩餘空間，預設值為 `0`
- `flex-shrink`：收縮比，預設值為 `1`<br />
  `( 子項目寬*收縮比/總比值 ) * 超出值 = 扣除值`<br />
  若設為 0 則由 basis 與 grow 進行計算
- `flex-basis`：控制主軸長度（主軸為衡=寬度 width，主軸為縱=高度 height）<br />
  權重比 width 和 height 大
- `flex-grow`、`flex-shrink`、`flex-basis` 可簡寫於 `flex` 屬性內
- `order`：設定元素所處順序，各個元素的預設值為 0<br />
  設定其中一個元素為 1 就會移到最右邊（其它為 0）<br />
  設定為 -1 則會移到最左邊
- `align-self` 內容屬性可再獨立設定於次軸上的對齊位置，設定此屬性後母容器的 `align-items` 則會無效

### 7. Grid

- 以二維的方式定位的模型
- grid 並非用於取代 flexbox，而是補足 flexbox 的不足
- 需先使用 `display: grid` 定義主容器顯示類型，再用 `grid-template` 定義版型結構
- [CSS Grid Generator | LayoutIt!](https://grid.layoutit.com/)

#### 宣告長寬

- `grid-template-columns`：宣告每行 （橫列）的寬度，劃分出 Y 軸線
- `grid-template-rows`：宣告每列（直列）的高度，劃分出 X 軸線
- 寬高可使用空行區隔，用以指定每行／列內的各空間寬度
- 亦可使用 `repeat(4, 2rem)` 一次建立 4 行 2rem 寬度的空間<br />
  `repeat()` 內還可使用 `auto-fill` 填滿所有空間，或 `auto-fit` 填滿至指定空間
- 也可以使用 `grid-auto-columns`、`grid-auto-rows` 快速指定版型<br />
  ex：`grid-auto-columns: 60px;`

##### 長寬單位

- `fr` 是總數比例單位，例如 `grid-template-columns: 1fr 1fr 2fr;` 是宣告每欄寬度為 1/4、1/4、2/4
- `max-content` 取得容器最大尺寸的空間，當成填充條件<br />
  `min-content` 取得容器最小尺寸的空間，當成填充條件<br />
  `minmax ( min, max )` 以最小尺寸 `min` 定義，最大尺寸需小於或等於 `max`
- `auto` 自動設定空間尺寸，上述寬高指定也可以混用<br />
  ex：`grid-template-columns: 1fr min-content minmax ( 100px, max-content ) ;`

#### 分配元素

- `grid-auto-flow`：宣告 Grid 的排列方式<br />
  ├ 預設為 `row` 先欄後列<br />
  └ 還有 `column` 先列後欄、 `dense` 自動填滿
- `grid-template-areas`：定義主容器裡各區塊的位置與名稱，可使用 `.` 略過某區塊不指定

```css
.example {
  grid-template-areas:
    "header header header header header"
    "side main main main main"
    "side footer footer footer footer";
}
```

- `grid-area`：指定區塊名稱，並配置至對應位置
- `grid-area` 的區塊必須是連接在一起的，即不可一個區塊名稱分散於兩側位置，並且只能是矩形
- `grid-gap`：區域之間的距離，可省略前面的前綴 `grid-`<br />
  ├ `grid-gap: { grid-row-gap } { grid-column-gap };`<br />
  ├ `grid-column-gap: { grid-column-gap };`<br />
  └ `grid-row-gap: { grid-row-gap };`

#### 區塊

- `grid-column: <起始 column-num> / <結束 column-num>`：宣告區塊定位自己位置
- `grid-row: <起始 row-num> / <結束 row-num>`：宣告區塊定位自己位置
- `justify-self`，`align-self`：同 `flexbox` 用法

#### 其它 grid 參考資料

- [GRID: A simple visual cheatsheet for CSS Grid Layout](https://grid.malven.co/)
- [A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [關於 Grid Layout 的使用姿勢](https://blog.hinablue.me/css-grid-layout/)
- [CSS Grid | 剛學會怎麼用 Grid，那就來畫個 TV 檢驗圖練練手吧！- 手寫筆記 - Medium](https://medium.com/%E6%89%8B%E5%AF%AB%E7%AD%86%E8%A8%98/using-css-grid-to-draw-test-card-7ed24d3559ab)
- [CSS | 所以我說那個版能不能好切一點？- Grid 基本用法 - Enjoy life enjoy coding - Medium](https://medium.com/enjoy-life-enjoy-coding/css-%E6%89%80%E4%BB%A5%E6%88%91%E8%AA%AA%E9%82%A3%E5%80%8B%E7%89%88%E8%83%BD%E4%B8%8D%E8%83%BD%E5%A5%BD%E5%88%87%E4%B8%80%E9%BB%9E-grid-%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-cd763091cf70)

### 8. 其它 display 屬性

- `none`：清除此元素<br />
  └ 此屬性值常與 `visibility: hidden` 相提並論

設定為 `display: none` 的元素在 DOM 和 CSSOM trees 結合後的 Render Tree 中不會產生對應的盒模型，故不佔有任何排版空間，但仍然存在於 DOM Tree 上，可以進行相關操作

而 `visibility: hidden` 的元素仍然會保留其 box，因此雖然內容不可視，仍會佔有空間

- `inherit`：繼承父元素的 display 屬性值
- `initial`：該元素的預設屬性值
- `unset`：等同於 `inherit` 和 `initial` 的組合值<br />
  ├ 若該屬性預設為繼承，此值等同 `inherit`<br />
  └ 若該屬性預設為不可繼承，此值等同 `initial`

## overflow

`overflow` 可以決定當內容超過容器尺寸時如何呈現，可設定為：

- `visible`：內容全部可見、會全部渲染至超出容器、可能與其它內容重疊
- `hidden`：隱藏超出容器部份的內容
- `auto`：替超出容器部份的方向加上捲動軸
- `scroll`：無論內容是否超出容器，加上捲動軸

## position

### 1. `static`

- 預設定位，依照 document flow 決定

### 2. `relative`

- 相對，保留原始空間，自初始座標進行偏移
- 有定位的物件的 `z-index` 會優先於沒有定位的元素
- 如果兩個都有定位，位於原始碼後方的元素會蓋過前方的元素

### 3. `absolute`

- 絕對，類似於 `fixed`，獨自獨立一層
- 當一個物件設定為絕對定位，會去父層尋找非 `static` 的元素定錨
- 首個有定位的父層元素，會成為元素絕對定位位置的座標依據<br />
  └ 如果沒有，預設會定位在**瀏覽器視窗上** （注意，不是 `body` 也不是 `html`）
- 不同於 `fixed`，預設只會定位一次，拉動捲軸會跟著捲軸跑，不會固定在視窗上

### 4. `fixed`

浮動，以瀏覽器視窗為定位，固定於視窗範圍內<br />
├ 將 `top`、`left`、`right`、`left` 都設為 0，<br />
│ `margin` 設定為 `auto`，元素就會在瀏覽器正中間。<br />
├ `fixed`、`absolute`、`float` 與 `flex` 底下的元素皆預設為不會自動抓取空間寬度，<br />
└ 因此設定寬度後會取得所在空間寬度並與空間等寬。

### 5. `sticky`

邊界，（待）

### 6. `z-index`

- `z-index` 非 `display` 的值，而是另一個獨立的屬性
- 用於決定非 `static` 的元素圖層關係，預設值為 `0`
- `z-index` 值越高的元素會位於圖層的越前方

![z-index](https://i.imgur.com/LBE29Hq.png)

### 如何運用 display 與 position 做出置中效果

- [23 種 CSS 垂直置中技巧](http://csscoke.com/2018/08/21/css-vertical-align/)
- [連續 30 天的超實務網頁設計的垂直置中教學](https://ithelp.ithome.com.tw/users/20112550/ironman/2092)

## vertical-align

（待）
