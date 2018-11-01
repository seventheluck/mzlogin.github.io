---
layout: post
title: Java I/O - 10 DataOutputStream
categories: Java
description: Java I/O - 10 DataOutputStream
keywords: Java, I/O
---

#### 1. Constructor
```java
File file = new File("/Users/petter/test/testDataInputStream.txt");
FileOutputStream fos = new FileOutputStream(file);
DataOutputStream dos = new DataOutputStream(fos);
```

#### 2. Examples

```java
package filesAndIo.byteStreams;

import java.io.DataOutputStream;
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;

public class DataOutputStreamClasses {

    public static void main(String[] args) {
        File file = new File("/Users/petter/test/testDataInputStream.txt");
        try {
            FileOutputStream fos = new FileOutputStream(file);
            DataOutputStream dos = new DataOutputStream(fos);
            dos.writeInt(Integer.MAX_VALUE);
            dos.writeChars("Hello!");
            dos.writeChar('c');
            dos.writeDouble(0.01);
            dos.writeFloat((float) 0.1);
            dos.flush();
            fos.close();
            dos.close();
        } catch (IOException io) {
            System.out.println(io);
        }


    }
}

```