---
title: 函数
date: 2017-05-18 22:44:25
tags: python
categories: techn
---
## 调用函数
### python内置函数

[官方文档中的函数](https://docs.python.org/3/library/functions.html)

### 调用函数

可以直接用python内置函数把一种数据类型变成另一种数据类型

### 定义函数

    def my_abs(x):
        if x>=0:
            return x
        else:
            return -x

可以直接在python命令行中定义和输出如
    
    >>> def my_abs(x):
    ...     if x >= 0:
    ...             return x
    ...     else:
    ...             return -x
    ...
    >>> my_abs(8)
    8
    >>> my_abs(-5)
    5

定义函数后，输入指示符会变成...
函数定义完毕后，要两次回车才能变回>>>

当把定义了my_abs()函数的文件保存为 abstest.py
那么可以在当前目录下启动python解释器，利用from abstest import my_abs
来导入my_abs()函数

### 定义空函数

    def nop()
        pass

pass 可做占位符，如果没想好要怎么写函数，就可以先用一个pass使代码可以运转起来

#### 返回多个值

    import math
    def move(x,y,step,angle = 0):
        nx = x + step * math.cos(angle)
        ny = y - step * math.sin(angle)
        return nx, ny
    x, y = move(100,100,60,math.pi/6)
    print(x,y)
    
    151.96152422706632 70.0

   其实在这里的返回值是一个不可变值的tuple，

   在语法上，tuple可以省略括号，

   多个变量可以同时接受一个tuple，按位赋对应的值。

##### 函数调用时确定参数和返回值即可

### 函数的参数类型和例子

#### 位置参数

 传入的值按位置顺序依次赋给参数

 例:

     def power(x,n):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
    print(power(5,0))
    
    1

#### 默认参数（缺省值）

某个值在定义时即赋初值，这样在 这个值没有给出 的调用时也能正常运行

    def power(x=2,n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s 
    print(power())
    print(power(5))
    #print(power(,4)) 返回错误

缺省值只能从前向后缺省
赋初值可以只赋一个，但应从后向前赋值

默认参数必须指向不变对象，指向变量可能会因为变量被更改而出现错误

可以给变量定义None

例:

    def add_end(L=None):
    if L is None:
        L = []
    L.append('END')
    return L
    print(add_end())
    
    ['END']

#### 可变参数

  传入0个或任意个参数，（参数在函数调用时自动组装为一个tuple）

  定义方式：** * **

    def calc(*numbers):
        sum = 0
        for n in numbers:
            sum = sum + n * n
        return sum

##### 把已有的list或tuple作为可变参数，调用一个函数

    num = [1,2,3]
    print(calc(*num))
    
    14

 **利用*num来把num这个list中的所有元素传入函数，很有用！**

#### 关键字参数

传入0个或任意个含参数名的参数，（参数在函数内部自动组装成一个dict）

    def person(name,age,**kw):
        print('name:',name,'age:',age,'other:',kw)

 必选参数：name，age

 关键字参数：kw (形式必须是:参数名=参数)

 调用函数时可以只传入必选参数

 也可传入任意个数的关键字参数

    print(person('Michael',30))
    print(person('Bob',35,city='Beijing'))
    print(person('Adam',45,gender='M',job='Engineer'))

运行结果：

    name: Michael age: 30 other: {}
    None
    name: Bob age: 35 other: {'city': 'Beijing'}
    None
    name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
    None

##### 把已有的dict传入到函数的**kw参数

    extra = {'city':'Beijing','job':'Engineer'}
    person('Jack',24,**extra)

 **extra : 把extra这个dict的key-value用关键字参数传入到函数的**kw参数中

 对kw的改动不会影响extra

#### 命名关键字参数

限制关键字参数的名字，就可以用命名关键字参数

例如只接受city和job作为关键字参数

定义函数：

    def person(name,age,*,city,job):
        print(name,age,city,job)

分隔符** * **， * 后面的参数被视为命名关键字函数

调用方式：

    person('Jack',24,city='Beijing',job='Engineer')

结果：
    
    Jack 24 Beijing Engineer

如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不用特殊分隔符*

    def person(name,age,*args,city,job):
    print(name,age,args,city,job)


    person('Jack',24,city='Beijing',job='Engineer')
    Jack 24 () Beijing Engineer

**命名关键字参数必须传入参数名，如果没有传入，调用将报错**

    person('Jack', 24, 'Beijing', 'Engineer') 
    
    Traceback (most recent call last):
    File "D:\code\py\function.py", line 106, in <module>
    person('Jack',24,'Beijing','Engineer')
    TypeError: person() missing 2 required keyword-only arguments: 'city' and 'job'

python解释器把4个参数均视为位置参数，但person()只接受2个位置参数。

命名关键字参数可以有缺省值

#### 参数组合

python中定义函数时：参数类型的定义顺序必须是：
**必选参数，默认参数，可变参数，命名关键字参数，关键字参数**

    ##a,b,默认参数，可变参数，关键字参数
    def f1(a,b,c=0,*args,**kw):
        print('a=',a,'b=',b,'c=',c,'args=',args,'kw=',kw)
    #a,b,默认参数，分隔符（命名关键字参数），命名关键字参数，关键字参数
    def f2(a,b,c=0,*,d,**kw):
        print('a=',a,'b=',b,'c=',c,'d=',d,'kw=',kw)

调用：

    f1(1,2)
    f1(1,2,c=3)
    f1(1,2,3,'a','b',x=99)
    f1(1,2,3,'a','b')
    f2(1,2,d=99,ext=None)

结果：

    a= 1 b= 2 c= 0 args= () kw= {}
    a= 1 b= 2 c= 3 args= () kw= {}
    a= 1 b= 2 c= 3 args= ('a', 'b') kw= {'x': 99}
    a= 1 b= 2 c= 3 args= ('a', 'b') kw= {}
    a= 1 b= 2 c= 0 d= 99 kw= {'ext': None}

通过tuple和dict调用：

    args = (1,2,3,4)
    kw = {'d':99,'x':'#'}
    f1(*args,**kw)
    
    a= 1 b= 2 c= 3 args= (4,) kw= {'d': 99, 'x': '#'}
    #为什么args返回(4,)?
    
    args = (1,2,3)
    kw = {'d':88,'x':'#'}
    f2(*args,**kw)
    
    a= 1 b= 2 c= 3 d= 88 kw= {'x': '#'}
## 有点懵==

kw中的值赋给d了吗？(关键字参数的参数可以匹配给命名关键字)
然后kw就只输出剩下的那一部分？

**对于任意函数，都可以通过类似func(*args, **kw)的形式调用它，无论它的参数是如何定义的。**

### 递归函数

小心栈溢出--使用**尾递归**优化

在函数返回时，调用自身本身，return语句不能包含表达式。

这样递归本身调用多少次都只占用一个栈帧，不会出现栈溢出的情况

    def fact(n):
    return fact_iter(n,1)
    
    def fact_iter(num,product):
        if num == 1:
            return product
        return fact_iter(num - 1, num * product)
    print(fact(5))

运算过程：

    fact(5)
    fact_iter(5,1)
    num = 5 != 1 : return fact_iter(4,5)
    num = 4 != 1 : return fact_iter(3,5*4=20)
    num = 3 != 1 : return fact_iter(2,5*4*3=60)
    num = 2 != 1 : return fact_iter(1,5*4*3*2=120)
    num = 1 :return 120

### 汉诺塔的移动可以用递归函数非常简单地实现。

请编写move(n, a, b, c)函数，它接收参数n，表示3个柱子A、B、C中第1个柱子A的盘子数量，然后打印出把所有盘子从A借助B移动到C的方法，例如：

    def move(n, a, b, c):
        if n == 1:
            print('move',a,'-->',c)
        else:
            move(n-1,a,c,b)
            move(1,a,b,c)
            move(n-1,b,a,c)
    
    move(3, 'A', 'B', 'C') 
    
    输出:
    A --> C
    A --> B
    C --> B
    A --> C
    B --> A
    B --> C
    A --> C

题目已知三个柱子，（A柱子上放有大小从小到大的1,2,3号圆盘），所以一定要用到B的过渡
所以当n！=1时，
首先移动A上的1号到C上
2-->B
然后把C上的1号-->B上的2上
A上的3-->C(空)上
B上的1-->A(空)上
B上的2-->C上的3上
A上的1-->C中3,2上
完成移动