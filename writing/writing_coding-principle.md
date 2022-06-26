# [何かのときにすっと出したい、プログラミングに関する法則・原則一覧](https://qiita.com/hirokidaichi/items/d6c473d8011bd9330e63)

## [得墨忒耳定律](https://zh.wikipedia.org/wiki/%E5%BE%97%E5%A2%A8%E5%BF%92%E8%80%B3%E5%AE%9A%E5%BE%8B)

又名「最少知識原則」。

> 每個單元應當僅擁有對於其他單元（包含子單元）的構造或屬性最小限度的知識。

即物件應當不可直接觸及成員的屬性或方式。例如：

```javascript
// 違反得墨忒耳定律
console.log(aStudent.class.grade);

// 遵守得墨忒耳定律
console.log(aStudent.getGrade());
```

## [維爾特定律](https://zh.wikipedia.org/wiki/%E7%B6%AD%E7%88%BE%E7%89%B9%E5%AE%9A%E5%BE%8B)

來自經驗法則的「軟體變慢的速度永遠快過硬體變快的速度。」

## [布魯克斯法則](https://zh.wikipedia.org/wiki/%E5%B8%83%E9%B2%81%E5%85%8B%E6%96%AF%E6%B3%95%E5%88%99)

來自經驗法則的「在一個已經進度落後的軟體項目上再增加人力，只會使這個軟體項目進度更加落後。」

由於隱含著「熟悉一個項目所需的時間」、「增加的溝通成本」等背景因素。

## [康威定律](https://zh.wikipedia.org/wiki/%E5%BA%B7%E5%A8%81%E5%AE%9A%E5%BE%8B)

「設計系統的組織，會將自己組織的溝通構造直接複製至系統上」

即系統設計本質上反映了企業的組織機構。系統各個模組之間的接口也反映了企業各個部門之間的訊息流動和合作方式。

## [侯世達定律](https://zh.wikipedia.org/wiki/%E4%BE%AF%E4%B8%96%E8%BE%BE%E5%AE%9A%E5%BE%8B)

「做事所花費的時間總是比你預期的要長，即使你的預期中考慮了侯世達定律。」

## [最小驚訝原則](https://en.wikipedia.org/wiki/Principle_of_least_astonishment)

「當介面存在兩個互相矛盾或關係不明瞭的元素，應當選擇在動作上對於人類使用者與程式設計師最自然（最少驚訝）的一方」

## 童子軍定律

「要離開時的營地比進入時更加乾淨。」

於軟體開發裡則是意味「存入模組時，必須比取得模組時更漂亮」

## [YAGNI](https://zh.wikipedia.org/wiki/YAGNI)

「You aren't gonna need it」

應在確定有其必要時，才加入該功能。

## [DRY](https://zh.wikipedia.org/wiki/%E4%B8%80%E6%AC%A1%E4%B8%94%E4%BB%85%E4%B8%80%E6%AC%A1)

「Don't repeat yourself」

## [KISS](https://zh.wikipedia.org/wiki/KISS%E5%8E%9F%E5%88%99)

「Keep it simple, stupid」

## [SOLID](https://zh.wikipedia.org/wiki/SOLID_%28%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E8%AE%BE%E8%AE%A1%29)

- S：Single Responsibility Principle（單一功能原則）
  - 「物件應該僅具有一種單一功能」
- O：Open/closed principle（開閉原則）
  - 「軟體應當對於擴充是開放的，但對於修改是封閉的」
- L：Liskov substitution principle（里氏替換原則）
  - 「應當可以在不改變程式正確性的前提下，替換物件與其子類」
- I：Interface segregation principle（介面隔離原則）
  - 「不可強制客戶端依賴於不使用的方法」
- D：Dependency inversion principle（依賴反轉原則）
  - 「上層的模組不可依賴下層的模組。每個模組都應該是『抽象』的」

