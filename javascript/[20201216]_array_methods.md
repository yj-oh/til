# array methods 총 정리 1
type | function | method | 수정 또는 사본
--- | --- | --- | ---
✍️ | 문자열로 출력 | [toString()](#tostring) | -
✍️ | 문자열로 출력(with separator) | [join()](#join) | -
⛔️ | 마지막 element 제거 | [pop()](#pop) | 수정
➕ | 마지막에 element 추가 | [push()](#push) | 수정
⛔️ | 첫번째 element 제거 | [shift()](#shift) | 수정
➕ | 앞에 element 추가 | [unshift()](#unshift) | 수정
⛔️ | 특정 index의 element 삭제 | [delete](#delete) | 수정
➕ | 특정 index에 element 추가 | [element 추가](#Add-element) | 수정
➕⛔ | index로 elements 추가, 삭제 | [splice()](#splice) | 수정
➕ | Merging Array | [concat()](#concat) | 사본
✂️ | 특정 index의 elements 잘라내기 | [slice()](#slice) | 사본
🔀 | 배열 안에서 element 교체 | [copyWithin()](#copywithin) | 수정
➕ | 배열 채우기 | [fill()](#fill) | 수정

---

#### 예제 데이터
```javascript
const log = console.log;

const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];
```

## toString()
- ✍️ 문자열로 출력
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];

log( arr            );  // (7) ['a', 3, 'b', 2, 'c', 1, 'A']
log( arr.toString() );  // a,3,b,2,c,1,A
```

## join()
- ✍️ 문자열로 출력(with separator)
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];

log( arr.join(' - ') );  // a - 3 - b - 2 - c - 1 - A
```

## pop()
- ⛔️ 마지막 element 제거
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];

log( arr.pop() );  // A
log( arr       );  // (6) ['a', 3, 'b', 2, 'c', 1]
```

## push()
- ➕ 마지막에 element 추가
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1];

log( arr.push('A') );  // 7
log( arr           );  // (7) ['a', 3, 'b', 2, 'c', 1, 'A']
```

## shift()
- ⛔️ 첫번째 element 제거
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];

log( arr.shift() );  // a
log( arr         );  // (6) [3, 'b', 2, 'c', 1, 'A']
```

## unshift()
- ➕ 앞에 element 추가
```javascript
const arr = [3, 'b', 2, 'c', 1, 'A'];

log( arr.unshift('a') );  // 7
log( arr );  // (7) ['a', 3, 'b', 2, 'c', 1, 'A']
```

## delete
- ⛔️ 특정 index의 element 삭제
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];

log( delete arr[0] );  // true
log( arr           );  // (7) [empty, 3, 'b', 2, 'c', 1, 'A']
log( arr[0]        );  // undefined
```

## Add element
- ➕ 특정 index에 element 추가
```javascript
const arr = [empty, 3, 'b', 2, 'c', 1, 'A'];

log( arr[0] = 'a' );  // a
log( arr          );  // (7) ['a', 3, 'b', 2, 'c', 1, 'A']
```

## splice()
- ➕⛔ index로 elements 추가, 삭제
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];

// index 2부터 2개 지우고 elements 추가
log( arr.splice(2, 2, 'new b', 'new 2') );  // (2) ['b', 2]
log( arr );  // (7) ['a', 3, 'new b', 'new 2', 'c', 1, 'A']

// index 2부터 2개 지움
log( arr.splice(2, 2) );  // (2) ['new b', 'new 2']
log( arr              );  // (5) ['a', 3, 'c', 1, 'A']

// index 2부터 0개 지우고 elements 추가
log( arr.splice(2, 0, 'b', '2') );  // []
log( arr                        );  // (7) ['a', 3, 'b', '2', 'c', 1, 'A']

// index 1부터 전부 삭제
log( arr.splice(1) );  // (6) [3, 'b', 2, 'c', 1, 'A']
log(arr            );  // ['a']
```

## concat()
- ➕ Merging Array
- 기존 array를 변경하지 않고 새 array를 반환한다.
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];
const arr2 = ['new a', 'new 3'];
const arr3 = ['new c', 'new 1'];

log( arr.concat(arr2, arr3) );  // (11) ['a', 3, 'b', '2', 'c', 1, 'A', 'new a', 'new 3', 'new c', 'new 1']
log( arr );  // (7) ['a', 3, 'b', '2', 'c', 1, 'A']

log( arr.concat('new A') );  // (8) ['a', 3, 'b', '2', 'c', 1, 'A', 'new A']
log( arr );  // (7) ['a', 3, 'b', '2', 'c', 1, 'A']
```

## slice()
- ✂️ 특정 index의 elements 잘라내기
- 기존 array를 변경하지 않고 새 array를 반환한다.
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];

// 앞에서부터 1개 잘라냄
log( arr.slice(1) );  // (6) [3, 'b', '2', 'c', 1, 'A']
log( arr          );  // (7) ['a', 3, 'b', '2', 'c', 1, 'A']

// index 2부터 3 전까지 잘라냄
log( arr.slice(2, 3) );  // ['b']
log( arr             );  // (7) ['a', 3, 'b', '2', 'c', 1, 'A']
```

## copyWithin()
- 🔀 배열 안에서 element 교체
- [Array copyWithin() method]([20210828]_array_copywithin.md)
```javascript
copyWithin(target)
copyWithin(target, start)
copyWithin(target, start, end)
```
```javascript
[1, 2, 3, 4, 5].copyWithin(3);          // [1, 2, 3, 1, 2]
[1, 2, 3, 4, 5].copyWithin(0, 4);       // [5, 2, 3, 4, 5]
[1, 2, 3, 4, 5].copyWithin(1, 0, 5);    // [1, 1, 2, 3, 4]
[1, 2, 3, 4, 5].copyWithin(-3, -4);     // [1, 2, 2, 3, 4]
[1, 2, 3, 4, 5].copyWithin(-3, 0, -4);  // [1, 2, 1, 4, 5]
```

## fill()
- ➕ 배열 채우기
- [Array fill() method]([20210829]_array_fill.md)
```javascript
fill(value)
fill(value, start)
fill(value, start, end)
```
```javascript
[1, 2, 3, 4, 5].fill(3);        // [3, 3, 3, 3, 3]
[1, 2, 3, 4, 5].fill(0, 4);     // [1, 2, 3, 4, 0]
[1, 2, 3, 4, 5].fill(1, 0, 5);  // [1, 1, 1, 1, 1]
[1, 2, 3, 4, 5].fill(-3, -4);   // [1, -3, -3, -3, -3]
```
