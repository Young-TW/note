---
tags: 筆記
---

# React 筆記

[TOC]

## jsx 檔案

直接看範例

```jsx=
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;

```

### jsx 標籤語法

上面的 jsx 檔案內  
函式 App 中的 return 值就是 HTML 的寫法  

### import

在 jsx 檔案最上面通常會 import 其他檔案  
例如 CSS 或其他 jsx 檔案  

### function

