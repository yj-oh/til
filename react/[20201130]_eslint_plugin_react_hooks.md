# eslint-plugin-react-hooks

### 설치
```
yarn add eslint-plugin-react-hooks
npm install eslint-plugin-react-hooks
```
- 💡 `Create React App`에 포함되어 있음.

### 다음과 같은 규칙을 강제함
1. 최상위(at the Top Level)에서만 Hook을 호출해야 한다.
    - 참고 : [Hook의 규칙]([20201021]_hook_규칙.md)
    
2. 오직 React 함수 내에서 Hook을 호출해야 한다.
    - React 함수 컴포넌트에서 호출
    - Custom Hook에서 호출
