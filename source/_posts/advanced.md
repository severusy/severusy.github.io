---
title: python的高级特性们
date: 2017-05-28 01:09:17
tags: python
categories: techn
---

## 切片(Slice操作符)

（取list或tuple的部分元素）

L = ['Michael','Sarah','Tracy','Bob','Jack']

    L[0:3]
    ['Michael', 'Sarah', 'Tracy']

从0开始取，但不包括3。
0,1,2总共3个元素。<!-- more -->

省略方法（如果第一个索引0）

    L[:3]
    ['Michael', 'Sarah', 'Tracy']

也可从索引1开始取出2个元素

    L[1：3]
    ['Sarah', 'Tracy']

倒数切片：**L[-1]** 取倒数第一个元素

举例：list

      L = list(range(100))
    
    0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99
    
    前10个数：L[:10]
    [0，1，2，3，4，5，6，7，8，9]
    
    后10个数：L[-10:]
    
    前11-20个数:L[10：20]
    [10，11，12，13，14，15，16，17，18，19]
    
    前10个数,每两个取一个：
    L[:10：2]
    [0，2，4，6，8]
    
    所有数，每五个取一个：
    L[::5]
    [0，5，10，15，20，25，30，35，40，45，50，55，60，65，70，75，80，85，90，95]
    
    L[:]
    原样复制一个list

tuple的切片也是tuple

字符串也可看做list，每个元素就是一个字符，所以字符串也可以切片，结果仍为字符串

    'ABCDEFG'[:3]
    'ABC'
    'ABCDEFG'[::2]
    'ACEG'

## 迭代（for循环 *遍历*  list/tuple）

1、对dict的迭代：
   默认情况下，dict迭代的是key：

    d = {'a':1,'b':2,'c':3}
    for key in d:
        print(key)
    
        a
        b
        c

   如果要迭代value，可以用

     for value in d.values()

   如果同时迭代key和value，可使用：

     for k,v in d.items()

2、字符串的迭代

    for ch in 'ABC':
        print(ch)
    
        A
        B
        C

for迭代时，只要作用于可迭代对象就可以正常运行

3、判断**可迭代对象**：collections模块的lterable类型判断

    from collections import Iterable
    print(isinstance('abc',Iterable))#str是否可迭代
    print(isinstance([1,2,3],Iterable))#list是否可迭代
    print(isinstance((1,2,3),Iterable)) #tuple是否可迭代
    print(isinstance(123,Iterable)) #整数是否可迭代
    
    True
    True
    True
    False

4、把list变成下标循环(索引-元素对)

可以在for循环中同时迭代索引和元素本身

    for i,value in enumerate(['A','B','C']):
    print(i,value)
    
    0 A
    1 B
    2 C
    
    for x,y in [(1,1),(2,4),(3,9)]:
    print(x,y)
    
    1 1
    2 4
    3 9

## 列表生成式 list comprehensions

求x*x的值，x = [1,2,3,4,5,6,7,8,9,10]

    [x*x for x in range(1,11)]
    
    生成元素放到前面，后面跟for循环-->创建list

for 后面加上if筛选偶数的平方：

    [x*x for x in range(1,11) if x%2 == 0]
    [4, 16, 36, 64, 100]

两层循环生成全排列：

    [m + n for m in 'ABC' for n in 'XYZ']
    ['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']

举例：

用两个变量生成list：

    d = {'x':'A','y':'B','z':'C'}
    [k + '=' + v for k,v in d.items()]
    
    ['x=A', 'y=B', 'z=C']

把一个list中的所有字符变成小写：

    L = ['Hello','World','IBM','Apple']
    print([s.lower() for s in L])
    
    ['hello', 'world', 'ibm', 'apple']

混合数据类型大写变小写：

    L1 = ['Hello', 'World', 18, 'Apple', None]
    L2 = [s.lower() for s in L1 if isinstance(s,str) == True]
    # 期待输出: ['hello', 'world', 'apple']
    print(L2)

输出：

     ['hello', 'world', 'apple']

## 生成器（一边循环一边计算）

创建生成器的方法：

1、把列表生成式的[]改成()

    g = (x*x for x in range(10))
    g
    
    <generator object <genexpr> at 0x02543F30>

打印generator的每个元素：

(1)使用next()
    
    next(g)
    0
    next(g)
    1
    ...
    next(g)
    StopIteration

计算到最后一个元素的时候返回StopIteration错误

(2)for()迭代generator

    g = (x*x for x in range(10))
    for n in g:
        print(n)
    
    0
    1
    4
    9
    16
    25
    36
    49
    64
    81



## 迭代器

isinstance()判断对象是否为Iterable()

    from collections import Iterable
    isinstance([],Iterable)
    isinstance({},Iterable)
    isinstance('abc',Iterable)
    
    True
    True
    True

**迭代器Iterator**：被next()函数调用并不断返回下一个值的对象

使用iter()函数可以将Iterable变成Iterator

