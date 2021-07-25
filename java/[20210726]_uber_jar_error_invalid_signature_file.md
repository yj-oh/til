# uber-JAR Error : Invalid signature file
- uber-JAR에 대해 알아봤었다.
  - [Maven 프로젝트, 라이브러리까지 포함하여 build 하기 (feat. uber-JAR)]([20210702]_uber_jar.md)
  - [실행 가능한 uber-JAR 만들기]([20210725]_create_executable_user_jar.md)
## 🤔 상황
- 실행 가능한 형태의 uber-JAR 만들기 위해 maven build 설정
### pom.xml
```xml
<build>
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
        <version>3.2.4</version>
        <executions>
            <execution>
                <phase>package</phase>
                <goals>
                    <goal>shade</goal>
                </goals>
                <configuration>
                    <transformers>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                            <manifestEntries>
                            	<Main-Class>com.yjworld.java.Main</Main-Class>
                            </manifestEntries>
                        </transformer>
                    </transformers>
                    <outputFile>target/${project.artifactId}.jar</outputFile>
                </configuration>
            </execution>
        </executions>
    </plugin>
</build>
```
- 실행하는데 에러가 발생했다.
```text
Exception in thread "main" java.lang.SecurityException:
  Invalid signature file digest for Manifest main attributes
```

## 💡 해결
- 모든 jar 풀어서 하나로 다시 묶는데, Manifest가 있는 jar 파일이 
  포함되어 있을 경우 발생하는 에러라고 한다.
- `<configuration>` 하위에 아래 manifest signature 제외하는 설정을 추가한다.
```xml
<filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
</filters>
```
##### * Reference : https://www.lesstif.com/java/uber-jar-maven-shade-plugin-24446041.html
