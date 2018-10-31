---
layout: post
title: Java I/O - 04 ByteArrayInputStream
categories: Java
description: Java I/O - 04 ByteArrayInputStream
keywords: Java, I/O
---
ByteArrayInputStream was used to creat a input stream from an array just like this:
byte array --> ByteArrayInputStream

#### 1. Constructor
```java
ByteArrayInputStream(byte[] bytes);
```

#### 2. Examples
```java
package filesAndIo.byteStreams;

import java.io.ByteArrayInputStream;
import java.io.IOException;

public class ByteArrayInputStreamClasses {
    public static void main(String[] args) {
        String str = "This is a test for ByteArrayInputStream.";
        byte[] result = str.getBytes();
        ByteArrayInputStream bis = new ByteArrayInputStream(result);
        int c = bis.read();
        while (c != -1) {
            System.out.print((char) c);
            c = bis.read();
        }
        try {
            bis.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```