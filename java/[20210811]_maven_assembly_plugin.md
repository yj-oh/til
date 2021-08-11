# 빌드할 때 일부 폴더 .zip 으로 묶기 - maven-assembly-plugin
- maven 프로젝트 jar 로 빌드하는데 특정 폴더는 .zip 으로 묶고 싶다.
- `maven-assembly-plugin` 사용.

## pom.xml
```xml
<build>
    <plugins>
        <plugin>
            <artifactId>maven-assembly-plugin</artifactId>
            <version>3.3.0</version>
            <executions>
                <execution>
                    <id>resources-zip</id>
                    <goals>
                        <goal>single</goal>
                    </goals>
                    <phase>package</phase>
                    <configuration>
                        <finalName>resources</finalName>
                        <appendAssemblyId>false</appendAssemblyId>
                        <descriptors>
                            <descriptor>./assembly.xml</descriptor>
                        </descriptors>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

## assembly.xml
```xml
<assembly>
    <id>resources-zip</id>
    <includeBaseDirectory>false</includeBaseDirectory>
    <formats>
    	<format>zip</format>
    </formats>

    <fileSets>
        <fileSet>
            <directory>resources</directory>
            <!-- 위에서 지정한 디렉토리 내용물이 zip 안에, test1 폴더에 들어간다. -->
            <outputDirectory>test1/</outputDirectory>
        </fileSet>
        <fileSet>
            <directory>resources2</directory>
            <outputDirectory>test2/</outputDirectory>
        </fileSet>
    </fileSets>
</assembly>
```

## 결과물
```text
resources.zip
|-- test1
|   `-- resources files
`-- test2
    `-- resources2 files
```
