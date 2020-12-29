# Parameter defaults
```javascript
function add(x, y) {
    return x + y;
}
console.log(add());         // NaN
console.log(add(1));        // NaN
console.log(add(1, 2));     // 3

function add2(x = 0, y = 0) {
    return x + y;
}
console.log(add2());        // 0
console.log(add2(1));       // 1
console.log(add2(1, 2));    // 3
```

### 원래대로라면 이렇게 처리해야 했을 것
```javascript
function add(x, y) {
    x = x ?? 0;
    y = y ?? 0;
    return x + y;
}
```
