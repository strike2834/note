# docsify - 即時轉譯 Markdown 成為網頁

- [Docsify](https://docsify.js.org/) 是一套以 Vue 為基底所撰寫，即時解析 markdown 檔案產生網頁頁面的靜態網站產生器
- 特徵是初始化完畢後，只需要 `index.html` 和 markdown 檔案即可運作，不需進行 build

## 安裝

```bash
npm i docsify-cli -g

# 初始化
docsify init ./檔案放置資料夾

# 預覽
docsify serve docs
```

## 檔案結構

初始化完畢後，目標資料夾底下會產生三個檔案

- `index.html`：主頁面（進入點），以及和設定相關的內容
- `README.md`：主頁面（進入點）的內容
- `.nojekyll`：使 Github Pages 不忽略名稱以 `_` 開頭的檔案

### 路由

Docsify 以資料夾進行分層，並藉此決定路徑，例如：

```
.
├── 檔案放置資料夾
│   ├── 2017
│   ├── 2018
│   ├── 2019
│   │   ├── YYYYMMDD_作業事項
│   │   │   ├── README.md    // 說明書
│   │   │   ├── _sidebar.md  // 側邊欄（資料樹狀大綱）
│   │   │   └── image.png    // 說明書內的使用圖片
│   │   ├── YYYYMMDD_作業事項
│   │   │   ...
│   │   └── README.md
│   ├── .nojekyll
│   ├── README.md
│   ├── _sidebar.md
│   └── index.html
├── node_modules
├── package.json
├── script
└── yarn.lock
```

存取 `YYYYMMDD_作業事項` 的路徑就會是 `/2019/YYYYMMDD_作業事項`。

並且可透過 `_sidebar.md` 加入側邊欄、 `_navbar.md` 加入下拉選單，而這些指引功能檔案的內容需自行以清單格式撰寫：

```markdown
- [需求規格](spec.md "需求規格")
  - [內容 A](speccontentA.md "內容A")
  - [內容 B](speccontentB.md "內容B")
- [時程安排](schedule.md "時程安排")
- [開發者技術](dev.md "開發者技術")
- [API 文件](api.md "API 文件")
- [DB schema](dbSchema.md "DB schema")
- [其他文件紀錄](otherDocument.md "其他文件紀錄")
```

加入 `_sidebar.md` 之後，還需要在 `index.html` 裡開啟相關功能選項

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadSidebar: true,
  };
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

## Deploy

- [Deploy](https://docsify.js.org/#/deploy)

## 參考資料

- [Docsify - Quick start](https://docsify.js.org/#/quickstart)
