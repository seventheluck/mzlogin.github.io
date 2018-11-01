---
layout: post
title: Java I/O - 17 FileWriter
categories: Java
description: Java I/O - 17 FileWriter
keywords: Java, I/O
---

#### 1. Constructor
```java
File file = new File("/Users/petter/test/testCharacterArrayWriter.txt");
FileReader fr = new FileReader(file);
```

#### 2. Examples

```java
package filesAndIo.characterStreams;

import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

public class FileReaderClasses {

    public static void main(String[] args) {
        File file = new File("/Users/petter/test/testCharacterArrayWriter.txt");
        try {
            FileReader fr = new FileReader(file);
            int c = fr.read();
            while (c != -1) {
                System.out.print((char) c);
                c = fr.read();
            }
            fr.close();
        } catch (IOException e) {
            e.printStackTrace();
        }

    }
}


```