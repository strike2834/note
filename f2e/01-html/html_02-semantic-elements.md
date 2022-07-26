# 語意化撰寫

- [我不知道的 HTML Semantic](https://w3c.hexschool.com/blog/989672eb)
- [なんとなくで書かないで！HTML5 を書く時に気にしてみたいタグごとのお約束](https://qiita.com/mikimhk/items/05b303d932093eb4c0d1)
- [SEO 対策として最低限押さえておきたい HTML/HTML5 マークアップの大事な 6 つのポイント](https://creive.me/archives/8814)
- 便於機械閱讀，能夠取得更好的 SEO 效果，並能讓螢幕閱讀器正確讀取
- 也便於人類閱讀，提升網頁的維護性

## 標籤

- 標籤內容的種類
- 可輸入標籤中的內容
- 可否省略標籤
- 可位於其之上的母元素
- 可使用的 Aria role
- DOM 介面

## 應該避開的寫法

```html
<!-- Bad Example -->
<!-- 直接在 a 標籤上加上 onclick -->
<a href="#" onclick="alert('alert!')">button</a>

<!-- 在 a 標籤裡再加入 a 標籤 -->
<a>
  <div>Title</div>
  <a href="#">Link</a>
</a>
```

1. 使用點擊觸動 js 時應該使用 `<button>`，因為無法預期執行的行為為何
2. `<a>` 標籤不允許擁有 `<a>` 標籤的母元素

```html
<!-- Bad Example -->
<!-- 沒有加入 alt 元素，試圖直接以 title 取代 -->
<img src="https://example.com/img/example.png" title="Title" />
```

## Aria 標籤

- [前端的基礎修養：aria-label - Just lepture](https://lepture.com/zh/2015/fe-aria-label)
- [ARIA 標籤和關係](https://developers.google.com/web/fundamentals/accessibility/semantics-aria/aria-labels-and-relationships?hl=zh-tw)
