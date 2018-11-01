---
layout: post
title: Java I/O - 13 OutputStreamWriter
categories: Java
description: Java I/O - 13 OutputStreamWriter
keywords: Java, I/O
---

#### 1. Constructor
```java
FileOutputStream fos = new FileOutputStream("/Users/petter/test/testOutputStreamReader.txt");
OutputStreamWriter osw = new OutputStreamWriter(fos);
```

#### 2. Examples

```java
package filesAndIo.characterStreams;

import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStreamWriter;

public class OutputStreamWriterClasses {

    public static void main(String[] args) {
        try {
            FileOutputStream fos = new FileOutputStream("/Users/petter/test/testOutputStreamReader.txt");
            OutputStreamWriter osw = new OutputStreamWriter(fos);
            osw.write("This is a test for OutputStreamWriter!");
            osw.flush();
            fos.close();
            osw.close();
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}


```