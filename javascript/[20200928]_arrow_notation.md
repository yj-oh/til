# 화살표 표기법
- 익명

## 단축 문법
- `function` 생략 가능
- parameter가 하나면 `괄호` 생략 가능
- body가 표현식 하나면 `중괄호`, `return문` 생략 가능

## 예제
```javascript
const f = function() { return "Hello, World!"; }

const f = () => "Hello, World!";
```
```javascript
const f = function(name) { return `Hello, ${name}!`; }

const f = name => `Hello, ${name}!`;
```
```javascript
const f = function(a, b) { return a + b; }

const f = (a, b) => a + b;
```

##### * Reference : ⌜Learning JavaScript⌟ - Ethan Brown
