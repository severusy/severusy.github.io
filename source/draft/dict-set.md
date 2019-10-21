---
title: dict与数据设置
date: 2017-05-20 17:10:54
tags: python
categories: techn
---
### dict和set

python内置了字典

根据同学的名字查找成绩-利用list

    names = ['Michael','Bob','Tracy']
    scores = [95,75,85]

-利用dict

    >>> d = {'Michael':95,'Bob':75,'Tracy':85}
    >>> d['Michael']
    95

**注意：利用dict时使用的是{ }而非[ ]**

-利用dict-通过key给出数据

    >>> d['Adam'] = 67
    >>> d['Adam']
    67

1个key对应1个value值，多次对1个key放入value，后面的值有效

key不存在，dict会报错，为避免key不存在的错误，有两种方法：

1、通过in

    >>> 'Thomas' in d
    False

2、通过dict提供的get方法

    >>> d.get('Thomas')
    >>> 
   返回none，python的交互式命令行不显示结果

    >>> d.get('Thomas',-1)
    >>> -1
   自己设置如果找不到Thomas的返回值为-1，如果找不到，就返回-1

    >>> d.get('Michael',-1)
    >>> 95
   找得到就返回对应的value

#### dict内部存放顺序与key的放入顺序无关