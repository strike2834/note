# Body Tag

## 構成元素

- `<tagName attributeName="attributeValue">Content</tagName>`
- [tagName](https://www.w3schools.com/tags/ref_byfunc.asp)
- [attributeName](https://www.w3schools.com/tags/ref_standardattributes.asp)
- `class` 與 `id` 是兩個相當常見的 attribute
  - `class` 通常是用於可重複使用的 css 分類命名
  - `id` 通常用於 JS 中抓取該元素的辨識方式<br />
    ├ 一個元素僅可有一個 id<br />
    └ 建議留給程式開發／網頁規劃使用

## 常見標籤

- `div`：區塊容器
- `h1`, `h2`, `h3`, `h4`, `h5`, `h6`：各級標題
- `p`：文字段落
- `span`：行內文字
- `a`：連結
- `ol`：有序清單
- `ul`：無序清單
- `img`：圖片
- `audio`：聲音
- `video`：影片
- `canvas`
- `details`, `summary`：可折疊內容
- `dd`, `dl`：定義清單
- `code`：程式碼段落

## Table 表格

```html
<table>
  <thead>
    <tr>
      <th>Table Row 1 Table Head</th>
      <th>Table Head 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Table Row 2 Table Data</td>
      <td>Table Data 2</td>
    </tr>
  </tbody>
</table>
```

- `<table>`：表格容器
- `<thead>`, `<tbody>`：表格標頭與內文容器
- `<tr>`：表格行
- `<th>`：標頭內容
- `<td>`：資料內容

## Form 表單

```html
<form id="form" name="form" action="">
    <input id="toggle1" type="checkbox">
    <label for="toggle1">Toggle me!</label>
    <input id="toggle2" type="checkbox">
    <label for="toggle2">Toggle me!</label>
    <input id="toggle3" type="checkbox">
    <input for="toggle3">Toggle me!</label>
</form>
```

`<form>` 為用來配置輸入與傳輸資料用的表單範圍，建立表單用的基礎元素。

其屬性有

- `action`：必備，傳送資料的目標 URL
- `method`：傳送資料的 HTTP 方式，常見值為 `get` 與 `post`<br />
  ├ `get`：預設值，以 URL 形式傳送表單<br />
  │ 適用於短表單（搜尋框）或從伺服器取得資料<br />
  ├ `post`：以文本資料形式傳送表單<br />
  │ 適用於使用者上傳、長表單、包含敏感性資料（如密碼）、增刪資料庫內容<br />
  ├ `put`：修改<br />
  └ `delete`：刪除
- `enctype`：適用於 `metod` 設定為 `post` 時，指定表單內傳送資料的類型（MIME）為何<br />
  ├ 可被 `button` 或 `input` 元素裡的 `formenctype` 屬性複載<br />
  ├ `application/x-www-form-urlencoded`：預設值<br />
  └ `multipart/form-data`：用於含有檔案傳送欄位（`inputtype="file"`）時必須設定
- `name`：表單識別用的名稱，建議與 `id` 一同使用
- `novalidate`：設定表單
- `target`：設定如何開啟 `action` 屬性的目標 URL<br />
  ├ `self`：預設值，於同分頁裡載入返回值<br />
  ├ `blank`：於新視窗載入<br />
  ├ `parent`：於父框架內載入，若無父元素則同 `self`<br />
  ├ `top`：在當前文件檔裡的最高元素內載入，若無父元素則同 `self`<br />
  └ `framename`：指定於何框架載入
- `autocomplete`：設定是否自動完成表單內容<br />
  ├ `on`：可根據輸入歷史紀錄自動輸入<br />
  └ `off`：瀏覽器不會自動輸入

## Input 輸入

- `<input>` 元素用來配置表單內的輸入欄位

### type

- 可以使用 `type` 屬性來配置各種不同類型的輸入欄位
- `type` 可用 3 種類型分類： 1. 按鈕、2. 輸入欄位、3. 其它

#### 1. 按鈕：

- `submit`：傳送表單
- `rest`：重設表單
- `button`：通用按鈕
- `image`：圖片式傳送按鈕

#### 2. 輸入欄位：

- `text`：單行文字
- `search`：搜尋關鍵字
- `tel`：電話
- `url`：網址
- `email`：電子信箱
- `password`：密碼
- `datetime`：UTC 日期時間
- `datetime-local`：本地日期時間
- `date`：日期
- `month`：月份
- `week`：星期
- `time`：時間
- `number`：數值
- `range`：範圍
- `color`：顏色

3. 其它：

- `checkbox`：複選方塊
- `radio`：單選按鈕
- `file`：檔案選擇
- `hidden`：隱藏欄位

### inputmode

- 可以使用 `inputmode` 屬性指定行動裝置上虛擬鍵盤的配置模式
- `none`：不顯示鍵盤
- `text`：預設鍵盤，視使用者語系決定
- `url`：網址，將底下替換為 `.`、`/`、`.com`
- `email`：電子信箱，將底下替換為 `space`、`@`、`.`
- `numeric`：整數，不包含任何數值符號
- `search`：搜尋功能，會將 `回傳／傳送` 鍵替換為 `搜尋`，並可能有加上相關符號
- `tel`：電話號碼，除了 `0-9` 之外還有 `*` 和 `#`
- `deciaml`：小數，會再有 `.` 或 `,` 這類可以標記小數的符號

### 其餘 input 屬性

- `name`：欄位識別用的名稱，建議與 `id` 一同使用。
- `value`：欄位預設值，`checkbox` 與 `radio` 類型的欄位此屬性不可為空。
- `maxlength`：指定欄位寬度，若為文字類型欄位則此數值為文字字數寬度，其於則為像素寬度。
- `checked`：設定該欄位為已選定，使用於 `checkbox` 與 `radio` 欄位。
- `disabled`：設定該輸入欄位不可使用。
- `readonly`：設定該輸入欄位不可變更。
- `src`：使用於 `image` 欄位，設定圖片來源網址。
- `alt`：使用於 `image` 欄位，設定圖片無法顯示時的替代文字。
- `align`：使用於 `image` 欄位，設定圖片與文字的排列方式。
- `tabindex`：設定當按下 Tab 鍵時，項目移動的順序，會從屬性值最小者開始移動。
- `accesskey`：設定快捷鍵文字。
- `accept`：設定伺服器處理該欄位資料時，可接受的 MIME 型態，可指定複數種型態。
- `autocomplete`：設定是否自動完成表單內容。
- `list`：指定欄位的候選資料列表。
- `required`：設定該欄位是否不可為空。
- `pattern`：設定欄位正規表達式。
- `step`：可使用 `min` 與 `max` 屬性限制數字或日期時間的增量。
- `max`：最大值。
- `min`：最小值。
- `placeholder`：顯示於欄位中的提示用預設值。
- `form`：設定欄位屬於何個表單，引用值為表單的 `id`。
- `formaction`：替代表單的 `enctype` 屬性用。
- `formmethod`：替代表單的 `method` 屬性用。
- `formnovalidate`：替代表單的 `novalidate` 屬性用。
- `formtarget`：替代表單的 `target` 屬性用。
- `width`：設定 `image` 欄位的按鈕圖片寬度。

## 其它元素

```html
<section>
  <label for="email" class="top-label">E-mail</label>
  <input id="email type="email" autocomplete="off">
</section>
<section>
  <label class="top-label"> How do you know us? </label>

  <input id="how-friend" name="how" type="radio" />
  <label for="how-friend" class="side-label">From Friend</label>

  <input id="how-internet" name="how" type="radio" />
  <label for="how-internet" class="side-label">From Internet</label>

  <input id="how-other" name="how" type="radio" />
  <label for="how-other" class="side-label">Other</label>

  <div class="how-other-disclousure">
    <label for="how-other-explain" class="top-label"
      >Please describe the reason.</label
    >
    <textarea id="how-other-explain"></textarea>
  </div>
</section>
<section>
  <input id="permitted" type="checkbox" />
  <label for="permitted" class="side-label">Agree to send the form</label>
  <div class="blocked">Please check agree to send form</div>
  <button>Send</button>
</section>
```

- `<button>` 同於 `<input>` 元素，並可於內容裡放置圖片與文字。
- `<textarea>` 用來配置表單中多行文字輸入欄位，元素標籤內容的文字將成為多行輸入的預設資料。
- `<select>` 用來配置多重選項的選單物件，項目使用 `<option>`。
- `<option>` 用於定義在 `<select>`、 `<optgroup>` 或 `<datalist>`元素中包含的選單項目。
- `optgroup` 用來建立 `<option>` 的群組。
- `<label>` 可用於<br />
  ├ 1. 將文字敘述與表單輸入欄位一同包起來。<br />
  └ 2. 獨立於表單之外，使用 `for` 屬性設定代表何個表單的控制選項。
- `<fieldset>`：群組化表單欄位
- `<legend>`：表單欄位的標籤
- `<datalist>`：候選清單
- `<keygen>`：加密金鑰
- `<output>`：資料輸出
- `<progress>`：進度條
- `<meter>`：測量值

## SVG

- [SVG 完整教學 30+1 天](https://ithelp.ithome.com.tw/articles/10161004)
- [設計師對 SVG 應該有的觀念](https://intersection.tw/%E8%A8%AD%E8%A8%88%E5%B8%AB%E5%B0%8D-svg-%E6%87%89%E8%A9%B2%E6%9C%89%E7%9A%84%E8%A7%80%E5%BF%B5-38ba64b48b32)
- [SVG Path Builder](https://codepen.io/anthonydugois/pen/mewdyZ)
- [Get Waves - Create SVG waves for your next design](https://getwaves.io/)

### 1. 基本介紹

- SVG 向量圖形的特色使其能自由縮放，並能搭配 JS 做出互動效果
- 但由於運算效能的原因，不適合用於較為複雜的圖形
- 不受 CSS box model 管轄
- 會在 SVG Canvas 底下渲染
- SVG Canvas 需要對應有限尺寸的 viewport

### 2. 可用圖形

SVG 有提供幾種基本形狀供使用：

1. 矩形：`<rect id="A" x="33" y="34" fill="#FF6CC4" stroke="#C30D23" stroke-width="3" width="75" height="75"/>`<br />
   ├ `id`：該圖形的名稱<br />
   ├ `x`、`y`：圖形左上的錨點<br />
   ├ `fill`：圖形填充色<br />
   ├ `stroke`：框線顏色<br />
   ├ `stroke-width`：框線寬度<br />
   └ `width`、`height`：圖形寬高，單位為 px
2. 圓角矩形：`<rect x="60" y="10" rx="10" ry="10" width="75" height="75" stroke="#FF5500" stroke-width="5" fill="#FFB255"/>`<br />
   ├ 於原本的矩形裡再新增圓角半徑屬性 `rx`、`ry`<br />
   └ 使用 Illustrator 產出的 SVG 會轉換成 `path` 圖形
3. 圓形：`<circle fill="#FF4343" stroke="#890000" stroke-width="5" cx="80.141" cy="73.446" r="44"/>`<br />
   ├ `cx`、`cy`：圖形圓心<br />
   └ `r`：半徑
4. 橢圓：`<ellipse fill="#77DD47" stroke="#246614" stroke-width="5" cx="100" cy="75" rx="67" ry="44"/>`<br />
   └ 橢圓另外還有 x 方向的半徑 `rx` 與 y 方向的半徑 `ry`
5. 多邊形 `<polygon fill="#D271FF" points="100,56 62,107 37,49"/>`<br />
   ├ 使用 `points` 標記多邊形的每個點，即幾邊形就會有幾個點<br />
   └ 其餘的設定與矩形相同

### 3. Path

- Path 可說是組成 SVG 物件裡最強大的基本形狀
- `<path d="M0 0 L50 50 A50 50 0 0 0 100 0" stroke="#f00" fill="none"/>`
- Path 以屬性 `d` 開始定義，後續包含一系列的指令

各個指令所使用的參數：

| 指令 | 參數                                                | 指令說明                                                                                                                                                                                                                                               |
| ---- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| M    | x y                                                 | 起始點的 x , y 座標（move to）                                                                                                                                                                                                                         |
| H    | x                                                   | 從目前點的座標畫水平直線到指定的 x 軸座標（horizontal line to）                                                                                                                                                                                        |
| V    | y                                                   | 從目前點的座標畫垂直線到指定的 y 軸座標（vertical line to）                                                                                                                                                                                            |
| L    | x y                                                 | 從目前點的座標畫直線到指定點的 x , y 座標（line to）                                                                                                                                                                                                   |
| C    | x1 y1 x2 y2 x y                                     | 從目前點的座標畫條貝茲曲線到指定點的 x, y 座標：其中 x1, y1 及 x2, y2 為控制點（curve）                                                                                                                                                                |
| S    | x2 y2 x y                                           | 從目前點的座標畫條反射的貝茲曲線到指定點的 x, y 座標：其中 x2, y2 為反射的控制點（smooth curve）                                                                                                                                                       |
| Q    | x1 y1 x y                                           | 從目前點的座標畫條二次貝茲曲線到指定點的 x, y 座標：其中 x1, y1 為控制點（quadratic Bézier curve）                                                                                                                                                     |
| T    | x y                                                 | 從目前點的座標畫條鏡射二次貝茲曲線到指定點的 x, y 座標：以前一個座標為反射控制點( smooth quadratic Bézier curve）                                                                                                                                      |
| A    | rx ry x-axis-rotation large-arc-flag sweep-flag x y | 從目前點的座標畫個橢圓形到指定點的 x, y 座標：其中 rx, ry 為橢圓形的 x 軸及 y 軸的半徑，x-axis-rotation 是弧線與 x 軸的旋轉角度，large-arc-flag 則設定 1 最大角度的弧線或是 0 最小角度的弧線，sweep-flag 設定方向為 1 順時針方向或 0 逆時針方向（Arc） |
| Z    | 無參數                                              | 關閉路徑，將目前點的座標與第一個點的座標連接起來（closepath）                                                                                                                                                                                          |

### 4. Stroke

- `stroke`：邊框顏色
- `stroke-width`：邊框寬度
- `stroke-linecap`：邊框端點屬性（`butt`（預設）、`square`、`round`）
- `stroke-linejoin`：邊框兩端接合尖角屬性（`miter`（預設）、`round`、`bevel`）
- `stroke-dasharray`：邊框虛線化的長度與間隔，單數值代表實線的長度，雙數值代表虛線的長度，只有單數個參數時會預設複製一份參數
- `stroke-dashoffset`：邊框虛線化的線條相對起點的偏移量，正值向右負值向左

### 5. Viewport

- 可以透過 `svg` 標籤上的 `width` 和 `height` 屬性設定 viewport 的尺寸
- `<svg width="800" height="600"><!-- SVG內容 --></svg>`
- SVG 裡的值不一定會有單位，無單位的值會採用用戶座標系裡的用戶單位
- 預設為 `px`，其他也支援 `em`、`ex`、`px`、`pt`、`pc`、`cm`、`mm`、`in`、`百分比`。
- 初始化的 viewport 座標系以左上角為 (0,0) 開始計算，X 軸向右為正向，Y 軸向下為正向。
- `<svg viewBox="<min-x> <min-y> width height"></svg>`
- `preserveAspectRatio`

### 6. Fill

## Canvas

- [クリエイティブコーディングの教科書](https://zenn.dev/baroqueengine/books/a19140f2d9fc1a/viewer/d0f81a)
