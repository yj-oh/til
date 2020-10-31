# Optional chaining (?.)
- 프로퍼티가 없는 중첩 객체에 에러 없이 안전하게 접근
- 대상이 undefined나 null이면 `undefined` 반환
- 남용하지 말 것
   - 반드시 있어야 하는 값에 값이 없을 경우, 에러를 통해 바로 발견해야 하는데
     에러를 감추므로 디버깅이 어려울 수 있다.

### 예제
```javascript
const fish = null;

//console.log(fish.type);        // Cannot read property 'type' of null
console.log(fish && fish.type);  // null
console.log(fish?.type);         // undefined
```

##### * References
- https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Optional_chaining
- https://ko.javascript.info/optional-chaining
