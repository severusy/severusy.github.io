---
title: 条件
date: 2017-05-14 18:01:02
tags: python
categories: techn
---
### 条件判断

1、格式：（***注意冒号*** **：**）
   
    if <条件判断1>：
    <执行1>
    elif <条件判断2>：
    <执行2>
    else：
    <执行3>

2、if语句执行从上往下判断，如果在某个判断上是True，把该判断对应的语句执行后，就忽略掉剩下的elif和else

### input

用input()读取用户输入

    D:\code\py>python if.py
    birth:1997

返回 报错

    Traceback (most recent call last):
    File "if.py", line 19, in <module>
    if birth < 2000
    TypeError: '<' not supported between instances of 'str' and 'int'

原因：
   input()返回的数据类型是 str ，str不能直接跟整数比较，必须先把 str 转换成整数

   int()可以吧str转换成整数，就可以用输入的1997和2000进行比较了

   如果输入abc，则int()函数会因为发现输入的是字符串不是数字而报错，程序退出

### 练习

小明身高1.75，体重80.5kg。请根据BMI公式（体重除以身高的平方）帮小明计算他的BMI指数，并根据BMI指数：

低于18.5：过轻
18.5-25：正常
25-28：过重
28-32：肥胖
高于32：严重肥胖
用if-elif判断并打印结果：

    # -*- coding: utf-8 -*-
    height = 1.75
    weight = 80.5
    bmi = weight/(height*height)
    if bmi < 0:
        pass
    elif bmi < 18.5:
        print('过轻')
    elif bmi >= 18.5 and bmi < 25:
        print('正常')
    elif bmi >= 25 and bmi < 28:
        print('过重')
    elif bmi >= 28 and bmi < 32:
        print('肥胖')
    elif bmi >=32 :
        print('严重肥胖')

这段代码我直接粘贴后 运行 返回了如下错误：

    File "if.py", line 26
    height = 1.75
    ^
    IndentationError: unexpected indent

百度后得到

>python是一种对缩进非常敏感的语言，最常见的情况是tab和空格的混用会导致错误，或者缩进不对，而这是用肉眼无法分别的。
 
经重新敲了一遍所有的空格后，终于成功了==
以后要注意这样的问题。
    

