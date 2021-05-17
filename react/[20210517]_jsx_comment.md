# JSX 주석
```jsx
{/* 주석 */}
```
- 태그 내부에서는 `//` 주석 사용 가능
```jsx
<div
  id='container'
  // 태그 내부
>
  <p>Hello, World!</p>
</div>
```
- 아래는 Error!
```jsx
const Test = () => {
    return (
        {/* 주석 */}
        <div id='container'>
            <p>Hello, World!</p>
        </div>
    );
};
```
- `<React.Fragment>` 감싸줘야 한다.
```jsx
const Test = () => {
    return (
        <>
            {/* 주석 */}
            <div id='container'>
                <p>Hello, World!</p>
            </div>
        </>
    );
};
```
