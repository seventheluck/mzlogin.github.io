---
layout: post
title: Java IO方法总结
categories: Java
description: Java IO方法总结
keywords: Java, IO
---
```java
package javaIO;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.io.RandomAccessFile;

public class CreatNewFile {
	
	private static String filePath = File.separator + "Users" + File.separator + "wenchaoma" + File.separator + "Documents"
			+ File.separator + "JavaIO";//+ File.separator + "JavaIO"
	private static String fileName = "hello.txt";

	public static void main(String[] args) throws IOException {
		// TODO Auto-generated method stub
		//creatFileAndPath();
		//deleteFile();
		//listFiles();
		//listFilesAndDirectories();
		//isDirectory();
		//String filePath = File.separator + "Users" + File.separator + "wenchaoma" + File.separator + "Documents";
		//File directory = new File(filePath);
		//findAllFiles(directory);
		//writeFile();
		//writeFileWithOutputStream();
		//writeFileWithOutputStreamByByte();
		//addInfoToFile();
		//readFile();
		//writerToFileInString();
		readFromFileInString();
	}
	
	/*创建文件
	 * 
	 * 
	 * */
	public static void creatFileAndPath() {
		
		// If the directory does not exit, the program will throw "java.io.IOException:
		// No such file or directory"
		System.out.println(File.pathSeparator);;
		File file = new File(filePath + File.separator + fileName);

		try {
			file.createNewFile();
		} catch (Exception e) {
			e.printStackTrace();
			
			try {
				File directory = new File(filePath);
				directory.mkdirs();
			}catch (Exception e1) {
				e1.printStackTrace();
			}
			
		}
	}

	/*删除文件
	 * 
	 * 
	 * */
	public static void deleteFile() {
		File file = new File(filePath + File.separator + fileName);
		if(file.exists()) {
			try {
				file.delete();
				System.out.println("Success to delete the file!");
			}catch (Exception e) {
				System.out.println("Fail to delete the file!");
				e.printStackTrace();
			}
			
			
		}else {
			System.out.println("File not exist!");
		}
	}
	
	/*列出指定目录下所有的文件
	 * 
	 * 
	 * */
	public static void listFiles() {
		String filePath = File.separator + "Users" + File.separator + "wenchaoma" + File.separator + "Documents";
		File directory = new File(filePath);
		String[] list = directory.list();
		for(String i : list) {
			System.out.println(i);
		}

	}

	/*列出指定目录下所有文件的路径
	 * 
	 * 
	 * */
	public static void listFilesAndDirectories() {
		String filePath = File.separator + "Users" + File.separator + "wenchaoma" + File.separator + "Documents";
		File directory = new File(filePath);
		File[] fileList = directory.listFiles();
		for(File i : fileList) {
			System.out.println(i);
		}
	}
	
	/*判断是否为目录
	 * 
	 * 
	 * */
	public static void isDirectory() {
		String filePath = File.separator + "Users" + File.separator + "wenchaoma" + File.separator + "Documents";
		File directory = new File(filePath);
		if(directory.isDirectory()) {
			System.out.println("Yes");
		}else {
			System.out.println("No");
		}
	}
	
	/*查询并列出指定目录下所有的文件
	 * 
	 * 
	 * */
	public static void findAllFiles(File directory) {
		if(directory != null) {
			if(directory.isDirectory()) {
				//列出目录下所有的文件
				File[] list = directory.listFiles();
				for(File i : list) {
					findAllFiles(i);
				}
			}else {
				System.out.println(directory);
			}
		}
		
	}

	/*向文件中写入字符串
	 * 
	 * 
	 * */
	public static void writeFile() {
		File file = new File(filePath + File.separator + fileName);
		try {
			RandomAccessFile ranfile = new RandomAccessFile(file,"rw");
			String hao = "好";
			ranfile.writeBytes("Hello");
			ranfile.writeInt(123);
			ranfile.writeByte('A');
			ranfile.write(hao.getBytes());
			ranfile.write("好".getBytes());
			ranfile.close();
		}catch (Exception e) {
			e.printStackTrace();
		}
		
		
	}

	/*字节流【向文件中写入字符串】
	 *
	 *
	 */
	public static void writeFileWithOutputStream() throws IOException {
		File file = new File(filePath + File.separator + fileName);
		try {
			FileOutputStream os = new FileOutputStream(file);
			byte[] fileByte = "大家好!!!!".getBytes();
			os.write(fileByte);
			os.close();
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
	}
	/*字节流【向文件中写入字符串】
	 *
	 *
	 */
	public static void writeFileWithOutputStreamByByte() throws IOException {
		File file = new File(filePath + File.separator + fileName);
		try {
			FileOutputStream os = new FileOutputStream(file);
			byte[] fileByte = "大家好123123!!!!".getBytes();
			for(byte i : fileByte) {
				os.write(i);
			}
			os.close();
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
	}
	
	/*字节流 向文件中追加新内容：
	 * 
	 * 
	 * */
	public static void addInfoToFile() throws IOException {
		File file = new File(filePath + File.separator + fileName);
		try {
			FileOutputStream os = new FileOutputStream(file, true);
			byte[] fileByte = "nihao你好啊123123".getBytes();
			os.write(fileByte);
			os.close();
		}catch(FileNotFoundException e) {
			e.printStackTrace();
		}
	}

	/*字节流 读取文件内容
	 * 
	 * 
	 * */
	public static void readFile() throws IOException {
		File file = new File(filePath + File.separator + fileName);
		try {
			//读取方法1:
			FileInputStream io = new FileInputStream(file);
			byte[] fileBytes = new byte[(int)file.length()];
			io.read(fileBytes);
			io.close();
			System.out.println(new String(fileBytes));
			
			//读取方法2:
			FileInputStream io1 = new FileInputStream(file);
			byte[] fileB = new byte[(int) file.length()];
			for(int i = 0; i < fileB.length; i++) {
				fileB[i] = (byte) io1.read();
				
			}
			io1.close();
			System.out.println(new String(fileB));
			
			//读取方法3:
			FileInputStream io2 = new FileInputStream(file);
			byte[] fileBb = new byte[1024];
			int i = 0;
			while(true) {
				
				int temp = io2.read();
				if(temp == -1)
					break;
				fileBb[i] = (byte) temp;
				i++;
			}
			io2.close();
			System.out.println(new String(fileBb));
			
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
	}
	
	/*字符流 【向文件中写入字符串】
	 * 
	 * 
	 * */
	public static void writerToFileInString() throws IOException {
		File file = new File(filePath + File.separator + fileName);
		FileWriter ow = new FileWriter(file);
		String writer = "你好啊，哈哈哈！！！";
		ow.write(writer);
		ow.close();
	}
	/*字符流 【从文件中读入字符串】
	 * 
	 * 
	 * */
	public static void readFromFileInString() throws IOException {
		File file = new File(filePath + File.separator + fileName);
		//读取方法1：
		FileReader ir = new FileReader(file);
		char[] ch = new char[(int) file.length()];
		ir.read(ch);
		ir.close();
		System.out.println(ch);
		//读取方法2：
		FileReader ir1 = new FileReader(file);
		char[] ch1 = new char[(int) file.length()];
		int i;
		for(i = 0; i < ch1.length; i++) {
			int temp = ir1.read();
			if(temp == -1)
				break;
			ch1[i] = (char) temp;
		}
		ir1.close();
		System.out.println(new String(ch1,0,i));
	}
	
}

```
关于字节流和字符流的区别
实际上字节流在操作的时候本身是不会用到缓冲区的，是文件本身的直接操作的，但是字符流在操作的 时候下后是会用到缓冲区的，是通过缓冲区来操作文件的。

