# python
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

    * tuple

    > 另一种有序列表叫元组：tuple。tuple和list非常类似，但是tuple一旦初始化就不能修改

    ``` python
    >>> classmates = ('Michael', 'Bob', 'Tracy')
    ```

    > classmates这个tuple不能变了，它也没有append()，insert()这样的方法。其他获取元素的方法和list是一样的，你可以正常地使用classmates[0]，classmates[-1]，但不能赋值成另外的元素。
    > tuple的陷阱：当你定义一个tuple时，在定义的时候，tuple的元素就必须被确定下来,只有1个元素的tuple定义时必须加一个逗号`,`，来消除歧义

* 条件判断
    > 计算机之所以能做很多自动化的任务，因为它可以自己做条件判断。

    ``` python
    age = 3
    if age >= 18:
        print('your age is', age)
        print('adult')
    elif age >= 6:
        print('your age is', age)
        print('teenager')
    else:
        print('your age is', age)
        print('kid')
    ```

    > 使用input()读取用户输入

    ``` python
    s = input('birth: ')
    birth = int(s)
    if birth < 2000:
        print('00前')
    else:
        print('00后')
    ```

* 循环
    * 循环

    > Python的循环有两种，一种是for...in循环，依次把list或tuple中的每个元素迭代出来

    ``` python
    names = ['Michael', 'Bob', 'Tracy']
    for name in names:
        print(name)
    ```

    > 计算1-100的整数之和

    ``` python
    # -*- coding: utf-8 -*-
    sum = 0
    for x in range(101):
        sum = sum + x
    print(sum)
    ```

    > 第二种循环是while循环，只要条件满足，就不断循环，条件不满足时退出循环。比如我们要计算100以内所有奇数之和，可以用while循环实现：

    ``` python
    sum = 0
    n = 99
    while n > 0:
        sum = sum + n
        n = n - 2
    print(sum)
    ```

    * break

    > 在循环中，break语句可以提前退出循环

    ``` python
    n = 1
    while n <= 100:
        if n > 10: # 当n = 11时，条件满足，执行break语句
            break # break语句会结束当前循环
        print(n)
        n = n + 1
    print('END') # 打印出1~10后，紧接着打印END
    ```

    * continue

    > 在循环过程中，也可以通过continue语句，跳过当前的这次循环，直接开始下一次循环

    ``` python
    n = 0
    while n < 10:
        n = n + 1
        if n % 2 == 0: # 如果n是偶数，执行continue语句
            continue # continue语句会直接继续下一轮循环，后续的print()语句不会执行
        print(n) # 1 3 5 7 9
    ```

* 使用dict和set
    * dict

    > Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。

    ``` python
    >>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
    >>> d['Michael']
    95
    ```

    > dict内部存放的顺序和key放入的顺序是没有关系的

    * set

    > set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。

    * 不可变对象

    ``` python
    >>> a = 'abc'
    >>> b = a.replace('a', 'A')
    >>> b
    'Abc'
    >>> a
    'abc'
    ```

    > 当我们调用a.replace('a', 'A')时，实际上调用方法replace是作用在字符串对象'abc'上的，而这个方法虽然名字叫replace，但却没有改变字符串'abc'的内容。相反，replace方法创建了一个新字符串'Abc'并返回，如果我们用变量b指向该新字符串，就容易理解了，变量a仍指向原有的字符串'abc'，但变量b却指向新字符串'Abc'了


### 函数
* 调用函数
    * 内置函数

    ``` python
    >>> abs(100)
    100
    >>> abs(-20)
    20
    >>> abs(12.34)
    12.34
    >>> max(1, 2)
    2
    >>> max(2, 3, 1, -5)
    3
    ```

    * 数据类型转换

    ``` python
    >>> int('123')
    123
    >>> int(12.34)
    12
    >>> float('12.34')
    12.34
    >>> str(1.23)
    '1.23'
    >>> str(100)
    '100'
    >>> bool(1)
    True
    >>> bool('')
    False
    ```

* 定义函数
    * 定义函数

    > 在Python中，定义一个函数要使用def语句，依次写出函数名、括号、括号中的参数和冒号:，然后，在缩进块中编写函数体，函数的返回值用return语句返回。

    > 自定义一个求绝对值的my_abs函数

    ``` python
    # -*- coding: utf-8 -*-
    def my_abs(x):
    if x >= 0:
        return x
    else:
        return -x
    ```

    > 请注意，函数体内部的语句在执行时，一旦执行到return时，函数就执行完毕，并将结果返回。因此，函数内部通过条件判断和循环可以实现非常复杂的逻辑。
    
    > 如果没有return语句，函数执行完毕后也会返回结果，只是结果为None。return None可以简写为return。
    
    > 如果你已经把my_abs()的函数定义保存为abstest.py文件了，那么，可以在该文件的当前目录下启动Python解释器，用from abstest import my_abs来导入my_abs()函数，注意abstest是文件名（不含.py扩展名）

    * 空函数

    > 如果想定义一个什么事也不做的空函数，可以用pass语句：

    ``` python
    def nop():
    pass
    ```

    > 实际上pass可以用来作为占位符，比如现在还没想好怎么写函数的代码，就可以先放一个pass，让代码能运行起来。

    * 参数检查

    > 调用函数时，如果参数个数不对，Python解释器会自动检查出来，并抛出TypeError

    * 返回多个值

    ``` python
    import math

    def move(x, y, step, angle=0):
        nx = x + step * math.cos(angle)
        ny = y - step * math.sin(angle)
        return nx, ny
    ```
    
    ``` python
    >>> r = move(100, 100, 60, math.pi / 6)
    >>> print(r)
    (151.96152422706632, 70.0)
    ```

    > 返回值是一个tuple！但是，在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值，所以，Python的函数返回多值其实就是返回一个tuple，但写起来更方便。

