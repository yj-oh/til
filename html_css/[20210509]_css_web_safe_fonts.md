# CSS Web Safe Fonts

## 🤔 상황
- `font-family`에 특정 폰트를 기재하지 않으면 WebStorm 이 경고 메시지를 띄운다.

![](.%5B20210509%5D_css_web_safe_fonts_images/a1677ca5.png)

## 💡 해결
- 특정 폰트라 함은 CSS Web Safe Fonts 를 말한다.
```text
Note
Before you publish your website, always check how your fonts appear on 
different browsers and devices, and always use fallback fonts!
```
### 폰트 목록
>- Arial (sans-serif)
>- Verdana (sans-serif)
>- Helvetica (sans-serif)
>- Tahoma (sans-serif)
>- Trebuchet MS (sans-serif)
>- Times New Roman (serif)
>- Georgia (serif)
>- Garamond (serif)
>- Courier New (monospace)
>- Brush Script MT (cursive)
>* _참고 : https://www.w3schools.com/cssref/css_websafe_fonts.asp_

- 위의 WebStorm 팝업에서 `Insert generic font name`를 누르면 몇 가지 선택지가 있음.
  - serif
  - sans-serif
  - cursive
  - fantasy
  - monospace
- cursive, fantasy 는 가독성이 좋지 않아 비추.
- monospace 는 코딩 폰트로도 많이 쓰인다.
- 보통 `serif`나 `sans-serif`로 설정하는 듯.

## 👉 serif vs sans-serif
![](.%5B20210509%5D_css_web_safe_fonts_images/35a877e7.png)
- 이미지 출처 : https://www.maconprinting.com/content/serif-versus-san-serif-fonts
