# PrintWriter vs FileWriter
- 새로 파일을 생성해서 내용 쓰는 작업 중.
```java
import java.io.*;

public class Example {
    public static void main(String[] args) {

    	File printWriterFile = new File("PrintWriter.txt");
    	File fileWriterFile = new File("FileWriter.txt");

    	try {
            PrintWriter printWriter = new PrintWriter(printWriterFile);
            printWriter.write("Hello, World!");
            printWriter.close();

            FileWriter fileWriter = new FileWriter(fileWriterFile);
            fileWriter.write("Hello, World!");
            fileWriter.close();
    		
    	} catch (IOException e) {
            e.printStackTrace();
    	}

    }
}
```
- 결과는?
  - PrintWriter.txt, FileWriter.txt 가 생성되고 내용도 "Hello, world!" 잘 써졌다.
- 그럼 둘은 무슨 차이가 있나 궁금해짐.

---

# 👉 1. 메소드
- 아래의 내용이 담긴 파일을 각각 생성해본다.
```text
Hello, World!I'm Yunju.:)
이건 새로운 줄에 쓰여지겠지.
이것도 NEW 줄에 쓰여질 것이고요.
```

## PrintWriter
```java
public static void main(String[] args) {

    File printWriterFile = new File("PrintWriter.txt");
    
    try {
        PrintWriter printWriter = new PrintWriter(printWriterFile);
        
        printWriter.write("Hello, World!");
        printWriter.write("I'm Yunju.");
        printWriter.println(":)");
        printWriter.append("이건 새로운 줄에 쓰여지겠지.");
        printWriter.println();
        printWriter.printf("이것도 %s 줄에 쓰여질 것이고요.", "NEW");
        
        printWriter.close();
    
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```
- printf(), println() 메소드를 자체적으로 가지고 있음.

## FileWriter
```java
public static void main(String[] args) {

    File fileWriterFile = new File("FileWriter.txt");

    try {
        FileWriter fileWriter = new FileWriter(fileWriterFile);
        
        fileWriter.write("Hello, World!");
        fileWriter.write("I'm Yunju.");
        fileWriter.write(":)\n");
        fileWriter.append("이건 새로운 줄에 쓰여지겠지.");
        fileWriter.append("\n");
        fileWriter.append(String.format("이것도 %s 줄에 쓰여질 것이고요.", "NEW"));
        
        fileWriter.close();
    
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```
- 줄 바꿈 해주려면 "\n" 등 사용해야 함.
- 문자열 포맷 지정도 String.format() 사용해야 함.

# 👉 2. 예외
- try-catch 벗겨보자.

## PrintWriter
```java
public static void main(String[] args){
    File printWriterFile = new File("PrintWriter.txt");

    // 🚨 Unhandled exception: java.io.FileNotFoundException
    PrintWriter printWriter = new PrintWriter(printWriterFile);
    
    printWriter.write("Hello, World!");
    printWriter.write("I'm Yunju.");
    printWriter.println(":)");
    printWriter.append("이건 새로운 줄에 쓰여지겠지.");
    printWriter.println();
    printWriter.printf("이것도 %s 줄에 쓰여질 것이고요.","NEW");
    
    printWriter.close();
}
```
- 메소드들이 `IOException` 던지지 않음.
- 일부 생성자에서만 IOException, FileNotFoundException 등을 던짐.
- 대신 `checkError()` 가 있다.
```java
public static void main(String[] args) {

    File printWriterFile = new File("PrintWriter.txt");

    PrintWriter printWriter = null;

    try {
    	printWriter = new PrintWriter(printWriterFile);
    } catch (FileNotFoundException e) {
    	e.printStackTrace();
    }
    printWriter.write("Hello, World!");
    
    System.out.println(printWriter.checkError());  // return false

    printWriter.close();
}
```

## FileWriter
```java
public static void main(String[] args){
    File fileWriterFile = new File("FileWriter.txt");
    
    // 🚨 Unhandled exception: java.io.IOException
    FileWriter fileWriter = new FileWriter(fileWriterFile);
    
    // write(), append() 모두 🚨 Unhandled exception: java.io.IOException
    fileWriter.write("Hello, World!");
    fileWriter.write("I'm Yunju.");
    fileWriter.write(":)\n");
    fileWriter.append("이건 새로운 줄에 쓰여지겠지.");
    fileWriter.append("\n");
    fileWriter.append(String.format("이것도 %s 줄에 쓰여질 것이고요.","NEW"));
    
    fileWriter.close();
}
```
- `IOException` 던짐.

# 👉 3. 문자 인코딩
## PrintWriter, FileWriter
```java
public static void main(String[] args) {

    File printWriterFile = new File("PrintWriter.txt");
    File fileWriterFile = new File("FileWriter.txt");

    try {
    	PrintWriter printWriter 
            = new PrintWriter(printWriterFile, StandardCharsets.UTF_8);
    	printWriter.write("안녕");
    	printWriter.close();

        FileWriter fileWriter
            = new FileWriter(fileWriterFile, StandardCharsets.UTF_8);
        fileWriter.write("안녕");
        fileWriter.close();

    } catch (IOException e) {
    	e.printStackTrace();
    }

}
```
- 둘 다 `Charset`을 파라미터로 가진 생성자가 존재함.

# 👉 4. auto flushing
## PrintWriter
- 생성자 파라미터에 `autoFlush`를 boolean으로 받음.
```java
PrintWriter printWriter 
        = new PrintWriter(new FileOutputStream(printWriterFile), true);
```
## FileWriter
- 그런 옵션은 없음.

---

# 💡 결론
![](.%5B20210808%5D_printwriter_vs_filewriter_images/4bcc8ca4.png)
* *이미지 출처 : https://medium.com/geekculture/using-printwriter-vs-filewriter-in-java-2958df85f105*

## 👉 공통점
- Writer 클래스를 상속함.
- 문자를 쓰기 위함.

## 👉 차이점
분류 | PrintWriter | FileWriter
--- | --- | ---
줄 바꿈 | println() | 줄 바꿈 문자 사용
문자열 포맷 | printf() | String.format()
예외 | 일부 생성자에서만, 메소드는 X | IOException
autoFlush | O | X

---

##### References
- `PrintWriter` https://docs.oracle.com/javase/8/docs/api/java/io/PrintWriter.html
- `FileWriter` https://docs.oracle.com/javase/8/docs/api/java/io/FileWriter.html
- https://stackoverflow.com/questions/5759925/printwriter-vs-filewriter-in-java
- https://medium.com/geekculture/using-printwriter-vs-filewriter-in-java-2958df85f105
