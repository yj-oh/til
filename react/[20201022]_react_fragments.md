# Fragments(<>)
- 컴포넌트 DOM에 별도의 노드를 추가하지 않고 여러 자식 엘리먼트를 그룹화

```javascript
render() {
  return (
    <React.Fragment>
      <span>A</span>
      <span>B</span>
      <span>C</span>
    </React.Fragment>
  );
}
```

- 묶어줄 뿐 자체적으로 형태를 가지지는 않는다.
- 위의 코드는 다음과 같이 변환됨.
```html
<span>A</span>
<span>B</span>
<span>C</span>
```

- 단축 문법으로 이렇게도 쓸 수 있다. `<></>`
```javascript
render() {
  return (
    <>
      <span>A</span>
      <span>B</span>
      <span>C</span>
    </>
  );
}
```
