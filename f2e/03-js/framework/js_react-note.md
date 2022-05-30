# React 筆記

- [Fullstack part1 | React 簡介](https://fullstackopen.com/zh/part1/react_%E7%AE%80%E4%BB%8B)
- [React 教學 - React 教學 Tutorial](https://www.fooish.com/reactjs/)
- [React を使うとなぜ jQuery が要らなくなるのか - Qiita](https://qiita.com/naruto/items/fdb61bc743395f8d8faf)
- [\[初心者向け\]React の基礎を徹底解説してみた - Qiita](https://qiita.com/renesisu727/items/98b308ee72281b6f8066#%E3%81%AF%E3%81%98%E3%82%81%E3%81%AB)
- [【React Native】アプリ開発未経験のフロントエンドエンジニアが ToDo リストを作ってみる - Qiita](https://qiita.com/daiend/items/9b7f2eada88ad0dd7c5c)
- [Chakra UI | Design System built with React](https://chakra-ui.com/)
- [デザイナーでも分かる範囲の React、その書き方と学び方 - Qiita](https://qiita.com/xrxoxcxox/items/91f84c6bc3e03deb5853)
- [React を深く知るための入り口](https://zenn.dev/panda_program/articles/deep-dive-into-react)
- [すごい React フック 8 選 - Qiita](https://qiita.com/baby-degu/items/52dbb382bbaf6c43e2db)
- [React ステート管理 比較考察 - uhyo/blog](https://blog.uhy.ooo/entry/2021-07-24/react-state-management/)

## 安裝

```
npx create-react-app@5.0.0 react-app
cd react-app
npm start
```

## JSX

### JSX 簡介

- 什麼是 JSX
  - 舉例：`const element = <h1>Hello, world</h1>;`
  - 這個有趣的標籤語法既不是字串也不是 HTML，它是 JSX，一種 JavaScript 的語法擴充，JSX 可以產生 React「元素」
- 為什麼使用 JSX
  - React 認為渲染邏輯本質上和其他 UI 邏輯內部耦合
  - React 沒有採用人為式的將標記與邏輯分離至不同檔案的方式，而是將兩者共同存於「組件」的鬆散耦合單元，藉此實現關注點分離
- JSX 內嵌入表達式
  - JSX 裡可以使用大括號 `{}` 嵌入表達式
  - 舉例：`const name = 'Josh Perez'; const element = <h1>Hello, {name}</h1>;`
- JSX 也是一種表達式
  - 在編譯之後，JSX 表達式會轉換為普通的 JavaScript 函式呼叫，並在取值後回傳 JavaScript 物件
  - 亦即你可以在 if 語法和 for 迴圈的程式碼區塊使用 JSX，儲存 JSX 至變數，以及從函式中回傳 JSX
- JSX 指定屬性
- 使用 JSX 指定子元素
- JSX 防止插入攻擊
- JSX 顯示物件

```javascript
const App = () => {
  return (
    <div>
      <p>Header</p>
      <p>Content</p>
      <p>Footer</p>
    </div>
  );
};
```

## props

- 向組件傳遞資料
- props 可為任意數量
- 如果傳入的值是 JS 表達式，需用 `{}` 包起

```javascript
const Hello = (props) => {
  return (
    <div>
      <p>
        Hello {props.name}, you are {props.age} years old
      </p>
    </div>
  );
};

const App = () => {
  return (
    <div>
      <h1>Greetings</h1>
      <Hello name="George" age={26 + 10} />
    </div>
  );
};
```

## 如何建構應用

- React 哲學
1. 從設計稿開始
2. 將設計好的 UI 劃分至組件層級
3. 用 React 製作靜態版本
4. 確定 UI state 的最小（且完整）呈現
5. 確定 state 存放位置
6. 加入逆向資料流的 fallback

## props 與 state

- 應清楚理解 props 與 state 的區別
- 透過三個問題，可以檢查該資料是否屬於 state：
  - 該資料是否由親組件 props 傳遞而來？若是，則其不是 state
  - 該資料是否時間過後依然不變？若是，則其不是 state
  - 該資料是否能從其他 state 或 props 計算而來？若是，則其不是 state
- 透過下列步驟，可以確認該有哪個組件擁有 state：
  - 找出所有根據此 state 渲染的組件
  - 找出其共同的擁有者組件（於層級上高於所有根據該 state 的組件）
  - 此共同擁有者組件或比其層級更高的組件應該擁有該 state
  - 若沒有適合的組件可以存放該 state，可另外建立一個高於所有共同擁有者組件的新組件來存放

## helper function

```javascript
const Hello = ({ name, age }) => {
  const bornYear = () => new Date().getFullYear() - age;
  return (
    <div>
      <p>
        Hello {name}, you are {age} years old
      </p>
      <p>So you were probably born in {bornYear()}</p>
    </div>
  );
};
```

## stateful component

```javascript
imoprt React, { useState } from 'react';

function App() {
  const [counter, setCounter] = useState(0);
  setTimeout(() => setCounter(counter + 1), 1000);
  return (
    <div className="App">
      <div>{counter}</div>
    </div>
  );
}
```

## event handling

```javascript
imoprt React, { useState } from 'react';

function App() {
  const [counter, setCounter] = useState(0);
  return (
    <div className="App">
      <div>{counter}</div>
      <button onClick={() => setCounter(counter + 1)}>plus</button>
      <button onClick={() => setCounter(0)}>zero</button>
    </div>
  );
}
```

## passing state to child component

```javascript
const Display = ({ counter }) => <div>{counter}</div>;

const Button = ({ onClick, text }) => <button onClick={onClick}>{text}</button>;

function App() {
  const [counter, setCounter] = useState(0);

  const increaseByOne = () => setCounter(counter + 1);
  const decreaseByOne = () => setCounter(counter - 1);
  const setToZero = () => setCounter(0);

  return (
    <div>
      <Display counter={counter} />
      <Button onClick={increaseByOne} text="plus" /> <Button
        onClick={setToZero}
        text="zero"
      /> <Button onClick={decreaseByOne} text="minus" />{" "}
    </div>
  );
}
```

## complex state

```javascript
function App() {
  const [clicks, setClicks] = useState({
    left: 0,
    right: 0,
  });

  const handleLeftClick = () => setClicks({ ...clicks, left: clicks.left + 1 });

  const handleRightClick = () =>
    setClicks({ ...clicks, right: clicks.right + 1 });

  return (
    <div>
      {clicks.left}
      <button onClick={handleLeftClick}>left</button>
      <button onClick={handleRightClick}>right</button>
      {clicks.right}
    </div>
  );
}
```

## handling array

```javascript
function App() {
  const [left, setLeft] = useState(0);
  const [right, setRight] = useState(0);
  const [allClicks, setAll] = useState([]);
  const handleLeftClick = () => {
    setAll(allClicks.concat("L"));
    setLeft(left + 1);
  };
  const handleRightClick = () => {
    setAll(allClicks.concat("R"));
    setRight(right + 1);
  };
  return (
    <div>
      {left}
      <button onClick={handleLeftClick}>left</button>
      <button onClick={handleRightClick}>right</button>
      {right}
      <p>{allClicks.join(" ")}</p>{" "}
    </div>
  );
}
```

## conditional rendering

```javascript
const History = (props) => {
  if (props.allClicks.length === 0) {
    return <div>the app is used by pressing the buttons</div>;
  }

  return <div>button press history: {props.allClicks.join(" ")}</div>;
};

const Button = ({ handleClick, text }) => (
  <button onClick={handleClick}> {text} </button>
);

function App() {
  const [left, setLeft] = useState(0);
  const [right, setRight] = useState(0);
  const [allClicks, setAll] = useState([]);

  const handleLeftClick = () => {
    setAll(allClicks.concat("L"));
    setLeft(left + 1);
  };

  const handleRightClick = () => {
    setAll(allClicks.concat("R"));
    setRight(right + 1);
  };

  return (
    <div>
      {left}
      <Button handleClick={handleLeftClick} text="left" /> <Button
        handleClick={handleRightClick}
        text="right"
      /> {right}
      <History allClicks={allClicks} />
    </div>
  );
}
```

## rendering collections

### `Note.js`

```javascript
import React from "react";

const Note = ({ note }) => {
  return <li>{note.content}</li>;
};

export default Note;
```

### `App.js`

```javascript
import React from "react";
import Note from "./components/Note";

function App({ notes }) {
  return (
    <div>
      <h1>Notes</h1>
      <ul>
        {notes.map((note) => (
          <Note key={note.id} note={note} />
        ))}
      </ul>
    </div>
  );
}
```

### `index.js`

```javascript
const notes = [
  {
    id: 1,
    content: "HTML is easy",
    date: "2020-06-01T17:30:31.098Z",
    important: true,
  },
  {
    id: 2,
    content: "Browser can execute only Javascript",
    date: "2020-06-01T18:39:34.091Z",
    important: false,
  },
  {
    id: 3,
    content: "GET and POST are the most important methods of HTTP protocol",
    date: "2020-06-01T19:20:14.298Z",
    important: true,
  },
];

ReactDOM.render(
  <React.StrictMode>
    <App notes={notes} />
  </React.StrictMode>,
  document.getElementById("root")
);
```

## filtering displayed elements

`App.js`

```javascript
function App(props) {
  const [notes, setNotes] = useState(props.notes);
  const [newNote, setNewNote] = useState("a new note...");
  const [showAll, setShowAll] = useState(true);
  const addNote = (event) => {
    event.preventDefault();
    const noteObject = {
      content: newNote,
      date: new Date().toISOString(),
      important: Math.random() < 0.5,
      id: notes.length + 1,
    };

    setNotes(notes.concat(noteObject));
    setNewNote("");
  };
  const handleNoteChange = (event) => {
    console.log(event.target.value);
    setNewNote(event.target.value);
  };
  const notesToShow = showAll
    ? notes
    : notes.filter((note) => note.important === true);
  return (
    <div>
      <h1>Notes</h1>
      <div>
        <button onClick={() => setShowAll(!showAll)}>
          show {showAll ? "important" : "all"}
        </button>
        <ul>
          {notesToShow.map((note) => (
            <Note key={note.id} note={note} />
          ))}
        </ul>
        <form onSubmit={addNote}>
          <input value={newNote} onChange={handleNoteChange} />
          <button type="submit">save</button>
        </form>
      </div>
    </div>
  );
}
```

## effect-hooks

`npx json-server --port 3001 --watch db.json`

`App.js`

```javascript
import React, { useState, useEffect } from "react";
import axios from "axios";

function App() {
  const [notes, setNotes] = useState([]);
  const [newNote, setNewNote] = useState("");
  const [showAll, setShowAll] = useState(true);
  const hook = () => {
    console.log("effect");
    axios.get("http://localhost:3001/notes").then((response) => {
      console.log("promise fulfilled");
      setNotes(response.data);
    });
  };

  useEffect(hook, []);
  console.log("render", notes.length, "notes");
  // ...
}
```

## sending data to the server

`App.js`

```javascript
// ...
const addNote = (event) => {
  event.preventDefault();
  const noteObject = {
    content: newNote,
    date: new Date().toISOString(),
    important: Math.random() < 0.5,
  };

  axios.post("http://localhost:3001/notes", noteObject).then((response) => {
    setNotes(notes.concat(response.data));
    setNewNote("");
  });
};
// ...
```

## changing the importance of notes

`Note.js`

```javascript
// ...
const Note = ({ note, toggleImportance }) => {
  const label = note.important ? "make not important" : "make important";
  return (
    <li>
      {note.content}
      <button onClick={toggleImportance}>{label}</button>
    </li>
  );
};
// ...
```

`App.js`

```javascript
// ...
const toggleImportanceOf = (id) => {
  const url = `http://localhost:3001/notes/${id}`;
  const note = notes.find((n) => n.id === id);
  const changedNote = { ...note, important: !note.important };

  axios.put(url, changedNote).then((response) => {
    setNotes(notes.map((note) => (note.id !== id ? note : response.data)));
  });
};
// ...
<ul>
  {notesToShow.map((note) => (
    <Note
      key={note.id}
      note={note}
      toggleImportance={() => toggleImportanceOf(note.id)}
    />
  ))}
</ul>;
// ...
```

## extracting communication into a seperate module

`services/notes.js`

```javascript
import axios from "axios";
const baseUrl = "http://localhost:3001/notes";

const getAll = () => {
  return axios.get(baseUrl);
};

const create = (newObject) => {
  return axios.post(baseUrl, newObject);
};

const update = (id, newObject) => {
  return axios.put(`${baseUrl}/${id}`, newObject);
};

const exportedObject = {
  getAll: getAll,
  create: create,
  update: update,
};

export default exportedObject;
```

`App.js`

```javascript
import noteService from "./services/notes";
// ...
useEffect(() => {
  noteService.getAll().then((response) => {
    setNotes(response.data);
  });
}, []);
const toggleImportanceOf = (id) => {
  const note = notes.find((n) => n.id === id);
  const changedNote = { ...note, important: !note.important };

  noteService.update(id, changedNote).then((response) => {
    setNotes(notes.map((note) => (note.id !== id ? note : response.data)));
  });
};
const addNote = (event) => {
  event.preventDefault();
  const noteObject = {
    content: newNote,
    date: new Date().toISOString(),
    important: Math.random() > 0.5,
  };

  noteService.create(noteObject).then((response) => {
    setNotes(notes.concat(response.data));
    setNewNote("");
  });
};
```
