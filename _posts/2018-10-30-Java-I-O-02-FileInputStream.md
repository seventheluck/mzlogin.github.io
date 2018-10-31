---
layout: post
title: Java I/O - 02 FileInputStream
categories: Java
description: Java I/O - 02 FileInputStream
keywords: Java, I/O
---

FileInputStream class: subclass of InputStream abstract class. 
create an input stream, used to read byte/bytes from a file. 
#### 1. Constructors :

##### A. FileInputStream(File file)
```java
    File file= new File("D:\\Textbook.txt");
    FileInputStream fis= new FileInputStream(file);
```
 

##### B. FileInputStream(String path)
```java
    FileInputStream fis= new FileInputStream("D:\\TextBook.txt");
```
#### 2. Code examples
```java
package filesAndIo.byteStreams;

import java.io.*;

public class BytesInputStream {

    public static void main(String[] args) throws IOException {
        File file = new File("/Users/petter/test/test.txt");
        FileInputStream fileInputStream = new FileInputStream(file);
        FileInputStream fileInputStream1 = new FileInputStream("/Users/petter/test/test.txt");
        int available = fileInputStream1.available();
        System.out.println(available);
        byte[] result = new byte[available];
        fileInputStream1.read(result);
        fileInputStream1.close();
        String str = new String(result);
        System.out.println("======================");
        System.out.println(str);
    }
}

```
