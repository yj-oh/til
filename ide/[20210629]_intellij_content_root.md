# IntelliJ 프로젝트 폴더 구성하기
- 참고 : [IntelliJ Content roots](https://www.jetbrains.com/help/idea/content-roots.html)

---

## 상황
- Java 프로젝트를 생성했는데 밑바닥부터 폴더 구성 하나하나 하다보니 패키지 등이
  일반 패키지로 구성되었다.
  
  ![](.%5B20210629%5D_intellij_content_root_images/ed11b957.png)

- resources, test 등 각 용도에 맞게 mark 해놓고 싶은데
  디렉토리 오른쪽 버튼 클릭 -> `Mark Directory as`에는 `Excluded` 밖에 없다.

## 해결
- File - Project Structure... - Project Settings - Modules

![](.%5B20210629%5D_intellij_content_root_images/3407052d.png)
