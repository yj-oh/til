# generator
- iterator를 이용해 자신의 실행을 제어
   - 참고 : [iterator]([20200929]_iterator.md)

## 일반 함수와의 차이
- 언제든 호출자에게 제어권을 넘길 수 있다
- 호출한 즉시 실행되는 게 아니라 iterator를 반환하고 next() 호출함에 따라 실행

## 특징적인 문법
- function 키워드 뒤에 `*`
- return 외에 `yield` 키워드 사용 가능
- 화살표 표기법 사용 불가능

### 예제
```javascript
function* alphabet() {
    yield 'a';
    yield 'b';
    yield 'c';
    yield 'd';
    yield 'e';
}
const it = alphabet();

console.log(it.next());  // {value: "a", done: false}
console.log(it.next());  // {value: "b", done: false}
console.log(it.next());  // {value: "c", done: false}
console.log(it.next());  // {value: "d", done: false}
console.log(it.next());  // {value: "e", done: false}

console.log("계속 호출하면?");
console.log(it.next());  // {value: "undefined", done: true}
```

### 예제 2 - iterator를 이용해 자신의 실행을 제어?
```javascript
function* userInfo() {
    let name = yield "이름은 무엇입니까?";
    let age = yield "나이는 몇 살입니까?";
    let job = yield "무슨 일을 합니까?";
    return `${name}는 ${age}살이고 ${job}다.`;
}
const it = userInfo();
console.log(it.next());
console.log(it.next("오윤주"));
console.log(it.next("31"));
console.log(it.next("간발자"));
console.log(it.next());
```

### 결과
![](.%5B20200930%5D_generator_images/4e529dea.png)

##### * Reference : ⌜Learning JavaScript⌟ - Ethan Brown (265 ~ 269p)
