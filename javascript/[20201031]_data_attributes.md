# data attributes
- `data-*`
- 정해진 속성 이외에, 속성을 추가하여 사용할 수 있음

```html
<label>
    <input id="hamster" data-value="cute" value="2"/>오춘식
</label>
```

```javascript
const dataValue = document.querySelector("#hamster").dataset.value;

console.log(dataValue);  // cute
```

### dataset은 어떤 모습?
```html
<div id="test" 
    data-id="id" 
    data-value="value"
    data-name="name"
    data-type="type"
>
    Test
</div>
```
```text
// browser console
DOMStringMap {id: "id", value: "value", name: "name", type: "type"}
    id: "id"
    name: "name"
    type: "type"
    value: "value"
    __proto__: DOMStringMap
```
