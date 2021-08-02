# Jenkins unmappable character * for encoding

## 상황
- Maven project jenkins에서 빌드하는데 콘솔에 붉게 에러가 떴다.
```text
[ERROR] /C:/project/build/project/ 
[ERROR] /C:/project/src/main/java/com/yjworld/test/Main.java:[1, 1]
  unmappable character (0xED) for encoding x-windows-949dicracter 
  (0xED) for encoding x-windows-949
```

## 해결
- pom.xml 에 encoding UTF-8 설정을 해준다.

#### pom.xml
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <encoding>UTF-8</encoding>
            </configuration>
        </plugin>
    </plugins>
</build>
```
