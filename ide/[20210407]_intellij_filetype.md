# IntelliJ 파일 형식 인식 못할 때

## 🤔 상황
- 후다닥 파일을 생성하다가 파일 형식을 지정하지 않아 아래와 같은 창이 뜸.

![](.%5B20210407%5D_intellij_filetype_images/246b815c.png)

- 급해서 확인 안 하고 엔터엔터엔터 침.
- java 클래스를 생성해야 하는데 `text` 파일로 인식.
- 파일을 지우고 재생성 해도 같은 이름의 파일을 생성하면 무조건 text 파일로 인식.

## 💡 해결
- Preferences - Editor - File Types

![](.%5B20210407%5D_intellij_filetype_images/62ce35fc.png)

- `File name patterns`에서 해당 파일명의 패턴을 찾아 삭제한다.
- 당연히 `Text` 타입에 있을 줄 알았는데 없어서 하나하나 찾아봄.
- `Auto-detect file type by content` 타입에 있었다.
