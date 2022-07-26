- [いざという時に使える13のHTML&CSS Tips集](https://pulpxstyle.com/html-css-tips01/)

## 文字貼合圓形圖片

- 於圖片容器加上 `shape-outside: circle(50%);`
- 此屬性必須搭配 `float`

## 新的 float 解除法

- 於 `float` 的父元素加上 `display: flow-root;`

## 響應顯示不同圖片

```html
<picture>
  <source srcset="image-large.jpg" media="(min-width: 768px)">
  <source srcset="image-medium.jpg" media="(min-width: 576px)">
  <img src="image-small.jpg" alt="">
</picture>
```

## 指定空元素內容

```css
dd:empty::before {
  contetn: '-';
}
```

## 自動播放影片

<video src="movie.mp4" loop autoplay muted playsinline></video>