# VSCode

## VSCode 快捷鍵

- [VS Code 23 個常用快捷鍵速查表](https://hackmd.io/@sean666/HJ3x8K6Z8)
- [Visual Studio Code 快速鍵一覽表](https://poychang.github.io/vscode-shortcuts/)
- [過去の自分に教えなければならない VSCode のショートカット - Qiita](https://qiita.com/rana_kualu/items/ea78200036fc80dce0a9)

| 按鍵                      | 功能                                              |
| ------------------------- | ------------------------------------------------- |
| `Ctrl` + `P`              | 跳至指定檔案<br>加上 `:行數` 會再自動跳至指定行數 |
| `Ctrl` + `G`              | 跳至指定行數處                                    |
| `Ctrl` + `B`              | 顯示／隱藏側邊欄                                  |
| `Ctrl` + `Shift` + `E`    | 跳至左側檔案管理處                                |
| `Ctrl` + `Shift` + `L`    | 反白所有指定文字                                  |
| `Ctrl` + `Shift` + `H`    | 跳至搜尋欄                                        |
| `Ctrl` + `Q`              | 切換終端                                          |
| `Ctrl` + `R`              | 切換工作區                                        |
| `Ctrl` + `L`              | 反白當前行內容                                    |
| `Alt` + `↑／↓`            | 移動當前行內容                                    |
| `Shift` + `Alt` + `↑／↓`  | 快速複製當前行內容                                |
| `Shift` + `Alt` + `F`     | 格式化文件                                        |
| `Ctrl` + `K` `F`          | 關閉當前資料夾                                    |
| `Ctrl` + `K` `Z`          | 禪模式                                            |
| `Ctrl` + `K` `Ctrl` + `S` | 鍵盤快捷鍵                                        |
| `Ctrl` + `K` `Ctrl` + `O` | 開啟指定資料夾                                    |
| `Ctrl` + `Shift` + `P`    | Master Key                                        |

## setting.json

```json
{
  "editor.fontFamily": "'Myrica M', 'Input Font Mono', Consolas, 'Courier New', monospace",
  "editor.fontSize": 16, // 更改字體大小
  "editor.renderControlCharacters": true, // 顯示控制字元
  "editor.renderLineHighlight": "all", // 突顯選擇中的行數號碼
  "editor.cursorStyle": "block", // 更改錨點的外觀成方塊狀
  "editor.bracketPairColorization.enabled": true, // 替括弧加上對應色
  "editor.rulers": [80, 120], // 加上邊界線
  "editor.tabCompletion": "on", // Tab 鍵自動完成
  "files.autoGuessEncoding": true, // 自動選擇檔案編碼
  "files.autoSave": "onFocusChange", // 切換檔案時自動儲存
  "editor.formatOnSave": false, // 存檔時不自動排版
  "breadcrumbs.enabled": true // 顯示檔案的麵包屑列表
}
```

## VSCode 插件

- [VSCode のオススメ拡張機能 24 選 (と Tips をいくつか)](https://qiita.com/sensuikan1973/items/74cf5383c02dbcd82234#1-vscode-icons)
- [JavaScript 開発者のための優秀な VSCode ツール 26 選](https://qiita.com/rana_kualu/items/4a4ce6ea7f489dc19f63)
- [これがなくては生きていけない VS Code エクステンション 10 選 - Qiita](https://qiita.com/rana_kualu/items/9f6919311f1407a71c5f)
- [The Ultimate VSCode Setup for Front End/JS/React](https://medium.com/productivity-freak/the-ultimate-vscode-setup-for-js-react-6a4f7bd51a2)

### 外觀樣式

| 名稱                                                                                                          | 說明                          |
| ------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| [Bracket Pair Colozier](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer) | 括號上色                      |
| [Indent-rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow)                  | 色彩區隔不同深度的縮排        |
| [Output Colorizer](https://marketplace.visualstudio.com/items?itemName=IBM.output-colorizer)                  | 色彩化 VSCode 的 Console 輸出 |

### 內容生成

| 名稱                                                                                                                            | 說明                                            |
| ------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| [Auto Rename Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag)                            | 自動修改前後對應標籤                            |
| [Auto Close Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-close-tag)                              | 自動關閉標籤                                    |
| [JAVASCRIPT (ES6) CODE SNIPPETS](https://marketplace.visualstudio.com/items?itemName=xabikos.JavaScriptSnippets)                |                                                 |
| [File Utils](https://marketplace.visualstudio.com/items?itemName=sleistner.vscode-fileutils)                                    | `F1` -> 輸入 `File:` 處理複製、移動、新增等功能 |
| [advanced-new-file](https://marketplace.visualstudio.com/items?itemName=patbenatar.advanced-new-file)                           | `cmd+alt+n` (Mac), `ctrl+alt+n` (Win, Linux)    |
| [PATH INTELLISENSE](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)                     | 自動補完輸入檔案路徑                            |
| [IntelliSense for CSS class names in HTML](https://marketplace.visualstudio.com/items?itemName=Zignd.html-css-class-completion) | 自動從已輸入的 HTML class 內補完命名            |
| CSS PEEK                                                                                                                        | 可以從 CSS class 名稱直接跳至對應定義           |

#### USER SNIPPET

- 透過快捷鍵快速產生內容
- 完全由使用者自訂
- `File（檔案）` -> `Preferences（喜好設定）` -> `User Snippets（使用者程式碼片段）`
- [snippet generator](https://snippet-generator.app/)
- [Using Current Date and Time In VS Code Snippets - DEV](https://dev.to/chaseadamsio/using-current-date-and-time-in-vs-code-snippets-4gog)

```json
{
  "Print to console": {
    "scope": "javascript,typescript",
    "prefix": "log",
    "body": ["console.log('$1')", "$2"],
    "description": "Log output to console"
  }
}
```

- `scope`：指定此 snippets 的使用語言
- `prefix`：指定此 snippets 的快捷關鍵字
- `description`：顯示此 snippets 時右邊的內容說明
- `body`：此 snippets 的實際輸入內容
- `$1`、`$2`：可以在按下 Tab 鍵後讓錨點跳至此處

### 輔助工具

| 名稱                                                                                                                                  | 說明                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| [GITLENS](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)                                                        |                                                                      |
| [Setting Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync)                                           | Upload Key : `Shift + Alt + U` <br> Download Key : `Shift + Alt + D` |
| [Quokka.js](https://marketplace.visualstudio.com/items?itemName=WallabyJs.quokka-vscode)                                              | `Ctrl/Cmd + Shift + P` -> type `Quokka`                              |
| [Wallaby.js](https://marketplace.visualstudio.com/items?itemName=WallabyJs.wallaby-vscode)                                            | `Ctrl/Cmd + Shift + P` -> type `Wallaby` OR `Ctrl/Cmd + Shift + =`   |
| [PROJECT MANAGER](https://marketplace.visualstudio.com/items?itemName=alefragnani.project-manager)                                    |                                                                      |
| [BLUEPRINT - NEW FILES AND FOLDERS OF FILES FROM TEMPLATES](https://marketplace.visualstudio.com/items?itemName=teamchilla.blueprint) | 建立泛用樣板檔案                                                     |
| [Search Docsets](https://marketplace.visualstudio.com/items?itemName=silverlakesoftware.searchdocsets-vscode)                         | `Shift + F1`                                                         |

#### Blueprint

- 模板資料夾預設存在 `blueprint-templates` 資料夾底下
- 可以依據官方說明文裡面，在 `settings.json` 裡面修改參照模板資料夾的路徑
- `"blueprint.templatesPath": ["./.vscode/blueprint-templates"`
- 模板分類概念是最外面的 Folder 是替模板命名用，裡面的子層資料夾才會收納模板檔案
- 可以使用 `__name__` 從輸入自訂資料夾或檔案的名稱，檔案內的自訂名稱則要改為雙括寫法 `{{name}}`
- 其它常用的命名法有 `__pascalCase_name__` 和 `__lowerDotCase_name__`
- 可以使用 `$` 開頭自行命名額外變數

### 規範限制

| 名稱                                                                                                            | 說明                                 |
| --------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| [Error Lens](https://marketplace.visualstudio.com/items?itemName=usernamehw.errorlens)                          | 顯示錯誤訊息於對應行上               |
| Code Spell Checker                                                                                              | 檢查拼字錯誤                         |
| [GREMLINS TRACKER](https://marketplace.visualstudio.com/items?itemName=nhoizey.gremlins)                        | 檢查難以辨識的問題字元               |
| [CODE SPELL CHECKER](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) |                                      |
| [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)                          | `CMD + Shift + P` -> Format Document |
| [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)                            |                                      |
| [DOCUMENT THIS](https://marketplace.visualstudio.com/items?itemName=joelday.docthis)                            | `Ctrl+Alt+D` and again `Ctrl+Alt+D`  |
| [Add jsdoc comments](https://marketplace.visualstudio.com/items?itemName=stevencl.addDocComments)               | `F1` -> `Add doc comments`           |
| [Import Cost](https://marketplace.visualstudio.com/items?itemName=wix.vscode-import-cost)                       | 顯示引用檔案大小                     |
| [CODEMETRICS](https://marketplace.visualstudio.com/items?itemName=kisstkondoros.vscode-codemetrics)             | 顯示函式的計算複雜度                 |

### 彩蛋番外

| 名稱                                                                                      | 說明                     |
| ----------------------------------------------------------------------------------------- | ------------------------ |
| [POLACODE](https://marketplace.visualstudio.com/items?itemName=pnp.polacode)              | 截取程式碼片段儲存為圖片 |
| [LEETCODE](https://marketplace.visualstudio.com/items?itemName=shengchen.vscode-leetcode) | 在 VSCode 上解 LeetCode  |
