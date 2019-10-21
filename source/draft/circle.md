---
title: 循环
date: 2017-05-14 19:49:41
tags: python
categories: techn
---

###  循环

python有两种循环

#### for x in...循环
  这个循环是依次把list或者tuple中的每个元素迭代出来
  
  也就是把每个元素代入变量x， 然后用x执行缩进块的语句

    sum = 0
    for x in [1,2,3,4,5,6,7,8,9,10]:
          sum = sum + x
    print(sum)

   上面这段代码的输出：

    1
    3
    6
    10
    15
    21
    28
    36
    45
    55

range()函数，给定范围，从0开始，range(5)相当于[0,5)

以下，用range()生成一个整数序列，然后通过list()函数转化为list

    >>> list(range(5))
    [0, 1, 2, 3, 4]

#### while循环

只要条件满足，就不断循环

    sum = 0
    n = 99
    while n > 0:
        sum = sum + n
        n = n - 2
    print(sum)

#### 练习

请利用循环依次对list中的每个名字打印出Hello, xxx!

    L = ['Bart', 'Lisa', 'Adam']
    for x in L:
        print('Hello, %s !' % x)

输出结果： 

    Hello, Bart !
    Hello, Lisa !
    Hello, Adam !

#### break

    n = 1
    while n<= 100:
        if n > 10:
            break
        print(n)
        n = n + 1
    print('END')

   break 用于提前结束循环
#### continue

跳过当前循环，开始下一次循环

###### continue 打印奇数

    n = 0
    while n < 10:
        n = n+1
        if n % 2 == 0:
            continue
        print(n)

##### break和continue要与if配合使用