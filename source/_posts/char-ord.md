---
title: 字符与编码
date: 2017-05-13 14:45:01
tags: python
categories: techn
---
## 字符与编码
### 计算机中的编码
   原本各国有各国不同的编码标准，标准不同就会产生冲突，在多语言混合的文本中显示出来就会有乱码。所以产生了Unicode。

   Unicode是把所有语言统一到一套编码里，但所有内容全部用Unicode编码的话，会有很多的空间浪费。所以产生了可变长编码的UTF-8编码。

   UTF-8把一个Unicode字符根据不同的数字大小编码成1-6个字节，常用的英文字母被编码成1个字节，汉字通常为3个字节，生僻的字符才会被编码成4-6个字节。<!-- more -->

### 计算机系统通用的字符编码工作方式
   在计算机内存中使用Unicode编码，当需要保存到硬盘或者需要传输时，就转换为UTF-8编码

   在显示时，文件会以Unicode的形式显示（使用记事本编辑时）

   在存储时，文件会以UTF-8的形式存储于硬盘

   在浏览网页时，服务器会把动态生成的Unicode内容转换为UTF-8再传输到浏览器

### python的字符串
  对于单个字符的编码，有ord()函数获取字符的整数表示，chr()函数把编码转换为对应的字符

    >>> ord('A')
    65
    >>> ord('中')
    20013
    >>>chr(66)
    'B'
    >>>chr(255991)
    '文'

  python 的字符串类型是str，如果在网络上传输或者保存到磁盘上，就需要把str变为以字节为单位的bytes(bytes中每个字符都只占用一个字节)
  python 对bytes类型的数据用带b前缀的单引号或双引号表示

       x = b'ABC'

   以Unicode表示的str通过encode()方法可以编码为指定的bytes， 例如

     >>> 'ABC'.encode('ascii')
     b'ABC'
     >>> '中文'.encode('utf-8')
     b'\xe4\xb8\xad\xe6\x96\x87'
     >>> '中文'.encode('ascii')
     Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     UnicodeEncodeError: 'ascii' codec can't encode characters in position 0-1: ordinal not in range(128)

   如果要把bytes变为str，就需要用decode()方法：

     >>> b'ABC'.decode('ascii')
     >>> ABC'

   len()函数计算的是str的字符数，若换成bytes，len()函数就计算字节数：

     >>> len(b'ABC')
     >>> 3
     >>> len('中文'.encode('utf-8'))
     >>> 6

   当源代码中包含中文时，让保存源代码时，应务必指定保存为utf-8编码读取，我们通常在文件开头写上这两行：

     #!/usr/bin/env python3
     # -*- coding: utf-8 -*-
    
     第一行注释是为了告诉linux/OS X系统，这是一个python可执行程序，Windows会忽略这个注释；
     第二行注释是为了告诉python解释器，按照utf-8读取源代码，否则，源代码中的中文输出可能有乱码

### 格式化
输出格式化的字符串。
    
     “亲爱的XXX你好！你XX月的话费是XX，余额是XX”

   xxx是根据变量变化的，所以，需要一种简便的格式化字符串的方式
   python中与c语言一致，用%实现

     >>> 'Hello,%s' %'world'
     'Hello,world'
     >>> 'Hi,%s,you have $%d.' % ('Michael',1000000)
     'Hi,Michael,you have $1000000.'

   常见的占位符有：

|占位符|意义|
|--|--|
|%d|整数|
|%f|浮点数|
|%s|字符串|
|%x|十六进制整数|

   在不确定用什么的情况下，**%s**永远起作用。
   可以把任何数据类型转换为字符串。

     >>> 'Age: %s. Gender: %s' % (25,True)
     'Age: 25. Gender: True'

   其中，格式化整数和浮点数还可以指定是否补0和整数与小数的位数

     >>> '%2d-%02d' % (3,4)
     ' 3-04'
     2代表位数为两位，添了0代表前面补0.
    
     >>> '%03d - %003d' % (3,4)
     '003 - 004'

   如果原本字符串里就有%，则需要转义，用%%表示一个%：
     >>> 'growth rate: %d %%'%7
     'growth rate: 7 %'
