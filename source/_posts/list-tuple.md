---
title: list和tuple数据类型
date: 2017-05-13 20:57:05
tags: python
categories: techn
---
## 使用list和tuple
### list（一种数据类型,有序）

    >>> classmates = ['Michael','Bob','Tracy']
    >>> classmates
    ['Michael','Bob','Tracy']

1、向list中追加元素到末尾

    >>> classmates.append('Adam')
    >>> classmates
    ['Michael','Bob','Tracy','Adam']

2、把元素插入指定位置，比如索引号为1的位置：
    
    >>> classmates.insert(1,'Jack')
    >>> classmates
    ['Michael','Jack','Bob','Tracy','Adam']

3、删除list末尾的元素

    >>> classmates.pop()
    'Adam'
    >>> classmates
    ['Michael','Bob','Tracy']

4、删除指定位置的元素pop(i)

替换某个指定的元素，给对应位置直接赋值：

    >>> classmates[1] = 'Sarah'
    >>> classmates
    ['Michael','Sarah','Tracy']

5、list中的元素可以是不同的数据类型
  list可以嵌套使用 相当于二维数组，三维...
  list可以是空list

    >>> L = []
    >>> len(L)
    0

### tuple (元组 有序 初始化后不可修改)

    >>> classmates = ('Michael','Bob','Tracy')

   这时classmates就不可以更改了，只能获取元素，比如说使用classmates[0],但是不能赋值成其他元素

   1、在定义tuple的时候，其中的元素就必须被确定下来

   2、如果要定义一个空的tuple，可以

    >>> t = ()
    >>> t
    ()

   3、如果要定义只有一个元素的tuple，需要给一个元素的tuple在定义时加一个逗号，来消除歧义
    >>> t=(1,)
    >>> t
    >>> (1,)

不加逗号的()按照表示数学公式中的小括号来进行计算

   4、可变的 tuple

    >>> t = ('a','b',['A','B'])
    >>> t[2][0] = 'X'
    >>> t[2][1] = 'Y'
    >>> t
    >>> ('a','b',['X','Y'])

   其实是用一个tuple里包含一个list元素，然后list元素可以改变
