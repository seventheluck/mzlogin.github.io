---
layout: post
title: Java I/O - 09 DataInputStream
categories: Java
description: Java I/O - 09 DataInputStream
keywords: Java, I/O
---

#### 1. Constructor
```java
File file = new File("/Users/petter/test/testDataInputStream.txt");
FileInputStream fis = new FileInputStream(file);
DataInputStream dis = new DataInputStream(fis);
```

#### 2. Examples

```java
package filesAndIo.byteStreams;

import java.io.*;

public class DataInputStreamClasses {

    public static void main(String[] args) {
        File file = new File("/Users/petter/test/testDataInputStream.txt");
        try {
            FileInputStream fis = new FileInputStream(file);
            DataInputStream dis = new DataInputStream(fis);
            System.out.println(dis.readInt());

        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}

```