# BrowserRouter
- react-router-dom 내장 컴포넌트
   - `HashRouter`와 `BrowserRouter`가 있다.
- HTML5의 History API를 사용하여 페이지 새로고침 없이 주소 변경, UI update

#### 👉 package 추가
- react-router-dom 내장 컴포넌트이므로 당연히 `react-router-dom` 추가
```
yarn add react-router-dom
npm install react-router-dom
```

#### 👉 src/index.js
- 아래와 같이 적용
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

ReactDOM.render(
    <BrowserRouter>
        <App />
    </BrowserRouter>,
    document.getElementById('root'),
);

reportWebVitals();
```
