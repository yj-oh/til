# CSS white-space
- 공백문자에 대한 처리

## 👉 동작
| 속성           | 개행 문자 | space, tab | 자동줄바꿈 | 줄 끝 공백 |
|--------------|-------|------------|-------|--------|
| normal       | 병합    | 병합         | Y     | 제거     |
| nowrap       | 병합    | 병합         | N     | 제거     |
| pre          | 유지    | 유지         | N     | 유지     |
| pre-wrap     | 유지    | 유지         | Y     | 넘침     |
| pre-line     | 유지    | 병합         | Y     | 제거     |
| break-spaces | 유지    | 유지         | Y     | 줄바꿈    |

## 👉 예제 코드
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>EXAMPLE</title>
    <style>
    	#normal         { white-space:normal; }
    	#nowrap         { white-space:nowrap; }
    	#pre            { white-space:pre; }
    	#pre-wrap       { white-space:pre-wrap; }
    	#pre-line       { white-space:pre-line; }
    	#break-spaces   { white-space:break-spaces; }
    </style>
</head>
<body>
    <div id="normal">
        <h4>normal</h4>
        <p>         안녕        하세요. 좋은 날씨입니다.</p>
    </div>
    
    <div id="nowrap">
        <h4>nowrap</h4>
        <p>         안녕        하세요. 좋은 날씨입니다.</p>
    </div>

    <div id="pre">
        <h4>pre</h4>
        <p>         안녕        하세요. 좋은 날씨입니다.</p>
    </div>
    
    <div id="pre-wrap">
        <h4>pre-wrap</h4>
        <p>         안녕        하세요. 좋은 날씨입니다.</p>
    </div>
    
    <div id="pre-line">
        <h4>pre-line</h4>
        <p>         안녕        하세요. 좋은 날씨입니다.</p>
    </div>

    <div id="break-spaces">
        <h4>break-spaces</h4>
        <p>         안녕        하세요. 좋은 날씨입니다.</p>
    </div>
</body>
</html>
```

## 👉 결과
![](.%5B20210331%5D_css_white_space_images/32208363.png)

- `normal` 연속 공백을 하나로 합침. 자동 줄바꿈.
- `nowrap` 연속 공백을 하나로 합침. 자동 줄바꿈 X.
- `pre` 연속 공백 유지. 자동 줄바꿈 X.
- `pre-wrap` 연속 공백 유지. 자동 줄바꿈.
- `pre-line` 연속 공백을 하나로 합침. 자동 줄바꿈.
- `break-spaces` 연속 공백 유지. 자동 줄바꿈. (아래의 차이점을 제외하고 `pre-wrap`과 동일)
  - 줄 끝 연속 공백 유지
  - 연속 공백의 중간에서도 자동 줄바꿈.
  - 유지한 연속 공백은 요소 바깥으로 넘치지 않고 공간을 차지하므로 
    박스의 본질 크기(min-content, max-content)에 영향

##### * Reference : https://developer.mozilla.org/ko/docs/Web/CSS/white-space
