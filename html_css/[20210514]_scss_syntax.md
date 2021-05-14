# SCSS 문법

### 목차
- [주석](#주석)
- [중첩](#중첩)
- [중첩된 속성](#중첩된-속성)
- [상위 선택자](#상위-선택자)
- [중첩을 벗어나 root 에 적용 : `@at-root`](#중첩을-벗어나-root-에-적용)
- [변수](#변수)
  - [전역 변수](#전역-변수)
  - [초깃값](#초깃값)
- [파일 분할](#파일-분할)
- [조건문, 논리](#조건문,-논리)
- [재사용 그룹](#재사용-그룹)
  - [매개변수](#매개변수)
- [함수](#함수)
- [반복문 for](#반복문-for)
- [반복문 each](#반복문-each)
- [반복문 while](#반복문-while)

---

## 주석
```scss
// 주석
/* 
여러 줄 주석
*/
div {}
```

## 중첩
```scss
div {
  background-color:aquamarine;

  p {
    font-size:20px;
    font-weight:bold;
  };
}
```

## 중첩된 속성
- 위는 아래와 같이 작성할 수 있다.
```scss
div {
  background-color:aquamarine;

  p {
    font: {
      size:20px;
      weight:bold;
    }
  };
}
```
- `font: {}` 콜론 주의

[🔝 목차](#목차)

## 상위 선택자
```scss
div {
  background-color:aquamarine;

  p {
    font-size:20px;

    &.hello {
      background-color: #ea779f;
    }
    &.scss {
      background-color: #4b7cde;
    }
  }
}
```
- Compiled to css
```css
div {
  background-color: aquamarine;
}
div p.hello {
  background-color: #ea779f;
}
div p.scss {
  background-color: #4b7cde;
}
```
### 👍 신기한 점
- `&`이 상위 선택자로 치환이 되는 듯
```jsx
<div id='container'>
  <p className='text-hello'>Hello, world!</p>
  <p className='text-scss'>SCSS</p>
</div>
```
```scss
p.text {
  &-hello {
    background-color: #ea779f;
  }
  &-scss {
    background-color: #4b7cde;
  }
}
```
- Compiled to css
```css
p.text-hello {
  background-color: #ea779f;
}
p.text-scss {
  background-color: #4b7cde;
}
```

[🔝 목차](#목차)

## 중첩을 벗어나 root 에 적용
- 아래 코드는 p 태그의 자식 요소에서 클래스를 찾기 때문에 `#ea779f`, `#4b7cde` 적용되지 않음
```scss
div {
  background-color:aquamarine;

  p {
    font-size:20px;

    .text {
      &-hello {
        background-color: #ea779f;
      }
      &-scss {
        background-color: #4b7cde;
      }
    }
  }
}
```
- Compiled to css
```css
div {
  background-color: aquamarine;
}
div p .text-hello {
  background-color: #ea779f;
}
div p .text-scss {
  background-color: #4b7cde;
}
```

### 👍 `@at-root` 사용

```scss
div {
  background-color:aquamarine;

  p {
    font-size:20px;

    @at-root .text {
      &-hello {
        background-color: #ea779f;
      }
      &-scss {
        background-color: #4b7cde;
      }
    }
  }
}
```
- Compiled to css
```css
div {
  background-color: aquamarine;
}
.text-hello {
  background-color: #ea779f;
}
.text-scss {
  background-color: #4b7cde;
}
```
- `@at-root {}` 형태로 여러 요소 묶어서도 작성 가능
```scss
@at-root {
  .text {
    &-hello {
      background-color: #ea779f;
    }
    &-scss {
      background-color: #4b7cde;
    }
  }
}
```

[🔝 목차](#목차)

## 변수
- 앞에 `$` 키워드 사용
- scope : 블록 `{}` 단위
```text
$변수명: 속성;
```
```scss
$pink: #ea779f;
$blue: #4b7cde;

p {
  font-size:20px;

  &.text {
    &-hello {
      background-color: $pink;
    }
    &-scss {
      background-color: $blue;
    }
  }
}
```
- 재할당 가능
```scss
$pink: #ea779f;
$blue: #4b7cde;

div {
  $pink: purple;
  
  background-color:aquamarine;
  color: $pink;  // 보라색 글씨
}
p {
  font-size:20px;

  &.text {
    &-hello {
      background-color: $pink;  // 분홍색 배경
    }
    &-scss {
      background-color: $blue;
    }
  }
}
```
![](.%5B20210514%5D_scss_syntax_images/a5a204ef.png)

[🔝 목차](#목차)

## 전역 변수
- `!global`
```text
$변수명: 속성!global;
```
```scss
$pink: #ea779f;
$blue: #4b7cde;

div {
  // 💡 전역 변수 선언
  $pink: purple!global;

  background-color:aquamarine;
  color: $pink;  // 보라색 글씨
}
p {
  font-size:20px;

  &.text {
    &-hello {
      background-color: $pink;  // 💡 보라색 배경
    }
    &-scss {
      background-color: $blue;
    }
  }
}
```

[🔝 목차](#목차)

## 초깃값
- `!default`
```text
$변수명: 속성!default;
```
```scss
$pink: #ea779f;
$blue: #4b7cde;

div {
  // 💡 보라색을 할당했지만 !default 키워드 때문에 기존 값(분홍색)을 사용
  $pink: purple!default;

  background-color:aquamarine;
  color: $pink;  // 분홍 글씨
}
p {
  font-size:20px;

  &.text {
    &-hello {
      background-color: $pink;  // 분홍 배경
    }
    &-scss {
      background-color: $blue;
    }
  }
}
```

[🔝 목차](#목차)

## 파일 분할
- scss 파일명 앞에 `_` 키워드가 있을 경우 별도의 파일로 컴파일 하지 않음.
### 일반적인 경우
- main.scss, sub1.scss, sub2.scss
- scss/main.scss 에 sub1.scss, sub2.scss import 
```scss
@import 'sub1', 'sub2';
```
- compile
```text
node-sass scss --output css
```
- output \
![](.%5B20210514%5D_scss_syntax_images/271f106a.png)
  
### `_` 키워드 사용
- main.scss, _sub1.scss, _sub2.scss
- output \
![](.%5B20210514%5D_scss_syntax_images/4b9e2020.png)

[🔝 목차](#목차)

## 조건문, 논리
- if 함수
  ```scss
  if(조건, true일 때, false일 때)
  ```
- 지시어 `@if` `@else if` `@else`
- 논리 `and` `or` `not`
```scss
$height: -1px;

.text-hello:after {
  @if($height > 100) {
    content: '높다';
  } @else if($height > 50) {
    content: '중간';
  } @else if($height > 0) {
    content: '낮다';
  } @else {
    content: '알 수 없음';
  }
}
```

[🔝 목차](#목차)

## 재사용 그룹
- 선언 `@mixin`
- 사용 `@include`
```scss
// 선언
@mixin primary-font-style {
  font-size: 20px;
  font-weight: bold;
  color: #ffffff;
}

p {
  // 사용
  @include primary-font-style;
}
```

### 매개변수
- 기본값 설정 가능
  - `$변수: 기본값`
```scss
// 선언
@mixin primary-font-style($size, $weight) {
  font-size: $size;
  font-weight: $weight;
  color: #ffffff;
}

p {
  // 사용
  @include primary-font-style(20px, weight);
}
```

[🔝 목차](#목차)

## 함수
```scss
// 선언
@function 함수명($매개변수) {
  @return 값;
}

// 사용
함수명();
```
- `@mixin`은 스타일 반환, `@function`은 값 반환
- 내장 함수와 충돌하지 않도록 네이밍 신경 쓰기

[🔝 목차](#목차)

## 반복문 for
```scss
$base-color: #036;

@for $i from 1 through 3 {
  ul:nth-child(3n + #{$i}) {
    background-color: lighten($base-color, $i * 5%);
  }
}
```
- Compiled to CSS
```css
ul:nth-child(3n + 1) {
  background-color: #004080;
}

ul:nth-child(3n + 2) {
  background-color: #004d99;
}

ul:nth-child(3n + 3) {
  background-color: #0059b3;
}
```

[🔝 목차](#목차)

## 반복문 each
```scss
$sizes: 40px, 50px, 80px;

@each $size in $sizes {
  .icon-#{$size} {
    font-size: $size;
    height: $size;
    width: $size;
  }
}
```
- Compiled to CSS
```css
.icon-40px {
  font-size: 40px;
  height: 40px;
  width: 40px;
}

.icon-50px {
  font-size: 50px;
  height: 50px;
  width: 50px;
}

.icon-80px {
  font-size: 80px;
  height: 80px;
  width: 80px;
}
```

[🔝 목차](#목차)

## 반복문 while
```scss
/// Divides `$value` by `$ratio` until it's below `$base`.
@function scale-below($value, $base, $ratio: 1.618) {
  @while $value > $base {
    $value: $value / $ratio;
  }
  @return $value;
}

$normal-font-size: 16px;
sup {
  font-size: scale-below(20px, 16px);
}
```
- Compiled to CSS
```css
sup {
  font-size: 12.36094px;
}
```

[🔝 목차](#목차)

## Built-In Modules
- https://sass-lang.com/documentation/modules

[🔝 목차](#목차)

##### * References
- [Sass(SCSS) 완전 정복!](https://heropy.blog/2018/01/31/sass/#sasswa-scssneun-caijeomeun-mweongayo)
- https://sass-lang.com/documentation

[🔝 목차](#목차)
