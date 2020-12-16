# array methods 총 정리 1
- ✍️ 문자열로 출력 `toString()`
- ✍️ 문자열로 출력(with separator) `join()`
- ⛔️ 마지막 element 제거 `pop()`
- ➕ 마지막에 element 추가 `push()`
- ⛔️ 첫번째 element 제거 `shift()`
- ➕ 앞에 element 추가 `unshift()`
- ⛔️ 특정 index의 element 삭제 `delete`
- ➕ 특정 index에 element 추가
- ➕⛔ index로 elements 추가, 삭제 `splice()`
- ➕ Merging Array `concat()`
- ✂️ 특정 index의 elements 잘라내기 `slice()`

---

#### 예제 데이터
```javascript
const log = console.log;

const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];
```

### ✍️ 문자열로 출력 `toString()`
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];

log( arr            );  // (7) ['a', 3, 'b', 2, 'c', 1, 'A']
log( arr.toString() );  // a,3,b,2,c,1,A
```

### ✍️ 문자열로 출력(with separator) `join()`
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];

log( arr.join(' - ') );  // a - 3 - b - 2 - c - 1 - A
```

### ⛔️ 마지막 element 제거 `pop()`
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];

log( arr.pop() );  // A
log( arr       );  // (6) ['a', 3, 'b', 2, 'c', 1]
```

### ➕ 마지막에 element 추가 `push()`
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1];

log( arr.push('A') );  // 7
log( arr           );  // (7) ['a', 3, 'b', 2, 'c', 1, 'A']
```

### ⛔️ 첫번째 element 제거 `shift()`
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];

log( arr.shift() );  // a
log( arr         );  // (6) [3, 'b', 2, 'c', 1, 'A']
```

### ➕ 앞에 element 추가 `unshift()`
```javascript
const arr = [3, 'b', 2, 'c', 1, 'A'];

log( arr.unshift('a') );  // 7
log( arr );  // (7) ['a', 3, 'b', 2, 'c', 1, 'A']
```

### ⛔️ 특정 index의 element 삭제 `delete`
```javascript
const arr = ['a', 3, 'b', 2, 'c', 1, 'A'];

log( delete arr[0] );  // true
log( arr           );  // (7) [empty, 3, 'b', 2, 'c', 1, 'A']
log( arr[0]        );  // undefined
```

### ➕ 특정 index에 element 추가
```javascript
const arr = [empty, 3, 'b', 2, 'c', 1, 'A'];

log( arr[0] = 'a' );  // a
log( arr          );  // (7) ['a', 3, 'b', 2, 'c', 1, 'A']
```

### ➕⛔ index로 elements 추가, 삭제 `splice()`
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

### ➕ Merging Array `concat()`
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

### ✂️ 특정 index의 elements 잘라내기 `slice()`
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
