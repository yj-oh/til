# event.target vs event.currentTarget
- `event.currentTarget`은 이벤트가 바인딩된 요소 반환
- `event.target`은 실제 이벤트가 발생하는 요소 반환

## 예제
```html
<button>
    <span>클릭</span>
</button>
```
- 클릭 이벤트를 `<button>`에 걸었다.
```javascript
document.querySelector('button').addEventListener('click', function (e) {
    console.log(e.target);
    console.log(e.currentTarget);
});
```
- 버튼을 클릭하면 `event.target`과 `event.currentTarget`을 각각 console 에 출력한다.

## 결과
![code result](.%5B20210521%5D_event_target_vs_currenttarget_images/3d9008fa.png)
- `event.target`은 `<span>`
- `event.currentTarget`은 `<button>`

## 왜?
>- `event.currentTarget`은 이벤트가 바인딩된 요소 반환
>- `event.target`은 실제 이벤트가 발생하는 요소 반환

- `<button>`에 이벤트를 걸었지만 이벤트 버블링에 의해 `<span>`도 이벤트를 사용할 수 있다.
- 그래서 `<span>`을 클릭했을 때 이벤트가 발동되고
  `event.target`은 `<span>` 본인을,
  `event.currentTarget`은 이벤트가 실제로 바인딩 된 `<button>`을 가리킨다.
