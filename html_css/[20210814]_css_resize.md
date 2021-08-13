# CSS resize
- CSS3
- 다음에는 적용되지 않음.
  - display: inline;
  - overflow: visible;

```css
div {
    resize: both;
    overflow: auto;
}
```
![](.%5B20210814%5D_css_resize_images/5dc36f69.png)

```css
div {
    resize: vertical;
    overflow: auto;
}
```
![](.%5B20210814%5D_css_resize_images/26d49780.png)

## Property Values
Value | Description
--- | ---
none | default. 크기 조절 불가
both | width & height 모두 조절
horizontal | width 조절
vertical | height 조절
initial | 기본값으로 설정
inherit | 부모 속성을 상속

##### * References
- https://developer.mozilla.org/en-US/docs/Web/CSS/resize
- https://www.w3schools.com/cssref/css3_pr_resize.asp
