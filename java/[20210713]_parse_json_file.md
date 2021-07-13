# JSON 파싱하는 다양한 방법 (Maven)
- 아래 3가지를 이용한 방법을 알아볼 것이다.
>1. [Org.JSON](#Org.JSON)
>2. [Google.Gson](#Google.Gson)
>3. [Jackson](#Jackson)
- https://stackoverflow.com/questions/2591098/how-to-parse-json-in-java
  - 위의 stackoverflow 답변을 참고해서 직접 실행해봄.

---

- 예제 프로젝트를 하나 팠다.
- https://github.com/yj-oh/json-parsing-examples.git

![Project Structure](.%5B20210713%5D_parse_json_file_images/b0d85239.png)

### resources/sample.json
- 파싱할 때 사용할 sample.json 파일을 생성한다.
```json
{
  "uuid": "03adf601-8c53-468e-b423-e29609f5c479",
  "color": {
    "id": "color01",
    "name": "white",
    "hex": "#ffffff"
  },
  "animals": [
    {
      "id": 1,
      "name": "오춘식",
      "type": "hamster"
    },
    {
      "id": 2,
      "name": "오춘무",
      "type": "fish"
    }
  ]
}
```

### Main.java
- 우선 sample.json 파일을 읽어서 String 변수에 담아둔다.
```java
public class Main {
    public static void main(String[] args) throws IOException {
    	String jsonString = readFile("/sample.json");
    }

    static String readFile(String fileName) throws IOException {
    	return IOUtils.resourceToString(fileName, Charset.defaultCharset());
    }
}
```

## Org.JSON
### pom.xml
```xml
<properties>
    <org.json.version>20210307</org.json.version>
</properties>

<dependencies>
    <!-- https://mvnrepository.com/artifact/org.json/json -->
    <dependency>
        <groupId>org.json</groupId>
        <artifactId>json</artifactId>
        <version>${org.json.version}</version>
    </dependency>
</dependencies>
```

```java
// JSON
JSONObject jsonObject = new JSONObject(jsonString);

System.out.println(jsonObject.get("uuid"));

// JSON 안의 JSON Object
JSONObject colorObject = jsonObject.getJSONObject("color");

System.out.println(colorObject.get("hex"));

// JSON 안의 Array 안의 JSON Object
JSONArray jsonArray = jsonObject.getJSONArray("animals");
for (int i = 0; i < jsonArray.length(); i++) {
    JSONObject animalObject = jsonArray.getJSONObject(i);
    
    System.out.println(animalObject.get("name"));
}
```

## Google.Gson
### pom.xml
```xml
<properties>
    <google.gson.version>2.8.7</google.gson.version>
</properties>

<dependencies>
    <!-- https://mvnrepository.com/artifact/com.google.code.gson/gson -->
    <dependency>
        <groupId>com.google.code.gson</groupId>
        <artifactId>gson</artifactId>
        <version>${google.gson.version}</version>
    </dependency>
</dependencies>
```

```java
// JSON
JsonObject jsonObject = JsonParser.parseString(jsonString).getAsJsonObject();

System.out.println(jsonObject.get("uuid").getAsString());

// JSON 안의 JSON Object
JsonObject colorObject = jsonObject.getAsJsonObject("color");

System.out.println(colorObject.get("hex").getAsString());

// JSON 안의 Array 안의 JSON Object
JsonArray jsonArray = jsonObject.getAsJsonArray("animals");
for (int i = 0; i < jsonArray.size(); i++) {
    JsonObject animalObject = jsonArray.get(i).getAsJsonObject();
    
    System.out.println(animalObject.get("name").getAsString());
}
```
### 다른 방법도 있다.
- JSON Object 구조대로 Java Object 생성

### Sample.java
```java
package com.example.jsonparsing;

public class Sample {
    private String uuid;
    private Color color;
    private Animal[] animals;
    
    // ... getter 생략

    static class Color {
    	private String id;
    	private String name;
    	private String hex;

    	// ... getter 생략
    }

    static class Animal {
        private Long id;
        private String name;
        private String type;

        // ... getter 생략
    }
}
```
```java
// 또다른 방법 : class 사용
Sample sample = new Gson().fromJson(jsonString, Sample.class);

System.out.println(sample.getUuid());
System.out.println(sample.getColor().getHex());
System.out.println(sample.getAnimals()[0].getName());
```

## Jackson
### pom.xml
```xml
<properties>
    <jackson.databind.version>2.12.4</jackson.databind.version>
</properties>

<dependencies>
    <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>${jackson.databind.version}</version>
    </dependency>
</dependencies>
```
- 위에서 만든 Sample.java 이용한다.
```java
ObjectMapper mapper = new ObjectMapper();

Sample sample = mapper.readValue(jsonString, Sample.class);
System.out.println(sample.getUuid());
System.out.println(sample.getColor().getHex());
System.out.println(sample.getAnimals()[0].getName());
```
