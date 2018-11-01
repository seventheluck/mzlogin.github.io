---
layout: post
title: Java I/O - 15 CharArrayWriter
categories: Java
description: Java I/O - 15 CharArrayWriter
keywords: Java, I/O
---

#### 1. Constructor
```java
char[] chars = {'a', 'b', 'c'};
CharArrayWriter caw = new CharArrayWriter();
caw.write(chars);
```

#### 2. Examples

```java
package filesAndIo.characterStreams;

import java.io.CharArrayWriter;
import java.io.FileWriter;
import java.io.IOException;

public class CharArrayWriterClasses {

    public static void main(String[] args) {
        char[] chars = {'a', 'b', 'c'};
        CharArrayWriter caw = new CharArrayWriter();
        for (int i = 0; i < chars.length; i++) {
            caw.write(chars[i]);
        }
        try {
            caw.write(chars);
        } catch (IOException e) {
            e.printStackTrace();
        }
        try {
            FileWriter fw = new FileWriter("/Users/petter/test/testCharacterArrayWriter.txt");
            caw.writeTo(fw);
            caw.flush();
            caw.close();
            fw.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```