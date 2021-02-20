# nth-child vs nth-of-type
- 이전에 블로그에 정리한 게 있는데 간만에 퍼블리싱 하려니 또 헷갈려서 다시 정리.

# 결론
- `nth-child` : 지정한 태그의 `형제 태그 전체` 중, 지정한 순서에 해당 태그가 있으면 적용
- `nth-of-type` : 지정한 태그의 `같은 타입 형제` 중, 지정한 순서에 해당하는 태그에 적용


## 예제
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Test</title>
<style>
    .sub { margin-left:50px; }
</style>
</head>
<body>

<div>
    <p>1</p>
    <p>2</p>
    <div class="sub">
        <p>1</p>
        <p>2</p>
        <p>3</p>
        <p>4</p>
    </div>
    <p>3</p>
    <p>4</p>
</div>

</body>
</html>
```

# nth-child
```css
p:nth-child(2) { background-color:#d2ad4f; /* 노랑 */ }
p:nth-child(3) { background-color:#43439b; /* 보라 */ }
```
![](.%5B20210220%5D_nth_child_vs_nth_of_type_images/dc176434.png)

# nth-of-type
```css
p:nth-of-type(2) { background-color:#d2ad4f; /* 노랑 */ }
p:nth-of-type(3) { background-color:#43439b; /* 보라 */ }
```
![](.%5B20210220%5D_nth_child_vs_nth_of_type_images/fc75d506.png)

# 왜?
## `p:nth-child`
- `같은 부모를 가진 형제 태그 전체 중`에 n번째에 p 태그가 있으면 선택
  ```html
  <div>
    <p>1</p>                <!-- 1번 -->
    <p>2</p>                <!-- 2번 --><!-- 2번, p 태그이므로 노랑 -->
    <div class="sub">       <!-- 3번 --><!-- 3번이지만 p 태그가 아니므로 선택 X -->
        <p>1</p>        <!-- 1번 -->
        <p>2</p>        <!-- 2번 --><!-- 2번, p 태그이므로 노랑 -->
        <p>3</p>        <!-- 3번 --><!-- 3번, p 태그이므로 보라 -->
        <p>4</p>        <!-- 4번 -->
    </div>
    <p>3</p>                <!-- 4번 -->
    <p>4</p>                <!-- 5번 -->
  </div>
  ```
  ![](.%5B20210220%5D_nth_child_vs_nth_of_type_images/dc176434.png)

## `p:nth-of-type`
- `같은 부모를 가진 p 태그 중`에 n번째 p 태그 선택
  ```html
  <div>
    <p>1</p>                <!-- 1번 -->
    <p>2</p>                <!-- 2번 --><!-- 노랑 -->
    <div class="sub">       
        <p>1</p>        <!-- 1번 -->
        <p>2</p>        <!-- 2번 --><!-- 노랑 -->
        <p>3</p>        <!-- 3번 --><!-- 보라 -->
        <p>4</p>        <!-- 4번 -->
    </div>
    <p>3</p>                <!-- 3번 --><!-- 보라 -->
    <p>4</p>                <!-- 4번 -->
  </div>
  ```
  ![](.%5B20210220%5D_nth_child_vs_nth_of_type_images/fc75d506.png)
