# AJAX

- 在講到非同步處理時，會有兩個經常出現的相關詞彙――「REST」和「AJAX」
  - 這兩個名詞其實都是技術概念的總稱
- 「REST（Representational State Transfer）」是一種網路架構的設計概念
  - 定義交換資訊時需要的具體狀態
  - 例如：
    - 統一介面
    - 所有資源都具有唯一的 URI
    - 可以透過超連結彼此連接
    - 不具有狀態
    - 每次的互動都在一次裡完結
  - RESTful API 就是符合這種設計思想的 API
- 「AJAX（Asynchronous JavaScript and XML）」則是泛指
  - 如何透過 JS 取得或傳遞延伸的資料（即 XML，Extensible Mark Language）
  - 並反應到網頁上的技術概念
  - 後續提及的 `XMLHttpRequest` 物件、jQuery 裡的 `.ajax` function、`Fetch` 和 axios 都是種 AJAX 技術
- [Native な JavaScript で Fetch API を利用し Ajax を行う](https://qiita.com/doriven/items/503fdc6de9bc0e725334)
- [Javascript の Ajax についての基本まとめ - Qiita](https://qiita.com/katsunory/items/9bf9ee49ee5c08bf2b3d)
- [透過 curl、Python、Postman 來 Request API \- 🐴 的學習筆記](https://jzchangmark.wordpress.com/2016/06/12/%E9%80%8F%E9%81%8E-curl%E3%80%81python%E3%80%81postman-%E4%BE%86-request-api/)
- [一起來把煩人 XMLHttpRequest 變成 Fetch 怎麼樣？](https://realdennis.medium.com/%E4%B8%80%E8%B5%B7%E4%BE%86%E6%8A%8A%E7%85%A9%E4%BA%BA-xmlhttprequest-%E8%AE%8A%E6%88%90-fetch-%E6%80%8E%E9%BA%BC%E6%A8%A3-8657f2854894)
- [AJAX 與 Fetch API · 從 ES6 開始的 JavaScript 學習生活](https://eyesofkids.gitbooks.io/javascript-start-from-es6/content/part4/ajax_fetch.html)

## 1. XMLHttpRequest

- 於 2006 年正式列入 W3C 標準中
- 難以閱讀與撰寫

```javascript
const result = document.querySelector(".result");
function reqOnload() {
  const data = JSON.parse(this.responseText);
  var email = data.results[0].email;
  result.textContent = email;
}
function reqError(err) {
  console.log(err);
}
var request = new XMLHttpRequest();
request.open("get", "https://randomuser.me/api/", true);
request.send();
request.onload = reqOnload;
request.onerror = reqError;
```

## 2. jQuery.ajax()

- 基於 XHR 開發，然而 XHR 架構不清晰，並已有替代方案
- jQuery 整體項目太大，效益低落

```javascript
var result = $(".result");

$.ajax({
  url: "https://randomuser.me/api/",
  dataType: "json",
  success: function (data) {
    result.html(data.results[0].email);
  },
});
```

## 3. Fetch

- 自 ES6 起提供的方式
- 概念相近 jQuery 的 `$.ajax`
- 使用 ES6 的 Promise 進行回傳，回傳 `ReadableStream` 物件
- 需搭配 then 與 catch 進行處理
- 會將 400，500 都當做請求成功，需要另外做處理
- 預設不帶 cookie
- 不支援 timeout handle
- 不支援監測請求的進度
- 較早的瀏覽器並不支援（IE11 以下不支援）

```javascript
const result = document.querySelector(".result");

fetch("https://randomuser.me/api/", {})
  .then((response) => {
    console.log(response);

    return response.json();
  })
  .then((data) => {
    var email = data.results[0].email;
    result.textContent = email;
  })
  .catch((err) => {
    console.log(err);
  });
```

## 4. Axios

- [Vue 套件介紹：axios - Eugene Su](https://eugenesu0515.github.io/Blog/2018/06/25/Vue%E5%A5%97%E4%BB%B6%E4%BB%8B%E7%B4%B9%EF%BC%9Aaxios/)
- Vue.js 作者推薦使用
- 使用需引入 [axios](https://github.com/axios/axios)
- 概念相近 jQuery 的 `$.ajax`
- 可以在 node.js 中使用
- 支援防 CSRF
- 提供併發請求
- 相當輕量，約 13kb

```javascript
const result = document.querySelector(".result");

axios
  .get("https://randomuser.me/api/")
  .then(function (response) {
    let data = response.data;
    result.textContent = data.results[0].email;
  })
  .catch(function (err) {
    console.log(err);
  })
  .finally(function () {
    console.log("Execued");
  });
```
