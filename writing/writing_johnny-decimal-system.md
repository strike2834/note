# [JD 整理術](https://tw.alphacamp.co/blog/johnny-decimal-system)

使用兩層十進位的值來分類，分別是：

- 領域（Area）：每種領域以同個首數做分類，例如「財務」相關領域占用 1 開頭的 10 ～ 19，上限 10 個。
- 類別（Category）：每種領域再進一步細分，例如財務領域的 10 ～ 19 底下細分為 11 信用卡帳單、12 券商對帳單、13 貸款、14 稅單、15 保單…etc. 上限同為 10 個。

之後再加上一個辨識用的流水號，一份文件就可組成 AC.ID 的專屬代號：

- 流水號（Id）：例如 14.28 2020 所得稅收執聯 的 1 代表財務領域，4 代表稅單分類，後面的 28 便是此文件專有的流水號

如果數量不夠用，可以改為採用**多個子 JD 系統**或是**使用不同的進位制**，例如改為 16 進位等等。