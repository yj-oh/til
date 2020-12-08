# Nullish coalescing operator
- `??`
- 값이 `null`이거나 `undefined`면 기본값

```javascript
function test(x) {
    return x ?? 'Unknown';
}

console.log(test(1));           // 1
console.log(test(null));        // Unknown
console.log(test(undefined));   // Unknown
```
```javascript
const user = {
    id: null,
    name: null,
};
console.log(user.id ? user.id : '뉴비');
// 기존에 위와 같이 쓰던 것을 아래와 같이 쓸 수 있다.
console.log(user.id ?? '뉴비');
```

### `?.`랑 뭔 차이?
- `??`는 `null`이거나 `undefined`인 값을 특정값으로 처리
- `?.`는 `null`이거나 `undefined`일 수 있는 객체에 접근
