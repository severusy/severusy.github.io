---
title: python中的回忆录
date: 2017-05-29 22:39:15
tags: python
categories: techn
---
1、L.append(n)
  把n添加到L中

2、range( )
  range()函数，给定范围，从0开始，range(5)相当于[0,5)

    L = list(range(100))

    0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99

3.判断是否为可迭代的对象
    from collections import Iterable
    isinstance('abc',Iterable)
4.判断变量是否为字符串isinstance(变量，str)
5.python 3 还用不成 MySQL for python，只能用pymysql

    pip install pymysql (python3.4不支持，3.6可以)

6.virtualenv(虚拟环境)
安装：

    pip3 install virtualenv

7.新建一套独立的Python运行环境
   1)创建目录myproject
   2)创建独立的python运行环境 venv
        virtualenv --no-site-packages venv
    (参数--no-site-packages：不要任何第三方包的干净python运行环境)

   Windows进入该环境：
        |D:\myproject>cd venv
        |D:\myproject\venv>cd scripts
        |D:\myproject\venv\Scripts>activate.bat
        |(venv)D:\myproject\venv\Scripts>

   也可使用：
        venv\scripts\activate


    退出环境：deactivate

8.python3自带venv模块支持轻量级虚拟环境
    创建环境：python -m venv 目录名(myvenv)
    进入退出环境和上面一样

9.格式化

    %s,表示格化式一个对象为字符
    %d,整数
    "Hello, %s"%"zhang3" => "Hello, zhang3"
    "%d"%33 => "33"
    "%s:%d"%("ab",3) => "ab:3"

10.错误
    
    抛出：如果要抛出错误，首先根据需要，可以定义一个错误的class，选择好继承关系
    (无参数)raise 原样抛出
    (在except中)raise 可以把一种类型的错误转换成另一种类型
    except ZeroDivisionError:
        raise ValueError('input error')


    class FooError(ValueError):
        pass
    def foo(s):
        n = int(s)
        if n==0:
            raise FooError('invalid value: %s' % s)
        return 10 / n
    foo('0')

    断言

    assert n != 0,'n is zero!'

   (意思是，n!=0应该为True,否则断言失败，抛出AssertionError)
   python -0 文件名 --> 关闭assert，该语句均当做pass

    pdb--调试器--单步运行
    启动：python -m pdb 文件名
    单步执行代码：n
    查看变量：p 变量名
    退出调试：q
