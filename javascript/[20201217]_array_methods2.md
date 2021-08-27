# array methods 총 정리 2
#### [array methods 총 정리 1]([20201216]_array_methods.md)
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
- ➕ 배열 안에서 element 교체 `copyWhithin()`
    
#### array methods 총 정리 2
>- ❓ 특정 문자열 포함 여부 `includes()`
>- ❓ 특정 조건 충족 여부 (일부라도) `some()`
>- ❓ 특정 조건 충족 여부 (전체) `every()`
>- ➕ callbackFunction의 결과로 새로운 배열 반환 `map()`
>- 🔎 특정 값 찾기 (첫 번째 반환) `find()`
>- 🔎 특정 값 찾기 (전체 반환) `filter()`

---

#### 예제 데이터
```javascript
const log = console.log;

const animals = [
    {
    	id: 1,
    	name: '오춘복',
    	type: 'hamster',
    	like: ['사료', '분홍 수면양말']
    },
    {
    	id: 2,
    	name: '오춘식',
    	type: 'hamster',
    	like: ['사료', '배칩', '브로콜리', '안경닦이']
    },
    {
    	id: 3,
    	name: '앵',
    	type: 'blood parrot cichlid',
    	like: ['사료', '집']
    },
    {
    	id: 4,
    	name: '충',
    	type: 'blood parrot cichlid',
    	like: ['돌', '모래', '사료']
    },
    {
    	id: 5,
    	name: '블루',
    	type: 'cichlid',
    	like: ['막렝이', '집', '사료']
    },
    {
    	id: 6,
    	name: '막렝이',
    	type: 'yellow cichlid',
    	like: ['사료']
    }
];
```

### ❓ 특정 문자열 포함 여부 `includes()`
- string.includes(search_string, index)
    - search_string : 찾고자 하는 문자열
    - index : 검색 시작 인덱스
- 대소문자 구분

### ❓ 특정 조건 충족 여부 (일부라도) `some()`
- 배열의 요소 중 하나라도 포함되면 true
```javascript
log( animals.some((animal) => animal.like.includes('집')) );    // true
log( animals.some((animal) => animal.like.includes('엽떡')) );  // false
```

### ❓ 특정 조건 충족 여부 (전체) `every()`
- 배열의 요소 전체가 포함되면 true
```javascript
log( animals.every((animal) => animal.like.includes('사료')) );  // true
log( animals.every((animal) => animal.like.includes('배칩')) );  // false
```

### ➕ callbackFunction의 결과로 새로운 배열 반환 `map()`
```javascript
log( animals.map((animal) => animal.name) );
// ["오춘복", "오춘식", "앵", "충", "블루", "막렝이"]
```

### 🔎 특정 값 찾기 (첫 번째 반환) `find()`
- 첫 번째 값만 반환
- 없으면 `undefined`
```javascript
log( animals.find((animal) => animal.name === '오춘식') );  
// {id: 2, name: "오춘식", type: "hamster", like: Array(3)}
```

### 🔎 특정 값 찾기 (전체 반환) `filter()`
- 검색 결과가 여러 건일 경우 배열 형태로 반환
```javascript
log( animals.filter((animal) => animal.like.includes('집')) );
// (2) [{...}, {...}]
//      0: {id: 3, name: "앵", type: "blood parrot cichlid", age: 3, like: Array(2)}
//      1: {id: 5, name: "블루", type: "cichlid", age: 2, like: Array(3)}
```
