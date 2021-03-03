# Entry point : index.html vs index.js
- 프로젝트를 하며 처음으로 Azure를 경험하고 있다.
- Azure 환경에서 React application을 띄우며 404 에러를 만났다.
```text
The requested content does not exist.
* HttpStatusCode: 404
* ErrorCode: WebContentNotFound
* RequestId: 
* TimeStamp: 2021-03-02T11:01:14.8223123Z
```
- `/`로 접근했을 때는 문제 없이 페이지를 띄우는데,
  `/login`등 uri template 변수를 넣으면 404 error가 뜨는 상황.
- 에러 해결을 위해 생각의 생각을 거듭하다가 
  겸사겸사 React entry point에 대한 고찰을 하게 되었다.
- 그 내용을 정리한다.

---

# 기본 구조
- `create-react-app`으로 생성한 react application
- 기본적으로 생성되는 구조가 있는데, 항상 존재하는 파일들만 구조화 해보면 아래와 같다.
```text
🗂 project
|-- 📂 public
|   `-- 📋 index.html
|-- 📂 src
|   |-- 📋 App.js
|   `-- 📋 index.js
```
- `App.js`는 단순히 index.js 안에 렌더링 되는 애라서 무시하고.
- 이름만 봐도 Entry point 인 `index.html`, `index.js`의 내용을 보면 아래와 같다.

### index.html
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="description"
      content="Web site created using create-react-app"
    />
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <title>React App</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```

### index.js
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

# index.js 살펴보기
```jsx
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```
- ReactDOM.render()
  - ```
    ReactDOM.render(element, container[, callback])
    ```
  - `element`를 `container` DOM에 렌더링한다.
- `document.getElementById('root')`는 index.html에 있다.
  - ```html
    <!DOCTYPE html>
    <html lang="en">
      <body>
        <div id="root"></div>
      </body>
    </html>
    ```
  - 한 마디로 설명하면 index.js에 의해 실행되고 반환되는 모든 React element들은 
    저 `<div id="root">`에 끼워넣어진다.
  - **Single Page Application!**

- 근데 아무리 봐도 index.html이 먼저 불러와지는지, index.js가 먼저 불러와지는지 모르겠다.
- index.html에 index.js가 끼워져있나 봤는데 그것도 아니고 둘은 무슨 관계지?
- 아무리 봐도 둘 사이에 접점이 없어보인다.
- 구글링, 그리고 찾은 글.
  - [stackoverflow - Where's the connection between index.html and index.js in a Create-React-App application?](https://stackoverflow.com/questions/42438171/wheres-the-connection-between-index-html-and-index-js-in-a-create-react-app-app)

# index.js와 index.html의 접점
- create-react-app은 `node_modules/html-webpack-plugin`을 사용하고
  webpack은 `html-webpack-plugin/index.js`을 entry point로 사용한다.
- `node_modules/html-webpack-plugin/index.js`를 보자.
```typescript jsx
const defaultOptions = {
  // ...
  filename: 'index.html',
  inject: true,
  // ...
};
```
- index.html을 템플릿으로 읽어야 한다고 지정해놨다.
- inject 옵션은 `true`다.
  - `true` || `'head'` || `'body'` || `false`
    - `true` : Passing true will add it to the head/body depending on the scriptLoading option
    - `head` <head>에 <script> 넣는다.
    - `body` <body>에 <script> 넣는다.
    - `false` : Passing false will disable automatic injections.
    - 참고 : https://github.com/jantimon/html-webpack-plugin
- 플러그인이 <body>에 <script>를 알아서 삽입해준다.
- 이해한 대로 결론을 내려보면,
  create-react-app이 사용하는 `node_modules/html-webpack-plugin`에
  index.html을 템플릿으로 지정하는 설정이 있고,
  템플릿 안에 <script>를 알아서 삽입하는 설정이 있어서 
  index.html과 index.js의 연결고리가 만들어진다.
  
```text
This final page is the one you get in build/index.html after running npm run build, 
and the one that gets served from / when you run npm start.
```
