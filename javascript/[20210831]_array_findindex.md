# Array findIndex() method - 조건을 만족하는 요소의 인덱스 반환
- 조건을 만족하는 요소의 index 를 반환하는 함수.
- 검색을 위해 각 요소에 대해 `callbackFn`를 실행한다.
- 참고 : [Array.prototype.findIndex() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)
- `TIL` \[20210120\] : [Array 내부 객체 중복값 제거]([20210120]_array_내부객체_중복값_제거.md)
  - 위 예제에 `findIndex()`가 나온다.

## 👉 문법
```javascript
// Arrow function
findIndex((element) => { ... } )
findIndex((element, index) => { ... } )
findIndex((element, index, array) => { ... } )

// Callback function
findIndex(callbackFn)
findIndex(callbackFn, thisArg)

// Inline callback function
findIndex(function callbackFn(element) { ... })
findIndex(function callbackFn(element, index) { ... })
findIndex(function callbackFn(element, index, array){ ... })
findIndex(function callbackFn(element, index, array) { ... }, thisArg)
```

### callbackFn
- 조건을 만족하는 요소를 찾을 때까지 배열의 각 값에 대해 실행할 함수

argument | description | optional
--- | --- | ---
`element` | 처리 중인 요소 | 
`index` | 처리 중인 요소의 index | O
`array` | - | O

### thisArg
- Optional
- `callbackFn` 실행할 때 `this`로 사용할 optional object

## 👉 반환값
- 조건에 해당하는 첫번째 요소의 index
- 조건에 해당하는 요소가 없으면 -1

## 👉 예제
- 소수를 찾는다.
```javascript
function isPrime(num) {
  for (let i = 2; num > i; i++) {
    if (num % i == 0) {
      return false;
    }
  }
  return num > 1;
}

console.log([4, 6, 8, 9, 12].findIndex(isPrime));  // -1, not found
console.log([4, 6, 7, 9, 12].findIndex(isPrime));  // 2 (array[2] is 7)
```
- "blueberries" 찾는다.
```javascript
const fruits = ["apple", "banana", "cantaloupe", "blueberries", "grapefruit"];

const index = fruits.findIndex(fruit => fruit === "blueberries");

console.log(index);          // 3
console.log(fruits[index]);  // blueberries
```
- 중복되지 않은 값을 찾는다.
```javascript
const uniqueArr = arr.filter((item, i) => {
    return arr.findIndex((item2) => {
        return item.id === item2.id && item.name === item2.name;
    }) === i;
});
// 0: {id: 1, name: "춘식"}
// 1: {id: 2, name: "춘복"}
// 2: {id: 3, name: "앵"}
// 3: {id: 4, name: "충"}
// 4: {id: 1, name: "블루"}
```
