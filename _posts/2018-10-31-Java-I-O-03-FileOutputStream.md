---
layout: post
title: Java I/O - 03 FileOutputStream
categories: Java
description: Java I/O - 03 FileOutputStream
keywords: Java, I/O
---

#### 1. Constructor
##### A. FileOutputStream(File file)
```java
File file = new File("/Users/petter/test/testoutput.txt");
FileInputStream fis= new FileInputStream(file);
```
##### B. FileOutputStream(String path)
```java
FileOutputStream fis= new FileOutputStream("/Users/petter/test/testoutput.txt");
```
#### 2. Examples
```java
package filesAndIo.byteStreams;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;

public class BytesOutputStream {

    public static void main(String[] args) throws IOException {
        File file = new File("/Users/petter/test/testoutput.txt");
        FileOutputStream fileOutputStream = new FileOutputStream(file);
        String str = "I want to write something by using file output stream!\nIs it Ok?";
        byte[] result = str.getBytes();
        fileOutputStream.write(result);
        //fileOutputStream.flush();//FileOutputStream is not buffered stream, so we do not need to use flush() here.
        fileOutputStream.close();
    }
}
```