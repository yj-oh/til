# 모바일에서 탭 하이라이트 제거하기
- 크롬 등 웹킷 기반 브라우저에서 모바일 웹뷰 작업을 했다.
- 탭 메뉴 `<li>`를 클릭하면 아래와 같이 하이라이트가 생긴다.

![](.%5B20210411%5D_css_mobile_tap_highlight_images/18d0dc9f.png)

```css
ul {
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
```
- `-webkit-tap-highlight-color` 속성을 추가하고 컬러값을 지정해준다.
- 물론 없애는 게 목적이므로 opacity 0
