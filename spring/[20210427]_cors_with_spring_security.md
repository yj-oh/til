# Spring Security 를 사용하는 프로젝트에서 CORS 설정

### 참고
* _[CORS에 대한 이해](../etc/[20210221]_cors.md)_
* _[Spring Boot - CORS 설정하기]([20210222]_spring_boot_cors.md)_

## 🤔 상황
- CORS 가 뭔지, Spring boot 프로젝트에 어떻게 설정하는지는 이전에 정리했었다. (위의 링크 참고)
- 오늘 다른 프로젝트에 CORS 적용을 하면서, preflight 가 실패하며 401이 떨어지는 상황을 만났다.
```text
XMLHttpRequest cannot load http://localhost:8080/test. 
No 'Access-Control-Allow-Origin' header is present on the requested resource.
Origin http://localhost:3000 is therefore not allowed access. 
The response had HTTP status code 401.
```

### 설정
- /src/main/java/{package}/config/WebConfig.java
```java
@EnableWebMvc
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) { 
    	registry.addMapping("/**")
                .allowedOrigins("*")
                .allowedMethods("GET", "POST")
                .maxAge(1000);
    }
}
```
- 이런 식으로 적용은 잘 되어있었고, 다른 프로젝트의 CORS 설정과 다를 바가 없었다.

## 💭 원인
- https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#filters-cors
```text
Spring MVC provides fine-grained support for CORS configuration 
through annotations on controllers. However, when used with Spring Security, 
we advise relying on the built-in CorsFilter that must be ordered 
ahead of Spring Security’s chain of filters.
```
- Spring Security 와 함께 사용할 경우 CorsFilter 가 
  시큐리티의 필터 체인보다 먼저 호출되어야 한단다.
- 내장된 CorsFilter 를 사용하지는 않고 전역 설정을 하고 있는 듯한데.
- 아무튼 CORS 체크하기 전에 시큐리티의 필터가 먼저 호출되어 401 떨구는 것 같다.

## 💡 해결
- WebSecurityConfigurerAdapter 클래스를 상속 받는 SecurityConfig 를 정의해두었다.

#### /src/main/java/{package}/config/SecurityConfig.java
```java
@EnableWebSecurity
@Configuration
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    // ...
    
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
                .anyRequest().authenticated()
                .and()
                .csrf().disable();
    }
}
```

- `http.cors()`를 추가해주었다.
```java
@EnableWebSecurity
@Configuration
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    // ...
    
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.cors()
                .and()
                .authorizeRequests()
                .anyRequest().authenticated()
                .and()
                .csrf().disable();
    }
}
```

##### * References
- https://stackoverflow.com/questions/40418441/spring-security-cors-filter
- https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#filters-cors
- https://docs.spring.io/spring-security/site/docs/4.2.x/reference/html/cors.html
