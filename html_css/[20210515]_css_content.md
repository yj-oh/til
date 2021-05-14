# CSS content

## 텍스트
```html
<div id='container'>
    <p class='hello'>반가워. </p>
</div>
```
```css
p:before {
	content:'안녕, ';
}
p:after {
    content:'CSS!';
}
```
- 결과
```text
안녕, 반가워. CSS!
```

## 이미지
```css
p:after {
    content:url('{주소}');
}
```

## 속성값
```css
p:after {
    content:attr(class);
}
```
- 결과
```text
hello
```

- https://developer.mozilla.org/en-US/docs/Web/CSS/content
