layout: post
title: Java I/O - 02 FileInputStream
categories: Java
description: Java I/O - 02 FileInputStream
keywords: Java, I/O


FileInputStream class: subclass of InputStream abstract class. 
create an input stream, used to read byte/bytes from a file. 

1. Constructors :

A. FileInputStream(File file)
```java
    File file= new File("D:\\Textbook.txt");
    FileInputStream fis= new FileInputStream(file);
```
 

B. FileInputStream(String path)
```java
    FileInputStream fis= new FileInputStream("D:\\TextBook.txt");
```

```java
    public static void main(String... ar) throws IOException {
        try {
            FileInputStream fin = new FileInputStream("D:\\TextBook.txt");
            int c;
            while ((c = fin.read()) != -1)//Readingonebyteoutofafile
            {
                System.out.print((char) c);//castingbytetocharfordisplayingonthescreenusing,System.out
            }
            fin.close();
        } catch (IOException e) {
            System.out.println(e);
        }
    }
```

Reading a whole byte array out of a file using read(byte[] b) method.

```java
    public static void main(String... ar) throws IOException {
        try {
            FileInputStream fin = new FileInputStream("D:\\TextBook.txt");
            int c;
            while ((c = fin.read()) != -1)//Readingonebyteoutofafile
            {
                System.out.print((char) c);//castingbytetocharfordisplayingonthescreenusing,System.out
            }
            fin.close();
        } catch (IOException e) {
            System.out.println(e);
        }
    }
```