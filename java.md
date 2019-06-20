## java

------

### 基本语法


```java
public class Demo {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```





### java8 新特性 Base64

```java
public class Base64Class {
    public static void main(String[] args) {
        try {
            // 使用基本编码
            String base64encodedString = Base64.getEncoder().encodeToString("java8Base64".getBytes("utf-8"));
            System.out.println("Base64 编码字符串 (基本) :" + base64encodedString);
            // 解码
            byte[] base64decodedBytes = Base64.getDecoder().decode(base64encodedString);
            System.out.println("原始字符串: " + new String(base64decodedBytes, "utf-8"));

            base64encodedString = Base64.getUrlEncoder().encodeToString("TutorialsPoint?java8".getBytes("utf-8"));
            System.out.println("Base64 编码字符串 (URL) :" + base64encodedString);

            StringBuilder stringBuilder = new StringBuilder();

            for (int i = 0; i < 10; ++i) {
                stringBuilder.append(UUID.randomUUID().toString());
            }

            byte[] mimeBytes = stringBuilder.toString().getBytes("utf-8");
            String mimeEncodedString = Base64.getMimeEncoder().encodeToString(mimeBytes);
            System.out.println("Base64 编码字符串 (MIME) :" + mimeEncodedString);

        } catch (UnsupportedEncodingException e) {
            System.out.println("Error :" + e.getMessage());
        }
    }
}
```



#### 面向对象

*   类与对象


#### IO简介
> 输入与输出，基本功能是读和写

##### IO流
> 作用：读写设备上的数据，硬盘文件、内存、键盘、网络……

* 根据数据的走向，可分为：输入流、输出流
* 根据处理的数据类型，可分为：字节流、字符流

##### 字节流与字符流

* **字节流**可以处理所有类型的数据，如MP3、图片、文字、视频等。在读取时，读到一个字节就返回一个字节。

> 在Java中对应的类都以“Stream”结尾。

* **字符流**仅能处理纯文本数据，如txt文本等。在读取时，读到一个或者多个字节，先查找指定的编码表，然后将查到的字符返回。

> 在Java中对应的类都以“Reader”或“Writer”结尾。

##### 字节(Byte)
> 字节是通过网络传输信息或在硬盘或内存中存储信息的单位，是计算机信息技术用于计量存储容量和传输容量的一种计量单位。

> 一个字节等于8位二进制，即一个8位的二进制数，是一个很具体的存储空间。

> 0x01，0x45，0xFA，……

##### 字符(Char)
> 字符是人们使用的记号，抽象意义上的一个符号。

> 如‘1’，'中’，‘a’，‘￥’，‘$’，……