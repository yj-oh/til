# querySelector
- CSS 선택자를 이용해 요소를 찾는 메소드

## 요소 찾기
- 요소가 가지고 있는 조건에 따라
```javascript
document.getElementById();
document.getElementsByClassName();
document.getElementsByTagName();
document.getElementsByName();
```

## querySelector, querySelectorAll
- 다른 요소와의 관계를 사용하므로 범용적
```javascript
document.querySelector('#p');       // id가 p인 요소
document.querySelector('.p');       // 클래스 이름이 p인 요소
document.querySelectorAll('p');     // p 태그 전체(배열)
```

### 예제
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Test</title>
    <style>
    </style>
</head>
<body>
<div id="wrap">
    <header>Hello, World!</header>
    <div>
        <p class="name">오윤주</p>
        <p class="title">제목 없음</p>
        <input name="age" value="31"/>
    </div>
    <div></div>
</div>
<script type="text/javascript">
    const wrap   = document.querySelector('#wrap');
    const header = document.querySelector('header');
    const div    = document.querySelectorAll('#wrap > div');
    const name   = document.querySelector('.name');
    const input  = document.querySelector('input[name=age]')

    console.log(wrap);
    console.log(header.innerText === 'Hello, World!');  // true
    console.log(div.length === 2);                      // true
    console.log(name.innerHTML === '오윤주');            // true
    console.log(input.getAttribute('value') === '31');  // true
</script>
</body>
</html>
```
