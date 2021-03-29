# Controlled vs Uncontrolled components
## Controlled components
- form element를 렌더링하는 React 컴포넌트가 form에 발생하는 사용자 입력값을 제어
  - state, setState()
- 모든 입력 상태를 관리하는 게 피로할 수 있다.
  - 대안 : `Uncontrolled components`
- _https://ko.reactjs.org/docs/forms.html#controlled-components_

## Uncontrolled components
- 상태를 React 컴포넌트가 관리하는 controlled component와 달리,
  DOM 자체에서 입력값을 관리
- 빠르고 간편하게 적은 코드를 작성 가능하지만 일반적으로 controlled component를 사용해야 함.

## +) uncontrolled component를 사용하며 만난 에러
```text
Failed form propType: You provided a `value` prop to a form field 
without an `onChange` handler
```

### 상황
- 속성값을 props로 받아 input element를 반환하는 공통 input 컴포넌트를 작성했다.
- 검색 input은 따로 상태값을 관리하지 않고 
  DOM 자체에서 관리하도록 했다. (uncontrolled component)
  - 그래서 onChange를 정의하지 않고, name, type, onKeyDown 정도만 정의
- 공통 컴포넌트에 value값 보정을 위해 value 속성을 고정해두었다.
- 검색 input에 공통 컴포넌트를 적용하면서 name, type, onKeyDown, value 속성이 지정되었고
  위의 에러 발생.
- 결과적으로 아래의 element
```jsx
<input
    type='input'
    name='search'
    onKeyDown={onKeyDown}
    value='hi'
/>
```

### 해결 - 3가지 방법
1. `value` 대신 `defaultValue` 속성 사용하기
```jsx
<input
    type='input'
    name='search'
    onKeyDown={onKeyDown}
    defaultValue='hi'
/>
```
2. 또는 `onChange` 속성 추가하기
```jsx
<input
    type='input'
    name='search'
    onKeyDown={onKeyDown}
    value='hi'
    onChange={onChange}
/>
```
3. 또는 `readOnly`로 사용하기
```jsx
<input
    type='input'
    name='search'
    onKeyDown={onKeyDown}
    value='hi'
    readOnly
/>
```

##### * References
- https://ko.reactjs.org/docs/forms.html#controlled-components
- https://ko.reactjs.org/docs/uncontrolled-components.html
