# Controller에서 parameter받기
type | description | format
--- | --- | ---
@PathVariable | URL Path | /{id}/{name}/{team}
@RequestParam | Query Parameters | ?id={id}&name={name}&team={team}
@RequestBody | HTTP request body | 


## @PathVariable
```
Annotation which indicates that a method parameter should be bound to 
a URI template variable. Supported for RequestMapping annotated handler methods.
If the method parameter is Map<String, String> then the map is populated 
with all path variable names and values.
```
Type | Optional Element | Default | Description
--- | --- | --- | ---
String | name | "" | The name of the path variable to bind to.
boolean | required | true | Whether the path variable is required.
String | value | "" | Alias for name()

* *Reference : https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/bind/annotation/PathVariable.html*

```java
@RequestMapping(value = "/{id}")
public ResponseEntity<User> getUser(@PathVariable Long id) { ... }
```
→ call : http://localhost:8080/{id}

#### ex)
```java
@GetMapping(value = "/{id}")
public ResponseEntity<Classes> getClasses(@PathVariable Long id) {
	return new ResponseEntity<>(classesService.getClasses(id), HttpStatus.OK);
}
```
![@PathVariable](.%5B20200809%5D_controller에서_parameter_받기_images/ccfe1d2e.png)


## @RequestParam
```
Annotation which indicates that a method parameter 
should be bound to a web request parameter.
```
Type | Optional Element | Default | Description
--- | --- | --- | ---
String | defaultValue | "" | The default value to use as a fallback when the request parameter is not provided or has an empty value.
String | name | "" | The name of the request parameter to bind to.
boolean | required | true | Whether the parameter is required.
String | value |  | Alias for name()

* *Reference : https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/bind/annotation/RequestParam.html*

```java
@RequestMapping
public ResponseEntity<User> getUser(@RequestParam Long id) { ... }
```
→ call : http://localhost:8080?id={id}

#### ex)
```java
@GetMapping
public ResponseEntity<Classes> getClasses(@RequestParam(defaultValue = "1") Long id) {
	return new ResponseEntity<>(classesService.getClasses(id), HttpStatus.OK);
}
```
![@RequestParam](.%5B20200809%5D_controller에서_parameter_받기_images/76f1ddad.png)


## @RequestBody
```
Annotation indicating a method parameter should be bound to the body of the web 
request. The body of the request is passed through an HttpMessageConverter to 
resolve the method argument depending on the content type of the request. 
Optionally, automatic validation can be applied by annotating the argument 
with @Valid.
```
Type | Optional Element | Default | Description
--- | --- | --- | ---
boolean | required | true | Whether body content is required.
* *Reference : https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/bind/annotation/RequestBody.html*

```java
@GetMapping
public ResponseEntity<Classes> getClasses(@RequestBody Classes classes) {
	return new ResponseEntity<>(classesService.getClasses(classes.getId())
        , HttpStatus.OK);
}
```
→ call : http://localhost:8080

#### ex)
![](.%5B20200809%5D_controller에서_parameter_받기_images/32234802.png)

##### * References
- https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/bind/annotation/
- https://docs.spring.io/spring/docs/4.3.26.RELEASE/spring-framework-reference/htmlsingle/#mvc-ann-requestmapping-uri-templates
