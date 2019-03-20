##### Java的IO流

- 流是对输入输出设备的抽象，对于程序而言输入输出需要借助流
- 字节流（バイトストリーム）
  - 传输过程中，传输数据的最基本单位是字节的流
- 字符流（文字ストリーム）
  - 字符流--传输过程中，传输数据的最基本单位是字符的流。
- 字符编码方式不同，有时候一个字符使用的字节数也不一样，比如ASCLL方式编码的字符，占一个字节；而UTF-8方式编码的字符，一个英文字符需要一个字节，一个中文需要三个字节。
- 字节数据是二进制形式的，要转成我们能识别的正常字符，需要选择正确的编码方式。生活中的乱码问题就是字节数据没有选择正确的编码方式来显示成字符。
- 从本质上来讲，写数据（即输出）的时候，字节也好，字符也好，本质上都是没有标识符的，需要去指定编码方式。
在传输方面上，由于计算机的传输本质都是字节，而一个字符由多个字节组成，转成字节之前先要去查表转成字节，所以传输时有时候会使用缓冲区。

- 常用函数

|字节输入流|字节输出流|
|:-|:-|
|InputStream|OutputStream|
|FileInputStream|FileOutputStream|
|BufferedInputStream|BufferedOutputStream|

|字符输入流|字符输出流|
|:-|:-|
|Reader|Writer|
|InputStreamReader|OutputStreamWriter|
|FileReader|FileWriter|
|BufferedReader|BufferedWriter|


- FileReader，FileInputStream，InputStreamReader的read方法，每次调用的时候都会访问文件，效率不够理想。
- BufferedReader，BufferedInputStream的read方法，每次调用的时候都会把数据读入缓冲buffer，然后从缓冲区读取数据，缓冲区没数据了才会再度访问文件，overhead也比较少。write同理。

参考
- https://www.cnblogs.com/progor/p/9357676.html
- http://www.javaroad.jp/java_io1.htm
- http://www.javaroad.jp/java_io4.htm
