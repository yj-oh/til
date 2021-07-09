# Logback default values
- logback 설정 xml에 기본값을 지정하고 싶다.
```xml
<configuration>
    <property name="PATH" value="${PATH}" />
</configuration>
```
- Bash Shell 의 `:-`를 사용할 수 있다.

```xml
<configuration>
    <property name="PATH" value="${PATH:-./}" />
</configuration>
```

- 참고 : http://logback.qos.ch/manual/configuration.html
