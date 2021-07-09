# Logback 빌드 환경에 따라 설정 파일 다르게 적용하기 - include
- 로컬, 개발, 운영에 따라 설정 파일을 다르게 적용하고 싶다.

## 💡 해결
### logback.xml
```xml
<configuration>
    <include resource="logback-${ENV:-local}.xml" />
</configuration>
```

### logback-*.xml
```xml
<included>
    <!-- configuration -->
</included>
```
- `${ENV}`에 들어갈 값을 설정하는 방법은 여러가지가 있다.

## VM Options
- 실행할 때 VM 옵션을 지정해준다.
```text
java [options] -jar <file>.jar
```
- e.g
```text
java -DENV=local MyApp.jar
```

### IntelliJ - Run/Debug Configurations
- IntelliJ에서 실행한다면 VM 옵션을 아래와 같이 설정하는 방법도 있다.
- Run/Debug Configurations \
![](.%5B20210710%5D_logback_include_images/9a99041c.png)

## .properties에서 가져오기
#### logback.properties
```properties
ENV=local
```
#### logback.xml

```xml

<configuration>
    <property file="src/main/resources/logback.properties" />
    <include resource="logback-${ENV:-local}.xml" />
</configuration>
```

## Programmatically
```java
public class MyApp {
    public static void main(String[] args) throws IOException, JoranException {
    	LoggerContext context = (LoggerContext) LoggerFactory.getILoggerFactory();

    	JoranConfigurator jc = new JoranConfigurator();
    	context.reset();

    	context.putProperty("ENV", "local");
    	jc.setContext(context);

    	InputStream inputStream = new FileInputStream("logback.xml");
    	jc.doConfigure(inputStream);
    }
}
```
