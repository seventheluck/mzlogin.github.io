---
layout: post
title: Java I/O - 05 ByteArrayOutputStream
categories: Java
description: Java I/O - 05 ByteArrayOutputStream
keywords: Java, I/O
---
This method will reads bytes from byte array and writes the content to its own internal buffer. Then ByteArrayOutputStream writes its content of internal buffer to file.
#### 1. Constructor

```java
String str = "This is a test for ByteArrayOutputStream, this method will reads bytes from byte array and writes the content to its own internal buffer. Then ByteArrayOutputStream writes its content of internal buffer to file.";
byte[] bytes = str.getBytes();
ByteArrayOutputStream bos = new ByteArrayOutputStream();
```
#### 2. Examples

```java
package filesAndIo.byteStreams;

import java.io.*;

public class ByteArrayOutputStreamClasses {
    public static void main(String[] args) {
        String str = "This is a test for ByteArrayOutputStream, this method will reads bytes from byte array and writes the content to its own internal buffer. Then ByteArrayOutputStream writes its content of internal buffer to file.";
        byte[] bytes = str.getBytes();
        ByteArrayOutputStream bos = new ByteArrayOutputStream();
        FileOutputStream fis = null;
        try {
            fis = new FileOutputStream("/Users/petter/test/testByteArrayOutputStream.txt");
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
        try {
            bos.write(bytes);
            bos.writeTo(fis);
            bos.flush();
            bos.close();
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}
```