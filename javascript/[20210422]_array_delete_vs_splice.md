# Array elements - delete vs splice()

## delete
```javascript
let array = [1, 2, 3, 4, 5];

delete array[0];
```
### 결과
```javascript
console.log(array.length);      // 5
console.log(array[0]);          // undefined
console.log(array.toString());  // ,2,3,4,5
```

## splice()
```javascript
let array = [1, 2, 3, 4, 5];

array.splice(0, 1);
```

### 결과
```javascript
console.log(array.length);      // 4
console.log(array[0]);          // 2
console.log(array.toString());  // 2,3,4,5
```

## ⭐️ 결론
- `delete` 요소의 속성을 삭제하지만 index, length를 업데이트 하지 않음.
- `splice()` 요소 자체를 삭제하고 다시 indexing, length 조절.
