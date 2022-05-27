# TypeScript

- [Fullstack part9 - Typescript](https://fullstackopen.com/zh/part9/%E8%83%8C%E6%99%AF%E4%B8%8E%E4%BB%8B%E7%BB%8D)

## 介紹

- TypeScript 是一個類型化的 JavaScript 超集，它最終會被編譯成純的 JavaScript 代碼
- TypeScript 由三個獨立但相互滿足的部分組成：
  - The language
  - The compiler
  - The language Service
- TypeScript 的主要語言特性：

  - Type annotations 類型註解

  ```javascript
  const birthdayGreeter = (name: string, age: number): string => {
    return `Happy birthday ${name}, you are now ${age} years old!`;
  };
  ```

  - Structural typing 結構化類型
  - Type inference 類型推斷

  ```javascript
  const add = (a: number, b: number) => {
    /* The return value is used to determine
     the return type of the function */
    return a + b;
  };
  ```

  - Type erasure 類型擦除

## 使用

- TypeScript 需要編譯，因此需要編譯環境
  - `npm install -g ts-node typescript`
  - 修改 `package.json`：`"scripts":{ "ts-node": "ts-node" },`
  - `npm run ts-node`
- 或是使用[線上版的 Playground](https://www.typescriptlang.org/play)
