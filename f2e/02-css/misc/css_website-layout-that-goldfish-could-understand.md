# 金魚都能懂的網頁切版

## 影片清單

- [N01 圖文滿版區塊](https://youtu.be/rwTMBmnIHcY)
  - `.banner>.container>.banner-txt>(h1>small)+h2+p`
- [N02 互動圖文卡片](https://youtu.be/IocyLERRdko)
  - `.wrap>(.item>img[src="https://picsum.photos/500/400?random=10"]+.txt>h2{金魚都能懂的這個畫面怎麼切：互動圖文卡片}+p{護動圖文卡片是我們在網頁中經常見到的另一種稀飯版，不會切你就遜掉囉。})*4`
- [N03 人員介紹卡片](https://youtu.be/2Qs0EuqJIYA)
  - `.wrap>.item*3>img[src="https://picsum.photos/300/300?random=20"]+.txt>h2+p`
- [N04 交錯漂符版](https://youtu.be/aN7zFs_AT8s)
  - `.wrap>(.item>(.pic>img[src="https://picsum.photos/600/350?random=10"])+(.txt>h2+p))*4`
- [N05 超通用橫式版面](https://youtu.be/-mmzaE6eLzY)
  - `.wrap>.container>.item*3>(.pic>fak)+(.txt>h2+p)`
- [N06 網頁頁尾版塊](https://youtu.be/Y02yl_QQNv0)
  - `.main-footer>(.container>(.footer-item*3>h4+nav>a[href="#"]*4)+.footer-item>h4)+.copyright{Copyright $copy: 2019 金魚都能懂的這個網頁怎麼切}`
- [N07 導覽列](https://youtu.be/7BydlKueTgY)
  - `.main-header>.container>(a.logo[href="#"]>img[src="logo.png" alt="logo"])+(nav.main-nav>a*4[href="#"])+form.header-search>input[type="search" name="" id=""]+button`
- [N08 變化你的導覽列](https://youtu.be/9xT8kziyYko)
- [N09 網站麵包屑](https://youtu.be/n0yPFtpVRLU)
  - `.wrap>ol.breadcrumb>(li>a[href="#"]{Link})*5`
- [N10 方塊酥版面](https://youtu.be/Xhhzzc9YZW4)
  - `.wrap>.item*5>img[src="https://picsum.photos/500/500?random=$0"]+.txt>h3+p`
- [N11 破格式設計](https://youtu.be/l-sQNXNrw3s)
  - `.wrap>.item*3>.icon+.txt>h3+p`
- [N12 表格怎麼切](https://youtu.be/zRREfvlLFIU)
  - `.table>caption+table>(thead>tr>th[scope="col"]{敬請期待}*6)+(tbody>(tr>td{敬請期待}*6)*5)+(tfoot>tr>td+td[colspan="5"])`
- [N13 直式側邊選單](https://youtu.be/yB3_LtwBiaE)
  - `.sideMenu>(form>input+button>i.fas.fa-search)+(nav>a*4)`
- [N14 收合式側邊選單](https://youtu.be/-KPbFhZmBPE)
  - `input[type="checkbox" id="sideMenu-active"]+.sideMenu>(form>input+button>i.fas.fa-search)+(nav>a*4)+label[for="sideMenu-active"]>i.fas.fa-angle-right`
- [N15 多層次收合選單](https://youtu.be/_qmdKguG5IY)
  - `input[type="checkbox" id="sideMenu-active"]+.sideMenu>(form>input+button>i.fas.fa-search)+(ul.nav>(li>a+ul>(li>a)*3)*4)+label[for="sideMenu-active"]>i.fas.fa-angle-right`
- [N16 訂單進度條](https://youtu.be/AhHDJcys5tc)
  - `ul.list>(li>i.fa.fa-file-alt+{收到訂單})+(li>i.fa.fa-archive+{揀貨中})+(li>i.fa.fa-truck+{運送中})+(li>i.fa.fa-check-circle+{已送達})`
- [N17 登入表單](https://youtu.be/G5MA36MboNw)
  - `.login>form.form>h2{會員登入}+(.group>label[for="user_id"]{帳號}+input[type="text" name="" id="user_id"])+(.group>label[for="user_password"]{密碼}+input[type="password" name="" id="user_password"])+.btn-group>button.btn{登入}+button.btn{取消}`
- [N18 訊息對話紀錄](https://youtu.be/1tYhnmhdGNY)
  - `.dialogue>(.user.remote>(.avatar>.pic+.name)+txt)+(.user.local>(.avatar>.pic+.name)+.txt)`
- [N19 時間軸](https://youtu.be/AiR22hCQOGs)
  - `.wrap>h1+p+ul.timeline>(li>a[href="#"]>h2+p)*8`
- [N20 旋轉拼接方塊](https://youtu.be/QKGhYoRHJnI)
  - `ul>li.box${Text}*9`
- [N21 不規則邊緣](https://www.youtube.com/watch?v=7SFuF9XE24s)
  - `.banner+.section>.container>.item*2>h2+p*2`
- [N22 文字排版-上集](https://www.youtube.com/watch?v=-2sRROXi2pI)
  - `.wrap>.container>h1+.txt>p*2`
- [N23 文字排版-中集](https://www.youtube.com/watch?v=YYHqbVVXIGM)
  - `.wrap>.container>h1+.txt>p*4`
- [N24 文字排版-下集](https://www.youtube.com/watch?v=O6ags2wEGbc)
  - `.wrap>.container>h1+.txt>p*2`
- [N25 文字排版-完結](https://www.youtube.com/watch?v=VN-GcKUkdis)
- [標籤: CSS | TimCodingBlog](https://hsuchihting.github.io/tags/CSS/page/3/)

## 原理彙整

### [S01 N01-05 切版技巧原理彙整](https://youtu.be/R6q87Rfs0PM)

1. `display: flex;`
2. 對齊內容
   `justify-content`
   `center`
   `flex-end`
   `flex-start`
3. 控制主軸 main-axis
   `flex-direction`
   default: `row` 直向
   `column` 橫向
4. 換行
   `flex-wrap`
   default: `nowrap`
   `wrap`
5. 漸層色
   `background: #ccc;`
   `background-image: linear-gradient(角度, 起始色色標, 結束色色標);`
   0 度: 由下往上
   90 度: 由左往右
6. 三角形
   `width: 0;`
   `height: 0;`
   `border-top: 50px solid #f00;`
   `border-right: 50px solid #0f0;`
   `border-bottom: 50px solid #00f;`
   `border-left: 50px solid #aaa;`
7. `::before`／`::after` 產生於區塊內容裡的開頭／結尾
   `content: '';`
   `display: block;`
   `width: 20px;`
   `height: 20px;`
8. 定位

### [S02 N06-20 切版技巧原理彙整 2](https://youtu.be/cU43gPItOns)

1. `flex`
2. `margin: auto;`
3. `position: absolute;`, `position: relative;`, `position: fixed;`
4. `::before`
5. `float`
6. `transition`, `animation`
7. `box-shadow`
8. `colspan`
9. `cursor`
10. `backdrop-filter`
11. `order`
12. `display`

## 章節詳細

<details>

<summary>01. 圖文滿版</summary>

- CSS reset
- inline & block
- flex-direction
- linear-gradient
- 100vh
- `.banner>.container>.banner-txt>(h1>small)+h2+p`

#### CSS reset

```css
* {
  margin: 0;
  padding: 0;
  list-style: none;
}
```

#### container

```css
.container {
  width: 100%;
  max-width: 1280px;
  height: 100%;
  margin: 0 auto;
}
```

#### .bannerText 文字排版

```scss
.bannerText {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  h1 {
    font-size: 50px;
    border-bottom: 1px solid #000;
    small {
      display: block;
    }
  }
  h2 {
    font-size: 30px;
  }
  p {
    font-size: 20px;
  }
}
```

#### .banner 背景處理

```css
.banner {
  width: 100%;
  height: 100vh;
  background: linear-gradient(115deg, #f8d848 50%, transparent 50%) center center /
      100% 100%, url("https://images.unsplash.com/photo-1594046243098-0fceea9d451e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80")
      right center / auto 100%;
  .bannerText {
    /* ...; */
  }
}
```

</details>

<details>

<summary>02. 圖文互動</summary>

- `position: absolute;`, `position: relative;`
- `transition`
- `flex-direction`
- `.wrap>(.item>img[src="https://picsum.photos/500/400?random=10"]+.txt>h2{金魚都能懂的這個畫面怎麼切：互動圖文卡片}+p{護動圖文卡片是我們在網頁中經常見到的另一種稀飯版，不會切你就遜掉囉。})*4`

#### .wrap

```css
.wrap {
  width: 100vw;
  display: flex;
  margin: 0 auto;
}
```

#### .item

```scss
.item {
  width: 25%;
  position: relative;
  img {
    width: 100%;
    // 清除圖片多餘空間
    vertical-align: middle;
  }
  .content {
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    padding: 0 50px;
    background: rgba(#000, 0.6);
    // 垂直置中對齊
    display: flex;
    justify-content: center;
    flex-direction: column;
    // 透明漸變
    opacity: 0;
    transition: opacity 0.6s;
    cursor: pointer;
  }
  h2 {
    color: #00eaff;
    font-size: 32px;
  }
  p {
    color: #fff;
    padding: 5px 0;
    font-size: 10px;
  }
}
```

#### hover 效果

```scss
.item {
  width: 25%;
  position: relative;
  &:hover {
    .content {
      opacity: 1;
    }
  }
  // ...
}
```

#### ::after 偽元素

```scss
.item {
  width: 25%;
  position: relative;
  &:hover {
    .content {
      opacity: 1;
    }
    h2::after {
      width: 100%;
    }
  }
  // ...
  h2 {
    // ...
    &::after {
      content: "";
      display: block;
      width: 0;
      height: 2px;
      margin: 5px 0;
      background-color: #00eaff;
      transition: width 0.5s 0.3s;
    }
  }
}
```

</details>

<details>

<summary>03. 介紹卡片</summary>

- 製作三角形
- 計算區塊尺寸
- `position: absolute;`, `position: relative;`
- `transition`
- `flex-direction`
- `.wrap>.item*3>img[src="https://picsum.photos/300/300?random=20"]+.txt>h2+p`

#### 排版雛型

```scss
body {
  display: flex
  align-items: center;
  background-color: #000033;
}

.wrap {
  width: 960px;
  display: flex;
  margin: 0 auto;
}

.card {
  width: 300px;
  margin-right: 10px;
  margin-left: 10px;
  background-color: #fff;
  border: 1px solid #fff;
  transform: translateY(0px);
  transition: all 0.5s;
  cursor: pointer;
  img {
    width: 100%;
    vertical-align: middle;
  }
}

.content {
  padding: 20px;
  position: relative;
  text-align: center;
  h2 {
    font-size: 24px;
    font-weight: bold;
    border-bottom: 1px solid #333;
    padding-bottom: 10px;
    margin-bottom: 10px;
    text-align: center;
  }
  p {
    line-height: 1.5;
    text-align: left;
  }
  h2,
  p {
    color: #444;
  }
}
```

#### 三角形

```scss
.content {
  // ...
  &::before {
    content: "";
    position: absolute;
    width: 0;
    height: 0;
    top: 0;
    left: 0;
    border-top: 50px solid transparent;
    border-left: 149px solid #fff;
    border-right: 149px solid #fff;
    transform: translateY(-100%);
  }
}
```

#### hover 效果

```scss
.card {
  // ...
  &:hover {
    transform: translateY(-30px);
    .content {
      background-image: linear-gradient(0deg, #d0ff34, #fcff35);
    }
  }
  .content {
    // ...
    &:hover {
      &::before {
        content: "";
        border-left: 149px solid #fcff35;
        border-right: 149px solid #fcff35;
      }
    }
    // ...
  }
}
```

</details>

<details>

<summary>04. 交錯飄浮</summary>

- 計算區塊尺寸
- `box-sizing`
- `position: relative;`
- 色彩原理
- `flex-direction`
- `:nth-child()`
- `.wrap > (.item>(.pic>img[src="https://picsum.photos/600/350?random=10"])+(.txt>h2+p)) + (.item>(.txt>h2+p)+(.pic>img[src="https://picsum.photos/600/350?random=10"]))`

#### .item

```scss
.item {
  display: flex;
  align-items: center;
  margin-bottom: 70px;
  .pic,
  .text {
    flex-shrink: 0;
    width: 55%;
  }
  img {
    width: 100%;
    vertical-align: middle;
  }
}
```

#### 子代選取器

- `>:first-child`：選中的元素底下一層的第一個子元素
- `&:first-child`：選中的元素的第一個

```scss
.item {
  // ...
  > :first-child {
    margin-right: -50px;
  }
  &:nth-child(1) .text {
    background-color: rgba($color: #e0e0e0, $alpha: 0.8);
  }
  &:nth-child(2) .text {
    background-color: rgba($color: #e0e0e0, $alpha: 0.8);
  }
  &:nth-child(3) .text {
    background-color: rgba($color: #e0e0e0, $alpha: 0.8);
  }
  &:nth-child(4) .text {
    background-color: rgba($color: #e0e0e0, $alpha: 0.8);
  }
}
```

</details>

<details>

<summary>05. 通用橫板</summary>

- 計算區塊尺寸
- `box-sizing`
- 色彩原理
- `flex`
- `flex-direction`
- `object-fit`
- `flex-wrap`
- `.wrap>.container>.item*3>(.pic>fak)+(.txt>h2+p)`

#### 垂直置中

```css
.wrap {
  height: 100vh;
  display: flex;
  align-items: center;
}
```

#### 容器斷行置中

```css
.container {
  width: 1200px;
  display: flex;
  flex-wrap: wrap;
  margin: 0 auto;
}
```

#### 計算內容尺寸

- 內容 `50%` 減去左右間隔 `1%` 和邊框線 `1px` = `47%`
- 圖文比例 `6:4`
- 圖片保持原比例填滿容器：`object-fit: cover;`

```scss
.item {
  width: 47%;
  margin: 1%;
  display: flex;
  border: 1px solid #0a232b;
  box-shadow: 0 0 5px 2px rgba($color: #061a20, $alpha: 0.6);
  .pic {
    width: 60%;
    img {
      vertical-align: middle;
      object-fit: cover;
    }
  }
  .text {
    width: 40%;
    padding: 20px;
    background-color: #fff;
    display: flex;
    flex-direction: column;
    h2 {
      font-size: 28px;
      margin-bottom: 20px;
      color: #0987ad;
    }
    p {
      color: #444;
      font-size: 14px;
      line-height: 1.5;
    }
    .btn {
      line-height: 1.5em;
      border: 1px solid #0987ad;
      padding: 0 10px;
      align-self: flex-end;
      text-decoration: none;
      border-radius: 100px;
      color: #0987ad;
      margin-top: auto;
      &:hover {
        background-color: #0987ad;
        color: #fff;
        transition: all 0.3s;
      }
    }
  }
}
```

</details>

<details>

<summary>06. 頁尾資訊</summary>

- Google font -`flex-grow`
- `.main-footer>(.container>(.footer-item*3>h4+nav>a[href="#"]*4)+.footer-item>h4)+.copyright{Copyright $copy: 2019 金魚都能懂的這個網頁怎麼切}`

#### 基礎排板

```css
.main_footer {
  background: linear-gradient(-270deg, #0d47a1, #03a9f4);
  padding: 100px 0 0 0;
  position: fixed;
  bottom: 0;
  right: 0;
  left: 0;
}

.wrap {
  width: 1200px;
  margin: 0 auto;
  display: flex;
}
```

#### flex-grow

```css
.item {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  color: #fff;
  margin-right: 1%;
  margin-left: 1%;
}
```

#### 設定字體

```scss
.item {
  // ...
  h4 {
    font-size: 24px;
    border-bottom: 1px dotted #fff;
    font-weight: 700;
    padding-bottom: 10px;
  }
  li {
    font-size: 16px;
    font-weight: 300;
    padding-top: 10px;
    line-height: 1.5;
  }
  // ...
}
```

#### 置中訂閱電子報

```css
form {
  display: flex;
  margin: auto 0;
}
```

</details>

<details>

<summary>07. 導覽列</summary>

- `.main-header>.container>(a.logo[href="#"]>img[src="logo.png" alt="logo"])+(nav.main-nav>a*4[href="#"])+form.header-search>input[type="search" name="" id=""]+button`

#### 基礎排板

```css
a {
  text-decoration: none;
  color: #26ff93;
  font-weight: 300;
}
```

#### Logo 橫向對齊

```scss
.logo {
  margin-left: 1em;
  display: flex;
  align-items: center;
  .fa-spotify {
    padding-right: 0.5em;
    color: #26ff93;
  }
  span {
    font-size: 26px;
    font-weight: 500;
  }
}
```

#### 導覽列

```scss
.navbar {
  display: flex;
  align-items: center;
  margin: auto;
  .item {
    flex-grow: 1;
    padding: 20px;
    // 為了 hover 效果預留空間
    border-bottom: 5px solid transparent;
    transition: 0.3s
    &:hover {
      border-bottom: 5px solid #26ff93;
    }
  }
}
```

#### 搜尋列

```scss
.navSearch {
  display: flex;
  align-items: center;
  margin-left: auto;
  input,
  button {
    border: none;
    outline: none;
    height: 30px;
    background-color: #fff;
  }
  input {
    padding-left: 12px;
    width: 80%;
    border-radius: 100px 0 0 100px;
  }
  button {
    width: 20%;
    border-radius: 0 100px 100px 0;
    cursor: pointer;
  }
  .fa-search {
    color: #555;
    &:hover {
      color: #26ff93;
      transition: all 0.3s;
    }
  }
}
```

</details>

<details>

<summary>08. 麵包屑</summary>

- `+` 選取器
- hsl 色彩
- `::before`
- `.wrap>ol.breadcrumb>(li>a[href="#"]{Link})*5`

####　`+` 選取器

```scss
.breadcrumbList {
  border-bottom: 3px solid #26ff93;
  box-shadow: inset 0 0 11px 3px rgba(#000, 0.6);
  .breadcrumb {
    display: flex;
    li {
      padding: 20px 20px 20px 0px;
      & + li {
        padding-left: 0;
      }
      & + li::before {
        content: "/";
        color: #fff;
        padding-right: 20px;
      }
      &:last-child a {
        color: #26ff93;
      }
      a {
        color: #fff;
        font-weight: 100;
        font-size: 16px;
        cursor: pointer;
        &:hover {
          color: #26ff93;
        }
      }
    }
  }
}
```

</details>

<details>

<summary>09. 方塊酥圖片</summary>

- `float`
- `~` 選取器
- RGB 色彩
- `position: relative;`
- `position: absolute;`
- `.wrap>.item*5>img[src="https://picsum.photos/500/500?random=$0"]+.txt>h3+p`

#### box-sizing

```css
body {
  box-sizing: border-box;
  font-family: "Noto Sans TC", sans-serif;
  background-color: #271919;
}

.wrap {
  width: 1200px;
  margin: 5% auto;
  /* overflow: hidden 可讓父層自動抓到所有子層高度 */
  overflow: hidden;
}
```

#### 雙向排板

```scss
.item {
  // float 將元素轉為橫向排列後會斷行, flex 則否
  float: left;
  img {
    width: 100%;
    vertical-align: middle;
  }
  &:first-child {
    width: 50%;
  }
  &:first-child ~ .item {
    width: 25%;
  }
}
```

#### 文字效果

```scss
.text {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  text-align: center;
  color: #fff;
  background-color: rgba($color: #000, $alpha: 0.6);
  display: flex;
  flex-direction: column;
  justify-content: center;
  opacity: 0;
  transition: all 0.3s;
  &:hover {
    opacity: 1;
  }
}
```

</details>

<details>

<summary>10. 表格</summary>

- `flex`
- `first-child`
- `last-child`
- `nth-child`
- `caption` 表格標題
- `scope="col"`
- `colspan="#"` 合併表格
- `.table>caption+table>(thead>tr>th[scope="col"]{敬請期待}*6)+(tbody>(tr>td{敬請期待}*6)*5)+(tfoot>tr>td+td[colspan="5"])`

#### table 基礎

```scss
.table {
  width: 800px;
  margin: 0 auto;

  table {
    border: 3px double #333;
    width: 100%;
  }
  th,
  td {
    border: 1px solid #666;
    padding: 6px 10px;
  }
}
```

#### table 精修

```scss
.table {
  // ...
  caption {
    caption-side: bottom;
    text-align: right;
    font-weight: 300;
  }
  table {
    // ...
    background-color: #fff;
    border-radius: 10px;
    thead {
      th:first-child {
        border-radius: 10px 0 0 0;
      }
      th:last-child {
        border-radius: 0 10px 0 0;
      }
    }
    tfoot {
      td:first-child {
        border-radius: 0 0 0 10px;
      }
      td:last-child {
        border-radius: 0 0 10px 0;
      }
    }
  }
  // ...
}
```

#### 色彩效果

```scss
.table {
  // ...
  table {
    // ...
    thead {
      border-color: #333;
      color: #fff;
      // ...
    }
    tbody {
      tr:nth-child(even) {
        background-color: #ddd;
      }
      tr:hover {
        background-color: #ffc4c4;
        transition: all 0.5s;
        cursor: pointer;
      }
    }
    // ...
  }
}
```

</details>

<details>

<summary>11. 破格式</summary>

- `position: relative;`
- `position: absolute;`
- `animation`
- `flex`
- `background-image`
- `::before`
- `.wrap>.item*3>.icon+.txt>h3+p`

#### body

```css
body {
  display: flex;
  align-items: center;
}
```

#### .wrap

```css
.wrap {
  width: 1200px;
  margin: 0 auto;
  display: flex;
  padding-top: 50px;
}
```

#### .item

```css
.item {
  width: 29.3333%;
  height: 269px;
  text-align: center;
  margin: 0 3%;
  background-color: #131261;
  border: 5px solid #ffd665;
  border-radius: 20px;
  cursor: pointer;
}
```

#### icon

```scss
.icon {
  width: 150px;
  height: 150px;
  margin: -75px auto 0;
  background-color: #131261;
  border-radius: 100%;
  position: relative;
  &::before {
    content: "";
    position: absolute;
    width: 100%;
    height: 100%;
    border: 5px solid #ffd665;
    top: -5px;
    left: -5px;
    border-radius: 100%;
    border-left: 5px solid transparent;
    border-bottom: 5px solid transparent;
    transform: rotate(-45deg);
  }
  .fas {
    line-height: 150px;
    color: #ffd665;
  }
}
```

#### .text

```scss
.text {
  padding: 20px;
  position: absolute;
  top: 30px;
  h3 {
    color: #ffd665;
    font-size: 32px;
    font-weight: 500;
    padding-bottom: 1%;
  }
  p {
    color: #fff;
    font-weight: 100;
    line-height: 1.5;
    padding-bottom: 5%;
  }
}
```

#### 動畫效果

```scss
.item {
  width: 29.3333%;
  height: 269px;
  text-align: center;
  margin: 0 3%;
  background-color: #131261;
  border: 5px solid #ffd665;
  border-radius: 20px;
  box-shadow: 0px 0px 5px #000;
  position: relative;
  cursor: pointer;
  &:hover {
    .fas {
      animation: shake 0.2s linear infinite alternate;
      transition: all 0.5s;
      color: #ffebb4;
      filter: drop-shadow(0 0 10px #ffebb4);
    }
  }
}
@keyframes shake {
  0% {
    transform: rotate(-10deg);
  }
  100% {
    transform: rotate(10deg);
  }
}
```

</details>

<details>

<summary>12. 側邊選單</summary>

- `flex`
- `::before`、`::after`
- 選取器
- `box-sizing`
- `position: relative;`
- `position: absolute;`
- `.sideMenu>(form>input+button>i.fas.fa-search)+(nav>a*4)`

#### .sideMenu

```css
.sideMenu {
  width: 300px;
  height: 100%;
  background-color: #ff7575;
  border-right: 3px solid #d1d1d1;
  display: flex;
  flex-direction: column;
  padding: 50px 0;
  box-shadow: 5px 0 5px rgba(#303c4d, 0.6);
}
```

#### 搜尋列

```scss
form {
  display: flex;
  margin: 0 10px 50px;
  border-radius: 100px;
  border: 1px solid #fff;

  input {
    width: 85%;
  }

  button {
    width: 15%;
  }

  input,
  button {
    border: none;
    padding: 5px 10px;
    background-color: transparent;
    color: #fff;
  }
  input:focus,
  button:focus {
    outline: none;
  }
}
```

#### icon 位移

```scss
nav {
  a {
    display: block;
    color: #fff;
    padding: 20px 10px;
    position: relative;
    font-weight: 300;

    .fas {
      margin-right: -1.1em;
      transform: scale(0);
      transition: 0.3s;
    }

    &:hover .fas {
      margin-right: 0em;
      transform: scale(1);
    }

    & + a::before {
      content: "";
      position: absolute;
      border-top: 1px solid #fff;
      left: 10px;
      right: 10px;
      top: 0px;
    }
  }
}
```

</details>

<details>

<summary>13. 動態側邊選單</summary>

- `flex`
- `:checked`
- `position: absolute;` + `margin: auto;`
- RWD
- `input[type="checkbox" id="sideMenu-active"]+.sideMenu>(form>input+button>i.fas.fa-search)+(nav>a*4)+label[for="sideMenu-active"]>i.fas.fa-angle-right`

#### label

```css
label {
  width: 20px;
  height: 80px;
  background-color: #d1d1d1;
  color: #686666;
  position: absolute;
  right: -20px;
  top: 0;
  bottom: 0;
  margin: auto;
  line-height: 80px;
  text-align: center;
  border-radius: 0 5px 5px 0;
  box-shadow: 5px 0 5px rgba(23, 23, 54, 0.6);
}
```

#### checkbox

```scss
#sideMenu-active:checked + .sideMenu {
  transform: translateX(0);
  label .fas {
    transform: scaleX(-1);
  }
}

#sideMenu-active {
  position: absolute;
  opacity: 0;
  z-index: -1;
}

.sideMenu {
  // ...
  position: relative;
  transform: translateX(-100%);
  transition: 0.5s;
}
```

</details>

<details>

<summary>14. 多層收合選單</summary>

- 子代選擇器
- `:checked`
- `position: absolute;` + `margin: auto;`
- `input[type="checkbox" id="sideMenu-active"]+.sideMenu>(form>input+button>i.fas.fa-search)+(ul.nav>(li>a+ul>(li>a)*3)*4)+label[for="sideMenu-active"]>i.fas.fa-angle-right`

```html
<input type="checkbox" id="sideMenu-active" />
<div class="sideMenu">
  <form action="">
    <input type="text" /><button><i class="fas fa-search"></i></button>
  </form>
  <ul class="nav">
    <li>
      <a href=""></a>
      <ul>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
      </ul>
    </li>
    <li>
      <a href=""></a>
      <ul>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
      </ul>
    </li>
    <li>
      <a href=""></a>
      <ul>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
      </ul>
    </li>
    <li>
      <a href=""></a>
      <ul>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
      </ul>
    </li>
  </ul>
  <label for="sideMenu-active"><i class="fas fa-angle-right"></i></label>
</div>
```

## nav 微調

```scss
.nav {
  li {
    display: block;
    color: #fff;
    padding: 20px 10px;
    position: relative;

    a {
      color: #fff;
    }

    .fas {
      margin-right: -1.1em;
      transform: scale(0);
      transition: 0.3s;
    }

    &:hover .fas {
      margin-right: 0em;
      transform: scale(1);
    }

    & + a::before {
      content: "";
      position: absolute;
      border-top: 1px solid #fff;
      left: 10px;
      right: 10px;
      top: 0px;
    }
  }
}
```

## 子層選單

```scss
.nav {
  li {
    display: block;
    color: #fff;
    padding: 20px 10px;
    position: relative;
  }
  ul {
    position: absolute;
    left: 100%;
    width: 300px;
    background-color: rgba(#d1d1d1, 0.7);
    top: 15px;
    box-shadow: 5px 5px 10px rgba(#171736, 0.6);
  }
}
```

## 子層選單互動效果

```scss
.nav {
  li {
    display: block;
    color: #fff;
    padding: 20px 10px;
    position: relative;
    cursor: pointer;
    &:hover,
    > li {
      background-color: #a32c2c;
      transition: all 0.6s;
    }
    &:hover > ul {
      display: block;
    }
    ul {
      display: none;
      position: absolute;
      left: 100%;
      width: 300px;
      background-color: rgba(#d1d1d1, 0.7);
      top: 15px;
      box-shadow: 5px 5px 1px rgba(#171736, 0.6);
    }
  }
}
```

</details>

<details>

<summary>15. 對話紀錄</summary>

- `+` 選取器
- 計算區塊尺寸
- `position: absolute;`
- `position: relative;`
- `.dialogue>(.user.remote>(.avatar>.pic+.name)+txt)+(.user.local>(.avatar>.pic+.name)+.txt)`

#### .dialogue

```css
.dialogue {
  width: 500px;
  padding: 20px;
  box-shadow: 0 0 10px #000;
  background-color: #f4f5f7;
  border-radius: 20px;
}
```

#### .user

```scss
.user {
  display: flex;
  align-items: flex-start;
  margin-bottom: 20px;
  .avatar {
    width: 60px;
    text-align: center;
    flex-shrink: 0;
  }
  .pic {
    border-radius: 50%;
    overflow: hidden;
    img {
      width: 100%;
      vertical-align: middle;
    }
  }
  .name {
    color: #333;
  }
  .text {
    background-color: #aaa;
    padding: 16px;
    border-radius: 10px;
    position: relative;
  }
}
```

#### .remote & .local

```scss
.remote {
  .text {
    margin-left: 20px;
    margin-right: 80px;
    color: #eee;
    background-color: #4179f1;
    &::before {
      border-right: 10px solid #4179f1;
      left: -10px;
    }
  }
}

.local {
  justify-content: flex-end;
  .text {
    margin-right: 20px;
    margin-left: 80px;
    order: -1;
    background-color: #fff;
    color: #333;
    &::before {
      border-left: 10px solid #fff;
      right: -10px;
    }
  }
}
```

#### 對話三角框

```scss
.remote,
.local {
  & .text::before {
    content: "";
    position: absolute;
    top: 20px;
    border-top: 10px solid transparent;
    border-bottom: 10px solid transparent;
  }
  .text {
    font-weight: 300;
    box-shadow: 0 0 10px #888;
  }
}
```

</details>

<details>

<summary>16. 訂單進度條</summary>

- `flex-direction`
- `position: absolute;` + `margin: auto;`
- `.wrap>h1+p+ul.timeline>(li>a[href="#"]>h2+p)*8`

#### body

```css
body {
  box-sizing: border-box;
  font-family: "Noto Sans TC", sans-serif;
  display: flex;
  align-items: center;
}
```

#### li

```scss
li {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  width: 150px;
  height: 150px;
  border-radius: 100px;
  position: relative;
  background-image: linear-gradient(45deg, #1e681e, #69e742, #eef85a);
  box-shadow: 0 0 0 5px #fff;
  & + li {
    margin-left: 100px;
    &::before {
      content: "";
      position: absolute;
      width: 100px;
      height: 5px;
      background-color: #fff;
      top: 0;
      bottom: 0;
      left: -100px;
      margin: auto;
      z-index: -1;
    }
  }
  &.active ~ li {
    background-image: linear-grident(45deg, #999, #ccc, #eee);
  }
  .fas,
  p {
    color: #194588;
  }
}
```

</details>

<details>

<summary>17. 登入表單</summary>

- `flex`
- `backdrop-filter: blur;`
- `.login>form.form>h2{會員登入}+(.group>label[for="user_id"]{帳號}+input[type="text" name="" id="user_id"])+(.group>label[for="user_password"]{密碼}+input[type="password" name="" id="user_password"])+.btn-group>button.btn{登入}+button.btn{取消}`

#### body

```css
body {
  box-sizing: border-box;
  font-family: "Noto Sans TC", sans-serif;
  background: url("https://images.unsplash.com/photo-1578683010236-d716f9a3f461?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80")
    no-repeat center center / cover;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

#### login 區塊

```css
.login {
  width: 300px;
  height: 300px;
  padding: 20px;
  background-color: rgba(#000, 0.6);
  border-radius: 20px;
  border: 5px solid #fff;
  box-shadow: 0 0 30px #000;
  backdrop-filter: blur(5px);
  display: flex;
  justify-content: center;
  align-items: center;
}
```

#### 欄位與按鈕

```scss
.form {
  width: 100%;
  .loginGroup {
    margin-bottom: 10px;
  }
  label {
    color: #fff;
    line-height: 2.5;
    font-weight: 300;
    input {
      outline: none;
      padding: 10px 0;
      padding-left: 12px;
      width: 95%;
      border: 2px solid #aaa;
      border-radius: 6px;
      &:focus {
        border: 2px solid #72a8f0;
      }
    }
  }
  .btnGroup {
    display: flex;
    justify-content: space-between;
    margin-top: 20px;
    .btn {
      padding: 10px 50px;
      border-radius: 6px;
      outline: none;
      border: none;
      font-weight: 300;
      font-size: 16px;
      color: #fff;
      cursor: pointer;
    }
    .btnAccess {
      background-color: #2bc42b;
      &:hover {
        background-color: darken(#2bc42b, 10%);
      }
    }
    .btnCancel {
      background-color: #f08282;
      &:hover {
        background-color: darken(#f08282, 10%);
      }
    }
  }
}
```

</details>

<details>

<summary>18. 旋轉方塊</summary>

- class 選取器
- `::before`
- `:nth-child()`
- `ul>li.box${Text}*9`

#### .cube

```scss
.cube {
  display: flex;
  flex-wrap: wrap;
  padding: 100px 0;

  li {
    width: 200px;
    height: 200px;
    text-align: center;
    line-height: 200px;
    outline: 1px solid #f00;
    margin: 0 2% 4% 2%;
  }
}
```

#### li::before

```scss
.cube {
  // ...
  li {
    // ...
    position: relative;
    &::before {
      content: "";
      width: 100%;
      height: 100%;
      // 確認位置用外框線
      outline: 1px solid blue;
      position: absolute;
      top: 0;
      left: 0;
      transform: rotate(45deg);
    }
  }
}
```

#### :nth-child()

```css
li:nth-child(n + 4) {
  left: 153px;
}
li:nth-child(n + 7) {
  left: 0;
}
```

#### 偽元素背景顏色

```css
.box1::before {
  background-color: #4dd0e1;
}
.box2::before {
  background-color: #fff176;
}
.box3::before {
  background-color: #ff8e6c;
}
.box4::before {
  background-color: #c3a6f5;
}
.box5::before {
  background-color: #9ccc65;
}
.box6::before {
  background-color: #4dd0e1;
}
.box7::before {
  background-color: #ffe817;
}
.box8::before {
  background-color: #f48fb1;
}
.box9::before {
  background-color: #ebffd5;
}
```

#### 最後裝飾

```scss
.cube {
  // ...
  li {
    // ...
    &::before {
      // 刪除外框線
      // outline: 1px solid blue;
      // ...
      box-shadow: 0 0 5px #666;
      z-index: -1;
    }
  }
}
```

</details>

<details>

<summary>19. 時間軸</summary>

- `flex`
- `position: absolute;` + `margin: auto;`
- `float`
- `position: absolute;`
- `position: relative;`
- `::before`、`::after`
- `:last-child()`、`:nth-child()`
- `.wrap>h1+p+ul.timeline>(li>a[href="#"]>h2+p)*8`

#### .timeline

```scss
.timeline {
  padding-top: 5%;
  li {
    padding-top: 25px;
    padding-bottom: 25px;
    border-radius: 10px;
    width: 50%;
  }
}
```

#### li:nth-child()

```scss
.timeline {
  // ...
  a {
    display: block;
    background-color: #ffe033;
    border: 2px solid #fff;
    padding: 20px;
    box-shadow: 0 0 5px #666;
    border-radius: 10px;
    transition: all 0.5s;
    &:hover {
      background-color: #fcea86;
    }
  }
  li {
    // ...
    &:nth-child(odd) {
      float: left;
      padding-right: 100px;
    }
    &:nth-child(even) {
      float: right;
      padding-left: 100px;
      transform: translateY(50%);
    }
  }
}
```

#### 時間軸線條

```scss
.timeline {
  // ...
  li {
    // ...
    &:nth-child(odd) {
      // ...
      &::after {
        content: "";
        position: absolute;
        top: 0;
        right: 0;
        width: 1px;
        height: 100%;
        background-color: #fff;
      }
    }
    // ...
  }
}
```

#### 時間軸線條裝飾

```scss
.timeline {
  // ...
  li {
    // ...
    position: relative;

    &::before {
      content: "";
      position: absolute;
      top: 0;
      bottom: 0;
      margin: auto;
      width: 20px;
      height: 20px;
      border-radius: 50%;
      background-color: #fff;
    }

    &:nth-child(odd) {
      // ...
      & h2::after {
        right: 0;
      }
      &::after {
        // ...
      }
      &::before {
        right: -10px;
      }
    }

    &:nth-child(even) {
      // ...
      & h2::after {
        left: 0;
      }
      &:last-child {
        height: 50%;
      }
      &::before {
        left: -10px;
      }
    }
  }
}
```

</details>

<details>

<summary>20. 不規則邊緣</summary>

- `position: absolute;`
- `position: relative;`
- `flex`
- 偽元素
- `transform: translate()`
- `box-shadow`
- `.banner+.section>.container>.item*2>h2+p*2`

</details>

<details>

<summary>21. 九種文字排板</summary>

- `box-sizing: border-box;`
- `position: absolute;`
- `position: relative;`
- `flex-direction`
- `column-count`
- `column-gap`
- 偽元素
- `:first-letter`
- `.wrap>.container>h1+.txt>p*2`

#### 樣式一

```css
.content {
  width: 66.6666%;
  column-count: 2;
  column-gap: 5%;
}
```

</details>
