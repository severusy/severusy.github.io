---
title: 高阶函数
date: 2017-07-22 15:33:52
tags: python
categories: techn
---

1、map()
	map()接收两个参数：一个函数一个Iterable
	作用：把传入的函数作用于序列的每个元素上，并把结果作为新Iterator返回 ;Iterable和Iterator？？？
	例子：

	def f(x):
	    return x*x
    r = map(f,[1,2,3,4,5,6,7,8,9])
    print(list(r))

    [1, 4, 9, 16, 25, 36, 49, 64, 81]

2、reduce()

   reduce()接收两个参数:一个函数(接收两个参数)一个序列
   作用：函数接收序列中的两个数，结果继续和序列的下一个元素做累积计算
   例子：
    1、求和

    from functools import reduce
    def add(x,y):
        return x+y
    print(reduce(add,[1,3,5,7,9]))

    25

    2、将序列转换为整数

    from functools import reduce
    def fn(x,y):
        return x*10+y
    print(reduce(fn,[1,3,5,7,9]))

    13579

3、map()&reduce()
例子：

    from functools import reduce
    def fn(x,y):
        return x*10+y
    def char2num(s):
        return {'0':1,'1':1,'2':2,'3':3,'4':4,'5':5,'6':6,'7':7,'8':8,'9':9}[s]
    print(reduce(fn,map(char2num,'13579')))

整理为str2int的函数：

    from functools import reduce
    def str2int(s):
        def fn(x,y):
            return x*10+y
        def char2num(s):
            return {'0':0,'1':1,'2':2,'3':3,'4':4,'5':5,'6':6,'7':7,'8':8,'9':9}[s]
        return reduce(fn,map(char2num,s))







