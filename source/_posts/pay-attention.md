---
title: py注意(廖雪峰)
date: 2017-08-15 23:25:50
tags: python
categories: python
---
1.判断是否为可迭代的对象
    from collections import Iterable
    isinstance('abc',Iterable)
2.判断变量是否为字符串isinstance(变量，str)
3.python 3 还用不成 MySQL for python，只能用pymysql

    pip install pymysql (python3.4不支持，3.6可以)

