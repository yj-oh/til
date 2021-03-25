# KeyboardEvent.keyCode - `Deprecated`!

```javascript
document.addEventListener('keydown', function (e) {
    console.log(e.keyCode);
}, false);
```
- IDE로 코드 작성하는데 `keyCode`에 삭선이 가길래 확인.

```text
Deprecated
This feature is no longer recommended. Though some browsers might still support it, 
it may have already been removed from the relevant web standards, may be 
in the process of being dropped, or may only be kept for compatibility purposes. 
Avoid using it, and update existing code if possible; 
see the compatibility table at the bottom of this page to guide your decision. 
Be aware that this feature may cease to work at any time.
```
- https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/keyCode
- == 권장되지 않음. 웹 표준에서 이미 제거되었거나 drop 하는 중이거나 
  호환성 목적으로만 유지 중일 수 있음. 사용하지 말고 기존 코드 업데이트 해라.

## KeyboardEvent.key
- https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key

## 예제
```javascript
document.addEventListener('keydown', function (e) {
    console.log('keyCode : ' + e.keyCode);
    console.log('key : ' + e.key);
}, false);
```

## 결과
```text
keyCode : 13
key : Enter

keyCode : 27
key : Escape

keyCode : 8
key : Backspace

keyCode : 65
key : a

keyCode : 32
key :  
```

- 마지막은 SpaceBar인데 `e.key`에 아무것도 안 찍히네?
- 확인해보니 `' '`다.
```javascript
document.addEventListener('keydown', function (e) {
    console.log(e.key === ' ');  // true
}, false);
```
