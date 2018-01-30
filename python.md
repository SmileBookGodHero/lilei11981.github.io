## Python教程
-----

### Python基础

* 数据类型和变量
    * 整数：1，100，-2，0，0xff00（十六进制数），0xa5b4c3d2 (十六进制数)
    * 浮点数：1.23，3.14，-9.01，1.23e5（123000），1.2e-5(0.000012)
    * 字符串：'abc'，"xyz"
    * 布尔值：True、False
    * 空值：NONE
    * 变量：变量名必须是大小写英文、数字和```_```的组合，且不能用数字开头
    * 常量：PI = 3.14159265359

* 字符串和编码
    * 字符编码
    * Python的字符串
    
    > 对于单个字符的编码，Python提供了ord()函数获取字符的整数表示，chr()函数把编码转换为对应的字符：
    
    ``` bash
    >>> ord('A')
    65
    >>> ord('中')
    20013
    >>> chr(66)
    'B'
    >>> chr(25991)
    '文'
    ```
    
    > 以Unicode表示的str，通过encode()方法可以编码为指定的bytes，要把bytes变为str，就需要用decode()方法：
    
    ``` bash
    >>> '中文'.encode('utf-8')
    b'\xe4\xb8\xad\xe6\x96\x87'
    >>> b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
    '中文'
    ```
    
    > len()函数计算的是str的字符数，如果换成bytes，len()函数就计算字节数，1个中文字符经过UTF-8编码后通常会占用3个字节，而1个英文字符只占用1个字节，在操作字符串时，我们经常遇到`str`和`bytes`的互相转换。为了避免乱码问题，应当始终坚持使用UTF-8编码对`str`和`bytes`进行转换。
    
    ``` bash
    >>> len(b'ABC')
    3
    >>> len(b'\xe4\xb8\xad\xe6\x96\x87')
    6
    >>> len('中文'.encode('utf-8'))
    6
    ```
    
    > 由于Python源代码也是一个文本文件，所以，当你的源代码中包含中文的时候，在保存源代码时，就需要务必指定保存为UTF-8编码。当Python解释器读取源代码时，为了让它按UTF-8编码读取，我们通常在文件开头写上这两行：
    
    ``` bash
    #!/usr/bin/env python3
    # -*- coding: utf-8 -*-
    ```
    
    > 第一行注释是为了告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略这个注释；
    > 第二行注释是为了告诉Python解释器，按照UTF-8编码读取源代码，否则，你在源代码中写的中文输出可能会有乱码。

    * 格式化
    > 在Python中，采用的格式化方式和C语言是一致的，用%实现，举例如下：
    
    ``` bash
    >>> 'Hello, %s' % 'world'
    'Hello, world'
    >>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
    'Hi, Michael, you have $1000000.'
    ```

* 使用list和tuple
    * list
    
    > Python内置的一种数据类型是列表：list。list是一种有序的集合，可以随时添加和删除其中的元素。
    
    ``` bash
    >>> classmates = ['Michael', 'Bob', 'Tracy']
    >>> classmates
    ['Michael', 'Bob', 'Tracy']
    ```
    
    > len() 获得list元素的个数
    > 追加元素到末尾
    
    ``` bash
    >>> classmates.append('Adam')
    >>> classmates
    ['Michael', 'Bob', 'Tracy', 'Adam']
    ```
    
    > 插入元素到指定位置
    
    ``` bash
    >>> classmates.insert(1, 'Jack')
    >>> classmates
    ['Michael', 'Jack', 'Bob', 'Tracy', 'Adam']
    ```
    
    > 删除list末尾的元素
    
    ``` bash
    >>> classmates.pop()
    'Adam'
    >>> classmates
    ['Michael', 'Jack', 'Bob', 'Tracy']
    ```
    
    > 删除指定位置的元素
    
    ``` bash
    >>> classmates.pop(1)
    'Jack'
    >>> classmates
    ['Michael', 'Bob', 'Tracy']
    ```
    
    > 替换指定位置元素
    
    ``` bash
    >>> classmates[1] = 'Sarah'
    >>> classmates
    ['Michael', 'Sarah', 'Tracy']
    ```
    
    > list里面的元素的数据类型也可以不同
    
    ``` bash
    >>> L = ['Apple', 123, True]
    ```
    
    > list元素也可以是另一个list
    
    ``` bash
    >>> s = ['python', 'java', ['asp', 'php'], 'scheme']
    >>> len(s)
    4
    ```

* 条件判断

* 循环

* 使用dict和set

### 函数
* 调用函数
* 定义函数
* 函数的参数
* 递归函数

### 高级特性
* 切片
* 迭代
* 列表生成式
* 生成器
* 迭代器

### 函数式编程
* 高阶函数
* 返回函数
* 匿名函数
* 装饰器
* 偏函数

### 模块
* 使用模块
* 安装第三方模块

### 面向对象编程
* 类和实例
* 访问限制
* 继承和多态
* 获取对象信息
* 实例属性和类属性

### 面向对象高级编程
* 使用```_slots_```
* 使用@property
* 多重继承
* 定制类
* 使用枚举类
* 使用元类

### 错误、调试和测试
* 错误处理
* 调试
* 单元测试
* 文档测试

### IO
* 文件读写
* StringIO和BytesIO
* 操作文件和目录
* 序列化

### 进程和线程
* 多进程
* 多线程
* ThreadLocal
* 进程 vs. 线程
* 分布式进程

### 正则表达式

### 常用内建模块
* datetime
* collections
* base64
* struct
* hashlib
* hmac
* itertools
* contextlib
* urllib
* XML
* HTMLParser

### 常用第三方模块
* Pillow
* requests
* chardet
* psutil

### virtualenv

### 图形界面

### 网络编程
* TCP/IP
* TCP编程
* UDP编程

### 电子邮件
* SMTP发送邮件
* POP3收发邮件

### 访问数据库
* 使用SQLite
* 使用MySQL
* 使用SQLAlchemy

### Web开发
* HTTP协议简介
* HTML简介
* WSGL接口
* 使用Web框架
* 使用模板

### 异步IO
* 协程
* asyncio
* async/await
* aiohttp

### 实战