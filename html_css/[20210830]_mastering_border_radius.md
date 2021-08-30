# border-radius 정복하기 (feat.FANCY-BORDER-RADIUS)
- CSS 쪼물락 거리다가 `Fancy border radius generator`라는 사이트 발견.
- https://9elements.github.io/fancy-border-radius/

![Fancy border radius generator](.%5b20210830%5d_fancy_border_radius_generator/0fe78c15.png)

- GitHub : https://github.com/9elements/fancy-border-radius
- 보통 `border-radius: 10px`처럼 사용했는데 값 8개가 들어가는 게 신기해서 사이트에 기재되어있는 
  [Read the Story](https://9elements.com/blog/css-border-radius/) 를 읽어봤다.
- 신기방기...
- 아래는 사이트에 내용을 간단하게 필요한 부분만 번역, 의역한 것.

---

# 😎 Mastering border-radius
## 👉 단일값
![Single value](.%5b20210830%5d_fancy_border_radius_generator/60b3d323.png)
- 보통 `border-radius: 1em` 이렇게 단일값으로 사용.
- 백분율을 사용할 수도 있음.
  - 50% 로 설정해서 원을 만드는 데에 주로 사용.
  - 해당 요소의 width, height 를 기반으로 함. 그래서 직사각형에 사용하면 대칭되는 모서리 X
  - ![rectangle](.%5b20210830%5d_fancy_border_radius_generator/80ed290a.png)

## 👉 4개의 값
- 둘 이상의 값은 왼쪽 상단 모서리에서 시작해서 시계 방향으로 이동하며 각 모서리의 값 설정.
- 백분율을 사용할 수도 있고 백분율과 고정값을 함께 사용할 수도 있음.
- ![Four different values](.%5b20210830%5d_fancy_border_radius_generator/5d292550.png)

## 👉 슬래시로 구분된 8개의 값
- [W3C](https://www.w3.org/TR/css-backgrounds-3/#border-radius)
```text
“If values are given before and after the slash, then the values before 
the slash set the horizontal radius and the values after the slash set 
the vertical radius. If there is no slash, then the values set both radii equally.”
```
- 슬래시 앞의 값은 horizontal radius, 뒤의 값은 vertical radius
- 슬래시가 없으면 반지름을 균등하게.
- ![Values separated by a slash](.%5b20210830%5d_fancy_border_radius_generator/6d055581.png)
- 솔직히 모양 이상함. `border-radius: 50%`를 생각해보자.
  - 한 모서리의 두 값을 합하면 100%. 그리고 직선이 남아있지 않음.
  - 8개의 값에 동일한 논리를 적용하면 plectrum, organic cell 같은 모양을 만들 수 있다.
- ![Eight values](.%5b20210830%5d_fancy_border_radius_generator/7a852461.png)
- ![Four overlapping ellipses](.%5b20210830%5d_fancy_border_radius_generator/f7ff81ef.png)
- 결국 최종 모양은 겹쳐진 4개의 원이 만든다.
