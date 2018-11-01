---
layout: post
title: Java I/O - 11 PrintWriter
categories: Java
description: Java I/O - 11 PrintWriter
keywords: Java, I/O
---

#### 1. Constructor

```java
FileOutputStream fos = new FileOutputStream("/Users/petter/test/testPrintStream.txt");
PrintWriter pw = new PrintWriter(fos);
```

#### 2. Examples

```java
package filesAndIo.byteStreams;

import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.PrintWriter;

public class PrintStreamClasses {

    public static void main(String[] args) {
        try {
            FileOutputStream fos = new FileOutputStream("/Users/petter/test/testPrintStream.txt");
            PrintWriter pw = new PrintWriter(fos);
            pw.print(Integer.MAX_VALUE);
            pw.print('c');
            pw.print(123.123);
            pw.flush();
            fos.close();
            pw.close();
        } catch (IOException e) {
            e.printStackTrace();
        }


    }
}

```