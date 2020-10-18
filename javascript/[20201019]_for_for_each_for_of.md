# for, forEach, for ...of

## 이 배열 내부의 요소들을 순차적으로 출력해보자.
```javascript
const arr = ['a', 'b', 'c'];
```

### 👉 for
- 일반적인 반복문
- break를 사용할 수 있음
- index를 사용할 수 있음
```javascript
for(let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
    if(arr[i] === 'b') break;
}
```
```text
// 출력 결과
a
b
```

### 👉 forEach
- Array 객체에서 사용 가능
- ES6부터는 Map, Set 지원
- break를 사용할 수 없음
- index를 사용할 수 없음
```javascript
arr.forEach(alphabet => {
    console.log(alphabet);
    //if(alphabet === 'b') break;
});
```
```text
// 출력 결과
a
b
c
```

### 👉 for ...of
- ES6에서 추가됨
- 컬렉션 요소에 루프를 실행할 수 있음
- 배열은 물론 iterable 객체에 모두 사용 가능
```javascript
for(let alphabet of arr) {
    console.log(alphabet);
}
```

## 💡 iterator에 사용해보기

```javascript
// 위의 arr 배열을 사용하여 iterator 생성
const it = arr.values();
```

### 👉 forEach
```javascript
it.forEach(alphabet => {
    console.log(alphabet);
});
```
- 결과는?
   - ❌ error : Uncaught TypeError: it.forEach is not a function

### 👉 for ...of
```javascript
for(let alphabet of it) {
    console.log(alphabet);
}
```
```text
// 출력 결과
a
b
```
