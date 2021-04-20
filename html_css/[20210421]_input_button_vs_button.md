# input type="button" vs button
```html
<input type="button" value="안녕"/>
<button type="button">안녕</button>
```
- 둘은 생긴 것도 비슷하고 동작도 같다.
- 무슨 차이가 있을까?

```html
<button type="button">
    <img src="https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png" alt="google logo"/>
</button>
```
- \<button>은 스스로 닫지 않는 태그다.
  - == 각종 하위 태그를 포함할 수 있다.
  - == 다양한 스타일을 입힐 수 있고, 내부에 텍스트뿐만 아니라 이미지도 넣을 수 있다.
  - == 디자인적 관점에서 매우 자유롭다.
- \<input type="button">은 스스로 닫는 태그다
  - == 하위 태그를 포함할 수 없다.
  - == 스타일, 내부 컨텐츠 등을 태그 내에서 해결해야 한다.
  - == 제한이 있다.
