# 디렉토리 생성
- 참고 : https://mkyong.com/java/how-to-create-directory-in-java/

---

## java.nio.file.Files

### `createDirectory()`
- 상위 디렉토리가 존재하지 않을 경우 `NoSuchFileException`
- 해당 디렉토리가 이미 존재할 경우 `FileAlreadyExistsException`

### `createDirectories()`
- 상위 디렉토리가 존재하지 않을 경우 전부 생성함.
- 해당 디렉토리가 이미 존재할 경우 Exception 발생하지 않음.

### 예제

```java
import java.io.IOException;
import java.nio.file.*;

public class Main {
    public static void main(String[] args) {

        try {
            Path path = Paths.get("D:\\examples\\test");
            Files.createDirectory(path);

            System.out.println("디렉토리 생성 완료");

        } catch (FileAlreadyExistsException e) {
            System.out.println("존재하는 디렉토리");
            
        } catch (NoSuchFileException e) {
            System.out.println("유효하지 않은 경로");
            
        } catch (IOException e) {
            System.out.println("입출력 오류");
        }

    }
}
```

## java.io.File
### `mkdir()`
- 디렉토리 생성

### `mkdirs()`
- 상위 디렉토리가 존재하지 않을 경우 전부 생성
```java
import java.io.File;

public class Main {
    public static void main(String[] args) {

    	File file = new File("D:\\examples\\test");
    	file.mkdirs();

    }
}
```

## 뭐 쓰지?
- `java.io.File`의 `mkdir()`, `mkdirs()`는 상위 디렉토리가 존재하든 존재하지 않든,
  해당 디렉토리가 이미 존재해도, 경로가 유효하지 않아도 해당 정보를 알려주지 않기 때문에
  **문제 상황에서 디버깅하기 어려울 수 있다.**
