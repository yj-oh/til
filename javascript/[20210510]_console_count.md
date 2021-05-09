# console.count()
- console APIs
- 콘솔로 디버깅할 때 호출된 횟수를 출력해준다.

```javascript
console.count([label]);
```

## Examples
```javascript
console.count('call');
console.count('call');
console.count('call');
console.count('call');
```
- Output : 
```text
call: 1
call: 2
call: 3
call: 4
```
