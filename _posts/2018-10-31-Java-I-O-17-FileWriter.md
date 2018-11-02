---
layout: post
title: Java I/O - 17 FileWriter
categories: Java
description: Java I/O - 17 FileWriter
keywords: Java, I/O
---

#### 1. Constructor
```java
File file = new File("/Users/petter/test/testFileWriter.txt");
FileReader fr = new FileReader(file);
```

#### 2. Examples

```java
package filesAndIo.characterStreams;

import java.io.File;
import java.io.FileWriter;
import java.io.IOException;

public class FileWriterClasses {

    public static void main(String[] args) {
        File file = new File("/Users/petter/test/testFileWriter.txt");
        try {
            FileWriter fw = new FileWriter(file);
            String str = "This is a test for FileWriter!";
            fw.write(str);
            fw.flush();
            fw.close();
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}


```