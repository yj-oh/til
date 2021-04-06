# box-sizing
- 요소의 너비와 높이 계산
- `content-box` : 콘텐츠 영역의 너비와 높이만 계산. padding, border는 따로 계산.
- `border-box` : 콘텐츠 영역 + padding + border

## 코드
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>EXAMPLE</title>
    <style>
        div {
            margin:10px;
            width:100px;
            height:100px;
            background-color:crimson;
            border:solid 10px black;
        }

        #content-box    { box-sizing:content-box; }
        #border-box     { box-sizing:border-box; }
    </style>
</head>
<body>
    <div id="content-box"></div>
    <div id="border-box"></div>
</body>
</html>
```

## 결과
![](.%5B20210406%5D_box_sizing_images/53681527.png)

- 똑같이 `width: 10px`이지만
  - `content-box`는 콘텐츠 영역만 100px + border 10px씩 양쪽 총 20px = 120px
  - `border-box`는 전체가 100px
    
- 만약 padding 20px을 추가하면?
    - `content-box`는 콘텐츠 영역만 100px + border 20px, margin 40xp = 총 160px
    - `border-box`는 전체가 100px

![](.%5B20210406%5D_box_sizing_images/a887a4ae.png)

## 결론
- `box-sizing: border-box`는 border와 padding을 따로 계산할 필요 없이
  그 자체의 사이즈만 논하므로 더 명확하다고 느낌.
- 많이 사용하고 선호하는 데에는 다 이유가 있다.
