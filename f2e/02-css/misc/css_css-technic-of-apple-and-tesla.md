- [【CSS】「これどうやる？」アップルやテスラのWebレイアウト再現テクニック集](https://photoshopvip.net/136000)

## Apple - 於捲動時固定部份區塊

- [Demo](https://jsfiddle.net/bsc2w8fo/)
- 加入一個 wrapper 元素，高度設為子元素的 2 倍（`200vh`）
- 子元素設為 `sticky`（`position: sticky` 及 `top: 0`）與 `height: 100vh`
- wrapper 的下方鄰接元素設為 `margin-top: -100vh`

## Tesla - 全頁式捲動

- [Demo](https://codepen.io/steve8708/pen/GRQGYwr)
- 容器設為 `scroll-snap-type: y mandatory;`
- 元素設為 `scroll-snap-align: start;` 與 `scroll-snap-stop: always;`

### Apple & Nike - 橫向式捲動

- [Demo](https://jsfiddle.net/L1cs6gt5/1/)
- 容器設為 `scroll-snap-type: x mandatory;`
- 元素設為 `scroll-snap-align: start;`

## Apple - 漢堡選單動畫

- [Demo](https://fiddle.jshell.net/ba6szc7d/3/)

## Airbnb - 上拉式延伸內容

- [Demo](https://jsfiddle.net/pj1vnsum/)

## Apple - 於捲動時縮放部份區域

- [Demo](https://jsfiddle.net/pz5av4fr/)

## Apple - 霧面玻璃效果

- `backdrop-filter: saturate(180%) blur(20px);`
