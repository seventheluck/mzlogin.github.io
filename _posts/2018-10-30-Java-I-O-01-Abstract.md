# Java I/O - 01 Abstract

标签（空格分隔）： Java

---

### Summary:
Direction: **Input stream** & **Output stream**.
Type of data: **Byte Stream Classes** & **Character Stream Classes**.
#### 1. Byte Stream Classes
Read bytes from an input stream and write bytes to an output stream.
##### A. InputStream 
![此处输入图片的描述][1]
InputStream class is a base class of all the classes that are used to read bytes from a file, memory or console. InputStream is an abstract class and hence we can't create its object but we can use its subclasses for reading bytes from the input stream. 
##### B. OutputStream
![此处输入图片的描述][2]
OutputStream class is a base class of all the classes that are used to write bytes to a file, memory or console. OutputStream is an abstract class and hence we can't create its object but we can use its subclasses for writing bytes to the output stream. In the diagram below we have shown the hierarchy of OutputStream class and some of its important subclasses that are used to write bytes.
#### 2. Character Stream Classes
Used to read characters from the source and write characters to destination.
two kinds of Character Stream classes - Reader classes and Writer classes. 
##### A. Reader
![此处输入图片的描述][3]
Reader class and its subclasses are used to read characters from source. 
Reader class is a base class of all the classes that are used to read characters from a file, memory or console. Reader is an abstract class and hence we can't instantiate it but we can use its subclasses for reading characters from the input stream. We will discuss subclasses of Reader class with their code, in the next few articles. 
##### B. Writer
![此处输入图片的描述][4]
	Writer class and its subclasses are used to write characters to a file, memory or console. Writer is an abstract class and hence we can't create its object but we can use its subclasses for writing characters to the output stream. We will discuss subclasses of Writer with their code in the next few articles. 
	


  [1]: https://upload-images.jianshu.io/upload_images/2946710-9c0829482d92f090.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700/format/webp
  [2]: https://upload-images.jianshu.io/upload_images/2946710-12329993682fdbcb.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700/format/webp
  [3]: https://upload-images.jianshu.io/upload_images/2946710-039ec2e730834878.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700/format/webp
  [4]: https://upload-images.jianshu.io/upload_images/2946710-7bafd3d7560c123b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700/format/webp
