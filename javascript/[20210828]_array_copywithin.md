# Array copyWithin() method
- 배열 안에서 요소를 교체
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin

## 👉 문법
```javascript
copyWithin(target)
copyWithin(target, start)
copyWithin(target, start, end)
```
### target
- 요소를 복사할 인덱스

### start
- 요소 복사를 시작할 인덱스

### end
- 요소 복사를 중지할 인덱스 (기본값 : array.length)
- 만약 start 를 `0`, end 를 `3`으로 지정하면 index 0, 1, 2 가 복사된다.

## 👉 예제
```javascript
[1, 2, 3, 4, 5].copyWithin(3);          // [1, 2, 3, 1, 2]
[1, 2, 3, 4, 5].copyWithin(0, 4);       // [5, 2, 3, 4, 5]
[1, 2, 3, 4, 5].copyWithin(1, 0, 5);    // [1, 1, 2, 3, 4]
[1, 2, 3, 4, 5].copyWithin(-3, -4);     // [1, 2, 2, 3, 4]
[1, 2, 3, 4, 5].copyWithin(-3, 0, -4);  // [1, 2, 1, 4, 5]
```
