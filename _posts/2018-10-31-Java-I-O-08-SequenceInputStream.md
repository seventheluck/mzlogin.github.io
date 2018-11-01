---
layout: post
title: Java I/O - 08 SequenceInputStream
categories: Java
description: Java I/O - 08 SequenceInputStream
keywords: Java, I/O
---

#### 1. Constructor
```java
FileInputStream fis1 = new FileInputStream("/Users/petter/test/test.txt");
FileInputStream fis2 = new FileInputStream("/Users/petter/test/test.txt");
SequenceInputStream sis = new SequenceInputStream(fis1, fis2);
```

#### 2. Examples

```java
package filesAndIo.byteStreams;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.SequenceInputStream;

public class SequenceInputStreamClasses {

    public static void main(String[] args) {
        try {
            FileInputStream fis1 = new FileInputStream("/Users/petter/test/testBufferedOutputStream.txt");
            FileInputStream fis2 = new FileInputStream("/Users/petter/test/testBufferedOutputStream.txt");
            SequenceInputStream sis = new SequenceInputStream(fis1, fis2);
            int c = sis.read();
            while (c != -1) {
                System.out.print((char) c);
                c = sis.read();
            }
            fis1.close();
            fis2.close();
            sis.close();
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}

```