读者可以试着将上面的字节流和字符流的程序的最后一行关闭文件的代码注释掉，然后运行程序看看。你就会发现使用字节流的话，文件中已经存在内容，但是使用字符流的时候，文件中还是没有内容的，这个时候就要刷新缓冲区。

Reader 类是 Java 的 I/O 中读字符的父类，而 InputStream 类是读字节的父类，InputStreamReader 类就是关联字节到字符的桥梁，它负责在 I/O 过程中处理读取字节到字符的转换，而具体字节到字符的解码实现它由 StreamDecoder 去实现，在 StreamDecoder 解码过程中必须由用户指定 Charset 编码格式。值得注意的是如果你没有指定 Charset，将使用本地环境中的默认字符集，例如在中文环境中将使用 GBK 编码。
写的情况也是类似，字符的父类是 Writer，字节的父类是 OutputStream，通过 OutputStreamWriter 转换字符到字节。同样 StreamEncoder 类负责将字符编码成字节，编码格式和默认编码规则与解码是一致的。

### public abstract class Reader
extends Object
implements Readable, Closeable
Abstract class for reading character streams. The only methods that a subclass must implement are read(char[], int, int) and close(). Most subclasses, however, will override some of the methods defined here in order to provide higher efficiency, additional functionality, or both.

### public abstract class InputStream
extends Object
implements Closeable
This abstract class is the superclass of all classes representing an input stream of bytes.
Applications that need to define a subclass of InputStream must always provide a method that returns the next byte of input.

### public class InputStreamReader
extends Reader
An InputStreamReader is a bridge from byte streams to character streams: It reads bytes and decodes them into characters using a specified charset. The charset that it uses may be specified by name or may be given explicitly, or the platform's default charset may be accepted.
Each invocation of one of an InputStreamReader's read() methods may cause one or more bytes to be read from the underlying byte-input stream. To enable the efficient conversion of bytes to characters, more bytes may be read ahead from the underlying stream than are necessary to satisfy the current read operation.

For top efficiency, consider wrapping an InputStreamReader within a BufferedReader. For example:

 BufferedReader in
   = new BufferedReader(new InputStreamReader(System.in));
