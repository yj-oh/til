# @keyframes
- 애니메이션 코드를 정의
```css
@keyframes animationname {keyframes-selector {css-styles;}}
```

Value | Description
--- | ---
animationname | 애니메이션 이름
keyframes-selector | `0%` ~ `100%` 또는 `from` ~ `to`
css-styles | 적용할 스타일 속성

- 이렇게 정의한 `@keyframes`는 `animation`, 또는 `animation-name`에 그 이름을 넣어 사용
  - 💡 참고 : [CSS Animation]([20210315]_css_animation.md)
- 최상의 브라우저 지원을 위해 항상 0%, 100%를 모두 정의해야 함.
- `@keyframes` 내부의 `!important`는 무시됨.

## 예제
- 0.1초 간격으로 좌우로 흔들리는 초록 정사각형
```css
@keyframes rotate {
    0%      { transform:rotate(5deg); }
    100%    { transform:rotate(-5deg); }
}
#square {
    width: 100px;
    height: 100px;
    background-color: green;
    animation: rotate 0.1s alternate infinite;
}
```

##### * Reference : https://www.w3schools.com/cssref/css3_pr_animation-keyframes.asp
