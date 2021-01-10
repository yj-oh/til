# Spread syntax (...)

## 배열 캡쳐
```javascript
const log = console.log;

const arr = [1, 2, 3];
let arr2 = [...arr];
log(arr2);      // [1, 2, 3]
arr2.push(4);
log(arr2);      // [1, 2, 3, 4]
log(arr);       // [1, 2, 3]
// arr은 바뀌지 않음
```

## 배열 합치기
```javascript
arr2 = [...arr, ...arr2];
log(arr2);  // [1, 2, 3, 1, 2, 3, 4]
```

## rest
```javascript
const [num, ...rest] = arr;
log(rest);  // [2, 3]
```
```javascript
const family = {
    hamster: '춘식',
    fish: '앵',
    sunflower: '냉동',
}
const { sunflower, ...animals } = family;
log(animals);
// {hamster: "춘식", fish: "앵"}
```
