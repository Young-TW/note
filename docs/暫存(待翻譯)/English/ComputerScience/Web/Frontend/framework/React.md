---
tags: Note
---

# React Note

[TOC]

## jsx file

Example  

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

### jsx tag synatx

In the example jsx file  
The `return` in the Function `App` value is HTML syntax  

### import

在 jsx 檔案最上面通常會 import 其他檔案  
例如 CSS or another jsx file  

### function

