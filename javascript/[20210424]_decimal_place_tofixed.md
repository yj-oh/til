# 자릿수 보정 - toFixed()
- 반올림은 전에 알아봤었다.
  - [[20210302] Math Methods]([20210302]_math_methods.md)
```javascript
let num = 3.14159265359;

console.log(Math.round(num));
```

## 자릿수 보정은 어떻게 할까?
- toFixed()

```javascript
let num = 3.14159265359;

console.log(num.toFixed(1));    // 3.1
console.log(num.toFixed(2));    // 3.14
console.log(num.toFixed(3));    // 3.142
```

## 주의
- toFixed()는 반올림된다.
- return 값이 string
```javascript
console.log(typeof num.toFixed(3));  // string
```
