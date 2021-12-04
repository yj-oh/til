# addEventListener()
```text
target.addEventListener(type, listener [, options]);
target.addEventListener(type, listener [, useCapture]);
```
- event type
  - https://developer.mozilla.org/en-US/docs/Web/Events
  - `'click'`, `'keydown'`, `'mouseover'` 등등등
- listener
  - This must be an object implementing the EventListener interface, 
    or a JavaScript function.
- options
```javascript
target.addEventListener(type, listener, {
    capture: false,
    once: false,
    passive: false,
})
```
| options | description              | default |
|---------|--------------------------|---------|
| capture | 캡처링 사용할 것인지              | false   |
| once    | 한 번만 실행할 것인지             | false   |
| passive | preventDefault() 실행할 것인지 | false   |

##### * Reference : https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener
