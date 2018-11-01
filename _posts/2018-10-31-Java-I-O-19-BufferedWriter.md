---
layout: post
title: Java I/O - 19 BufferedWriter
categories: Java
description: Java I/O - 19 BufferedWriter
keywords: Java, I/O
---

#### 1. Constructor
```java
File file = new File("/Users/petter/test/testFileWriter.txt");
FileWriter fw = new FileWriter(file);
BufferedWriter bw = new BufferedWriter(fw);
```

#### 2. Examples

```java
package filesAndIo.characterStreams;

import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;

public class BufferedWriterClasses {

    public static void main(String[] args) {
        File file = new File("/Users/petter/test/testFileWriter.txt");
        try {
            FileWriter fw = new FileWriter(file);
            BufferedWriter bw = new BufferedWriter(fw);
            bw.write("This is a test for BufferedWriter!");
            bw.flush();
            fw.flush();
            fw.close();
            bw.close();
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}

```