* 函数的参数
    > 定义函数的时候，我们把参数的名字和位置确定下来，函数的接口定义就完成了。对于函数的调用者来说，只需要知道如何传递正确的参数，以及函数将返回什么样的值就够了，函数内部的复杂逻辑被封装起来，调用者无需了解。
    
    > Python的函数定义非常简单，但灵活度却非常大。除了正常定义的必选参数外，还可以使用默认参数、可变参数和关键字参数，使得函数定义出来的接口，不但能处理复杂的参数，还可以简化调用者的代码。
    
    * 位置参数
    
    > 计算x的平方的函数
    
    ``` python
    def power(x):
        return x * x
    ```
    
    ``` python
    >>> power(5)
    25
    >>> power(15)
    225
    ```
    
    > 把power(x)修改为power(x, n)，用来计算x的n次幂
    
    ``` python
    def power(x, n):
        s = 1
        while n > 0:
            n = n - 1
            s = s * x
        return s
    ```
    
    ``` python
    >>> power(5, 2)
    25
    >>> power(5, 3)
    125
    ```
    
    > 修改后的power(x, n)函数有两个参数：x和n，这两个参数都是位置参数，调用函数时，传入的两个值按照位置顺序依次赋给参数x和n
    
    * 默认参数
    
    ``` python
    def power(x, n=2):
        s = 1
        while n > 0:
            n = n - 1
            s = s * x
        return s
    ```
    
    > 当我们调用power(5)时，相当于调用power(5, 2)
    
    > 必选参数在前，默认参数在后，否则Python的解释器会报错
    
    > 当函数有多个参数时，把变化大的参数放前面，变化小的参数放后面。变化小的参数就可以作为默认参数。

    > 默认参数降低了函数调用的难度，而一旦需要更复杂的调用时，又可以传递更多的参数来实现。无论是简单调用还是复杂调用，函数只需要定义一个。
    
    > 有多个默认参数时，调用的时候，既可以按顺序提供默认参数，也可以不按顺序提供部分默认参数。当不按顺序提供部分默认参数时，需要把参数名写上。
    
    
    ``` python
    def add_end(L=[]):
        L.append('END')
        return L
    ```
    
    > 正常调用
    
    ``` python
    >>> add_end([1, 2, 3])
    [1, 2, 3, 'END']
    >>> add_end(['x', 'y', 'z'])
    ['x', 'y', 'z', 'END']
    ```
    
    > 使用默认参数调用
    
    ``` python
    >>> add_end()
    ['END']
    >>> add_end()
    ['END', 'END']
    >>> add_end()
    ['END', 'END', 'END']
    ```
    
    > Python函数在定义的时候，默认参数L的值就被计算出来了，即[]，因为默认参数L也是一个变量，它指向对象[]，每次调用该函数，如果改变了L的内容，则下次调用时，默认参数的内容就变了，不再是函数定义时的[]了。
    
    > 定义默认参数要牢记一点：默认参数必须指向不变对象！
    
    ``` python
    def add_end(L=None):
        if L is None:
            L = []
        L.append('END')
        return L
    ```
    
    ``` python
    >>> add_end()
    ['END']
    >>> add_end()
    ['END']
    ```
    
    > 为什么要设计str、None这样的不变对象呢？因为不变对象一旦创建，对象内部的数据就不能修改，这样就减少了由于修改数据导致的错误。此外，由于对象不变，多任务环境下同时读取对象不需要加锁，同时读一点问题都没有。我们在编写程序时，如果可以设计一个不变对象，那就尽量设计成不变对象。
    
    * 可变参数
    
    > 在Python函数中，还可以定义可变参数。顾名思义，可变参数就是传入的参数个数是可变的，可以是1个、2个到任意个，还可以是0个
    
    > 我们以数学题为例子，给定一组数字a，b，c……，请计算a^2 + b^2 + c^2 + ……
    
    ``` python
    def calc(numbers):
        sum = 0
        for n in numbers:
            sum = sum + n * n
        return sum
    ```
    
    > 调用的时候可以组装出一个list或tuple
    
    ``` python
    >>> calc([1, 2, 3])
    14
    >>> calc((1, 3, 5, 7))
    84
    ```
    
    > 把参数改为可变参数
    
    ``` python
    def calc(*numbers):
        sum = 0
        for n in numbers:
            sum = sum + n * n
        return sum
    ```
    
    > 定义可变参数和定义一个list或tuple参数相比，仅仅在参数前面加了一个*号。在函数内部，参数numbers接收到的是一个tuple，因此，函数代码完全不变。但是，调用该函数时，可以传入任意个参数，包括0个参数：
    
    ``` python
    >>> calc(1, 2)
    5
    >>> calc()
    0
    ```
    
    * 关键字参数
    
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