# Marp 

- VSCode 上的插件 Marp 
- 可將 markdown 檔案產出為既有的網頁形式
- 還可以轉換成 pdf 或 PowerPoint 等格式

## 安裝

- [Marp for VS Code - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode)
- 安裝完成後，開啟 markdown 檔案時上方會多出預覽和輸出的圖示，<br/>
  點選輸出圖示的 `Export slide deck...` 就可完成轉檔
- 另外 Marp 也有 cli 的版本，<br/>
  可以透過 npx 執行：`npx @marp-team/marp-cli slide-deck.md --pptx`
- [@marp-team/marp-cli - npm](https://www.npmjs.com/package/@marp-team/marp-cli)

## 撰寫

撰寫給 Marp 使用的 markdown 檔案時，需要在 yaml header 的部份加上 `marp: true`

投影片格式的 markdown 習慣上以分隔線 `---` 做分頁

```markdown
---
marp :true
---

# Your slide deck

Start writing!

---

# Next Slide

Content here.

---

# Another Slide

Some content.

---
```

使用 Marp 可以再加上 `headingDivider` 改為要以第幾號標題決定分頁，方便將既有的文章快速轉換成投影片

```markdown
---
marp :true
---

<!--
headingDivider: 2
-->

# 1st page

The content of 1st page

## 2nd page

### The content of 2nd page

Hello, world!

# 3rd page

😃
```

還可以再以 `theme` 決定投影片樣式主題、`header` 和 `footer` 設定投影片頭部和尾部內容，或是 `backgroundColor` 等參數進行更多設定

更多詳細內容可以參照官方文件的 [directives.md](https://github.com/marp-team/marpit/blob/master/docs/directives.md)

## 參考文章

- [【VS Code + Marp】Markdown から爆速・自由自在なデザインで、プレゼンスライドを作る - Qiita](https://qiita.com/tomo_makes/items/aafae4021986553ae1d8)
