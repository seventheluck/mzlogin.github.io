---
layout: post
title: Java I/O - 18 BufferedReader
categories: Java
description: Java I/O - 18 BufferedReader
keywords: Java, I/O
---

#### 1. Constructor
```java
File file = new File("/Users/petter/test/testFileWriter.txt");
FileReader fr = new FileReader(file);
BufferedReader br = new BufferedReader(fr);
```

#### 2. Examples

```java
package filesAndIo.characterStreams;

import java.io.*;

public class BufferedReaderClasses {

    public static void main(String[] args) {
        File file = new File("/Users/petter/test/testFileWriter.txt");

        try {
            FileReader fr = new FileReader(file);
            BufferedReader br = new BufferedReader(fr);
            int c = br.read();
            while (c != -1) {
                System.out.print((char) c);
                c = br.read();
            }
            fr.close();
            br.close();
        } catch (IOException e) {
            e.printStackTrace();
        }


    }
}


```