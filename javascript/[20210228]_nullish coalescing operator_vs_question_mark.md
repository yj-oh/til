# ? vs ??

- `value`라는 변수가 있고, 이 변수에는 empty string `''`이 담길 수 있다.
- 해당 변수 값을 체크해서 값이 있으면 보여주고 아니면 `'null'`을 출력한다.

```javascript
const value = '';

console.log(value ? value : 'null');    // null
console.log(value ?? 'null');           // 
```

- 처음에 `value ?? 'null'`의 결과는 당연히 `'null'`일 줄 알았는데 value값(`''`)이
  찍히기에 뭐지 했다.
- 다시 되새김질.

### `??`는 null 또는 undefined인 값을 특정값으로 처리한다.
  - _참고 : [Nullish coalescing operator]([20201209]_nullish_coalescing_operator.md)_
