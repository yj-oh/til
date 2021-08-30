# Array fill() method
- 배열 채우기
- 참고 : [Array.prototype.fill() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/fill)

## 👉 문법
```javascript
fill(value)
fill(value, start)
fill(value, start, end)
```

## 👉 설명
- `start`가 음수면, `array.length + start`
- `end`가 음수면, `array.length + end`
- mutator method. 복사본이 아닌, 배열 자체를 변경하고 반환.
- `value`가 객체면 각 요소는 객체의 참조값으로 변경됨.

## 👉 예제
```javascript
[1, 2, 3, 4, 5].fill(3);        // [3, 3, 3, 3, 3]
[1, 2, 3, 4, 5].fill(0, 4);     // [1, 2, 3, 4, 0]
[1, 2, 3, 4, 5].fill(1, 0, 5);  // [1, 1, 1, 1, 1]
[1, 2, 3, 4, 5].fill(-3, -4);   // [1, -3, -3, -3, -3]
```
