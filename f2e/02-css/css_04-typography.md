# 4. 文字

1.  `color`：文字色彩
2.  `font-size`：字級<br />
    ├ 使用 `em` 時若想簡化換算，可以在 `body` 指定 `font-size: 62.5%;`，<br />
    │ 讓 `1em = 16px x 62.5% = 10px`，這樣 `px` 數只需要除以 10 就能換算成 `em`。<br />
    └ 使用 `rem` 可以避免字體大小逐層複合的連鎖反應，讓所有網頁文字同時等比例縮放。
3.  `font-weight`：字重
4.  `text-align`：文字對齊
5.  `text-decoration`：文字裝飾
6.  `text-indent`：文字首行縮排
7.  `font-family`／`font-style`：字體<br />
    ├ `sans-serif`：英美字體的「無襯線體」，對應到中文的「黑體」。<br />
    ├ `serif`：英美字體的「襯線體」，對應到中文的「明體」。<br />
    ├ `monospace`：等寬字體。常用於程式的原始碼字體。<br />
    ├ `cursive`：手寫風格字體。會依據 OS 與瀏覽器而有大幅差異。<br />
    └ `fantasy`：裝飾風格字體。同樣會依據 OS 與瀏覽器有大幅差異。
8.  `letter-spacing`：字距
9.  `line-height`：行高<br />
    └ 字距用 em，行高用 ex
10. `overflow-wrap: break-word;`：換行<br />
    ├ `word-wrap: break-word;`<br />
    ├ `word-break: break-all;`<br />
    └ `word-break: break-word;`

- [Google Font](https://fonts.google.com/)
- [line-height について考えませんか](https://qiita.com/an_apco/items/87ff859950bc2752ae8c)
- [vw と rem を組み合わせて、4K ディスプレイを考慮した文字サイズを設計する](https://qiita.com/y___k/items/e663c3d9586861b8aa0d)
- [讓文字配合 RWD 網站自動縮放大小](https://medium.com/vhs-design-vitamin-for-creative-mind/font-size-4b4817ac17a3)
- [《網頁設計》舒適的中文文章 CSS 排版設定（附加思源黑體注意事項）](https://www.iamtie.com/2020/09/cssarticlesetting.html)
- [【老貓出版偵察課】易讀性的基本法則（三之一）](https://news.readmoo.com/2014/12/24/guidelines-for-readability-1/)
- [【老貓出版偵察課】易讀性的基本法則（三之二）](https://news.readmoo.com/2015/01/07/guidelines-for-readability-2/)
- [【老貓出版偵察課】易讀性的基本法則（三之三）](https://news.readmoo.com/2015/01/14/guidelines-for-readability-3/)
- [読みやすい＝理解しやすい　 Web の組版を整理してより良い文章を届けよう](https://qiita.com/xrxoxcxox/items/206b223844e3c42dc86f)
