## Leetcode

- [Blind Curated 75 - a list by rockymadden - LeetCode](https://leetcode.com/list/xoqag3yj/)
- [Clay-Technology World - Hope every day is better than yesterday](https://clay-atlas.com/)
- [今回の転職活動の雑感 - seri::diary](https://serihiro.hatenablog.com/entry/2022/04/29/000000)

## Code War

- find odd element
  - `const findOdd = (xs) => xs.reduce((a, b) => a ^ b);`
- unique in order
  - `var uniqueInOrder = function(iterable) { return [...iterable].filter((a, i) => a !== iterable[i-1]) }`
- expandedForm
  ```javascript
  const expandedForm = (n) =>
    n
      .toString()
      .split("")
      .reverse()
      .map((a, i) => a * Math.pow(10, i))
      .filter((a) => a > 0)
      .reverse()
      .join(" + ");
  ```
- delete nth
  ```javascript
  const deleteNth = (a, x) => {
    let m = {};
    return a.filter((v) => (m[v] = m[v] + 1 || 1) <= x);
  };
  ```

## Node Screenshot

1. 選擇要截圖的節點
2. 右鍵 -> 檢查 or `Ctrl` + `Shift` + `I` 開啟開發者工具
3. `Ctrl` + `Shift` + `P`
4. 輸入 `screenshot` -> 選擇 `Capture node screenshot`