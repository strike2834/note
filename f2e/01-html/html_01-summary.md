# HTML 緒論

## What is HTML？

- HTML（HyperText Markup Language）是撰寫網頁結構用的標記語言
- 「標記語言」的意思是直接將「特定寫法」轉換成「對應架構」
  - 以 HTML 來說，就是將各種標籤（ex. `<tag> ... </tag>`）轉換成瀏覽器上的內容架構和元素
- 一個基本 HTML 標籤裡會有「名稱」與「屬性」
  - 格式為 `<tagName attributeName="attributeValue">Content</tagName>`
  - 名稱（tagName）宣告這是什麼標籤，屬性（attributeName）宣告標籤的相關性質
- [HTML Standard](https://html.spec.whatwg.org/multipage/)
- [ECMA-262 - Ecma International](https://www.ecma-international.org/publications-and-standards/standards/ecma-262/)
- [HTML Standard 日本語訳](https://momdo.github.io/html/)
- [HTML Living Standard HTML 要素チートシート](https://htmlls.docs-share.com/)

## HTML 的四大基本結構

一份基礎的 HTML 文件大概像是：

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- head content here -->
  </head>
  <body>
    <!-- content here -->
  </body>
</html>
```

裡頭包含了 HTML 的四大基本結構：

1. `<!DOCTYPE html>`
2. `<html>`
3. `<head>`
4. `<body>`

### 1. `<!DOCTYPE html>`

- 宣告這是一份使用 HTML5 語法標準的文件
- 必須位於文件的第一行
- 前方不可有空格與空行

### 2. `<html>`

- 標記文件正文開始
- HTML 文件檔案的 ROOT（根元素）
- 其他元素都會是此元素的後代
- 可使用 `lang=代碼縮寫` 屬性標註此網頁所使用的語言（IETF 語言標籤）
- 繁體中文的網頁通常使用 `lang="zh-TW"` 或是 `lang="zh-Hant"`

### 3. `<head>`

- 規範與網頁相關資訊（metadata）的區域
- 可設置
  - `<meta>`：設定相關 metadata
  - `<base>`：網頁相對路徑
  - `<title>`：此網頁標題
  - `<style>`：撰寫樣式
  - `<link>`：引用樣式檔案
  - `<script>`：引用 JavaScript 檔案或撰寫 JavaScript
  - `<noscript>`：JavaScript 未執行時的替代顯示內容

#### 3-1. metadata tag

- `<meta name="" content="">`
- [你可以這樣用 HTML 的 Meta 標籤](https://poychang.github.io/how-to-use-html-head/)
- 提供網頁資訊給瀏覽器、搜尋引擎
- 通常用於指定頁面描述、關鍵字、作者…等等資訊
- 常用的 meta name 的屬性值：

| name         | content 說明                                                      |
| ------------ | ----------------------------------------------------------------- |
| author       | 記錄網頁的作者名稱                                                |
| description  | 網頁的簡短描述，內容不能太長，需於 200 個字元（100 個中文字）以內 |
| generator    | 記錄網頁編輯器名稱                                                |
| keywords     | 放置網頁關鍵字，但此屬性目前已幾乎無作用                          |
| distribution | 記錄網頁的發佈地區                                                |

- 也可以控制使用者的瀏覽器 viewport（可見區域）<br />
  └ `meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"`
- 網頁編碼<br />
  └ `meta charset="UTF-8"`
- 早期 HTML4.01 的寫法<br />
  ├`meta http-equiv="屬性值" content="內容"`<br />
  ├ 此屬性值有三種常見的纇型：<br />
  │ `content-type` 設定網頁文字編碼<br />
  │ `default-style` 指定要使用的樣式表<br />
  │ `refresh` 網頁自動刷新的間隔時間<br />
  └ 各屬性值都必須搭配一個 content

#### SEO

- SEO（Search Engine Optimization，搜尋引擎最佳化）也與 metadata tag 有關
  - 搜尋引擎的結果通常與 `<title>` 裡的文字有關
  - 標題底下的簡短說明會是 `<meta name="description" content="網頁簡短描述">` 部份的文字
- 2010 年時 Facebook 制定了一套 Open Graph Protocol 標準，決定相關內容在社群網站要如何呈現
  - 於 `meta` tag 裡改用 `property` 屬性指定：`<meta property="og:type" content="article" />`。
  - [網站管理員 - Sharing](https://developers.facebook.com/docs/sharing/webmasters/)
  - [最佳作法 - Sharing](https://developers.facebook.com/docs/sharing/best-practices)

| property         | content 說明                                                                        |
| ---------------- | ----------------------------------------------------------------------------------- |
| `og:title`       | 網頁內容的標題，不包含網站名稱等任何品牌內容                                        |
| `og:url`         | 網頁內容的網址，此網址應為標準網址（canonical URL）                                 |
| `og:description` | 內容的簡短說明，通常為 2 到 4 個句子                                                |
| `og:image`       | 用戶將內容分享至 SNS 時顯示的圖像網址，建議為 `1.91:1` 比例、最小 `1200x630` 解析度 |
| `og:type`        | 內容的媒體類型，每個網址都應該是單一物件，預設為 `website`                          |
| `og:locale`      | 資源的地區設定，預設為 `en_US`，原生內容以非英文撰寫時才需設定                      |

- [SEO まるわかり大全集](https://tcd-theme.com/introduction-seo)
- [SEO チェキ! 無料で使える SEO ツール](https://seocheki.net/)

另外還可以使用 `robots.txt` 告訴爬蟲遵循什麼規則抓取網頁，以及 `sitemap.xml` 告訴爬蟲整個網域裡存在哪些網頁。

```
User-agent: *
Disallow:
Allow:
sitemap: <sitemap.xml>
```

- [Robots.txt 規範](https://developers.google.com/search/reference/robots_txt?hl=zh-tw)
- [建立並提交 Sitemap](https://developers.google.com/search/docs/advanced/sitemaps/build-sitemap)

### 4. `<body>`

- 網頁文件的主體，主要放置顯示給讀者的內容
- 可設置如容器、文字、連結、圖像、表格、清單等內容
