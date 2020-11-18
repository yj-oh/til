# Route exact path
## exact
- 경로가 정확히 일치하는지 여부
```jsx
<Route component={MainPage}  path="/" />
<Route component={LoginPage} path="/login" />
<Route component={ListPage}  path="/list" />
<Route component={PostPage}  path="/post" />
```
- 위와 같을 때, 어떤 path로 접근하든 MainPage를 함께 탄다.
- 다른 path에도 `/`가 포함되어 있기 때문이다.

```jsx
<Route component={MainPage}  path="/" exact />
<Route component={LoginPage} path="/login" />
<Route component={ListPage}  path="/list" />
<Route component={PostPage}  path="/post" />
```
- `/`에 exact true를 설정하면 정확히 `/`로 들어왔을 때에만 MainPage를 탄다.

---

### install react-router-dom
```
npm install react-router-dom
yarn add react-router-dom
```

### index.js
```jsx
import React from 'react';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
  document.getElementById('root'),
);

serviceWorker.unregister();
```

### App.js
```jsx
import React from 'react';
import { Route } from 'react-router-dom';
import MainPage from './pages/MainPage';
import SubPage from './pages/SubPage';
import LoginPage from './pages/LoginPage';

const App = () => {
  return (
    <>
      <Route component={LoginPage} path="/login" exact />
      <Route component={MainPage}  path="/:type" exact />
      <Route component={SubPage}   path="/:type/:id" />
    </>
  );
};

export default App;
```

### 그러나 위와 같이 구성했을 때,
- `/login`으로 접근하면 LoginPage, MainPage를 둘 다 탄다.

### Switch를 활용하자
### App.js
```jsx
import React from 'react';
import { Route, Switch } from 'react-router-dom';
import MainPage from './pages/MainPage';
import SubPage from './pages/SubPage';
import LoginPage from './pages/LoginPage';

const App = () => {
  return (
    <Switch>
      <Route component={LoginPage} path="/login" exact />
      <Route component={MainPage}  path="/:type" exact />
      <Route component={SubPage}   path="/:type/:id" />
    </Switch>
  );
};

export default App;
```
- `/login`으로 접근하면 해당 컴포넌트를 띄우고 끝낸다.
