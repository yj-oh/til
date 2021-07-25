# 실행 가능한 uber-JAR 만들기
- uber-JAR에 대해 알아봤었다.
  - [Maven 프로젝트, 라이브러리까지 포함하여 build 하기 (feat. uber-JAR)]([20210702]_uber_jar.md)
  
## pom.xml
### 기본 형태
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
            </execution>
        </executions>
    </plugin>
</build>
```

### 실행 가능한 형태
- 아래의 main class 진입점을 `<execution>` 하위에 추가해준다.
```xml
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
```

##### * Reference : https://maven.apache.org/plugins/maven-shade-plugin/examples/executable-jar.html
