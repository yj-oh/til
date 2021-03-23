# How to get CSS values
1. `{element}.style.{property}`
2. `getComputedStyle({element}).{property}`

## Example code
```css
#element {
    width: 100px;
    font-weight:bold;
}
```
```html
<div id="element" style="background-color: cyan; font-size:1rem"></div>
```

## Getting inline styles
```javascript
const element = querySelector('#element');

const backgroundColor = element.style.backgroundColor;
const fontSize = element.style.fontSize;

console.log(backgroundColor);   // cyan
console.log(fontSize);          // 1rem

// CSS file에 정의한 스타일을 가져오려고 하면?
console.log(element.style.width);       // ''
console.log(element.style.fontWeight);  // ''
```
- 왜 CSS file에 적용한 스타일은 못 가져올까?
- 스타일 객체를 console에 찍어보자.
```javascript
console.log(element.style);
```
- 쭉 내려 보면,

![](.%5B20210323%5D_get_css_values_images/a34fc97d.png)

- inline으로 정의한 `font-size`는 값이 있지만 CSS file에 정의한 `font-weight`는 값이 없다.
- node 자체에 스타일 속성이 있고, 그 값은 node가 가진 스타일 객체에 정의되어 있다.

## Getting computed styles
```javascript
const element = querySelector('#element');
const style = getComputedStyle(element);

const backgroundColor = style.backgroundColor;
const fontSize = element.style.fontSize;

console.log(backgroundColor);   // rgb(0, 255, 255)
console.log(fontSize);          // 16px
```
- 왜 `1rem`이 아니라 `16px`?
  - 개발자가 정의한 스타일 값이 아닌, 그 결과물로 최종 적용된 CSS 데이터를 가져오기 때문.
    
## 언제 무엇을 쓸까?
- `element.style` 스타일 변경 가능
  ```javascript
  element.style.fontSize = '2rem';
  ```
- `getComputedStyle()` 읽기 전용으로, 속성값 확인만 가능
  ```javascript
  getComputedStyle(element).fontSize = '2rem';
  ```
  - 위와 같이 변경을 시도하면 브라우저 콘솔에 에러 뜸
  ```text
  🚨 Uncaught DOMException: Failed to set the 'font-size' property on 
  'CSSStyleDeclaration': These styles are computed, and therefore 
  the 'font-size' property is read-only.
  ```

## 전체 코드
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>EXAMPLE</title>
    <style>
        #element {
            width: 100px;
            font-weight:bold;
        }
    </style>
</head>
<body>
<div id="element" style="background-color: cyan; font-size:1rem"></div>

<script type="text/javascript">
    const log = console.log;
    const element = document.querySelector('#element');

    // inline styles
    log(element.style.backgroundColor);             // cyan
    log(getComputedStyle(element).backgroundColor); // rgb(0, 255, 255)

    log(element.style.fontSize);                    // 1rem
    log(getComputedStyle(element).fontSize);        // 16px
    

    // css file
    log(element.style.width);                       // ''
    log(getComputedStyle(element).width);           // 100px

    log(element.style.fontWeight);                  // ''
    log(getComputedStyle(element).fontWeight);      // 700

    
    log(element.style);

    getComputedStyle(element).fontSize = '2rem';
</script>
</body>
</html>
```
