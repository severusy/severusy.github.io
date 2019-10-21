---
title: Head First Python 笔记
date: 
tags: python入门
categories: python
---
### 第一章
点记法调用方法
append()--列表末尾添加
pop()--列表末尾删除
extend()--列表末尾添加数据项集合
remove()--删除特定项
insert(0,'able')--特定位置前添加项
len()--长度

for 目标标识符 in 列表：
    列表处理
(!for 只打印外列表的各数据项)

isinstance()--判断当前处理的特定标识符是否本身为某特定类型数据
dir(_bulitins_)--BIF列表

if 必有一个else与之对应

def 函数名(参数):
    内容
列表用中括号包围

### 第二章 模块

####自建模块(windows)
1、将模块文件nester.py放到模块文件夹nester中
2、模块文件夹中创建setup.py,包含有关发布的元数据
    
    from distutils.core import setup
    setup(
        name = 'nester',
        version = '1.0.0',
        py_modules = ['nester'],
        author = 'hfpython',--可以不同
        author_email = 'hfpython@headfirstlabs.com',--
        url = 'http://www.headfirstlabs.com'--
        description = 'A simple printer of nested lists',--
        )

3、构建发布文件：
    在模块文件夹nester中打开终端窗口，键入命令

    E:\coding\python3.6.2\python.exe(Python安装路径) setup.py sdist 

4、将发布安装到python本地副本中

    E:\coding\python3.6.2\python.exe(安装路径) setup.py install
**准备就绪**

#### 导入使用模块

导入：import 模块名
使用时注意命名空间：**nester**.python_lol()

from module import function--导入模块到当前命名空间(模块中的内容可能覆盖自己定义的内容)
import sys; sys.path--展示已有模块路径
range(4)--给定范围(不包括给定数据)
end=''--作为print()BIF的一个参数会：在输入中自动包含换行
indent 缩进

### 第三章 文件与异常
open()BIF--打开磁盘文件，一次读取一个数据行
import os--导入os模块
os.getcwd()--查询当前工作目录
data.readline()--从打开的文件获取一个数据行
data.seek(0)--返回文件起始位置
              python的文件也可使用tell()
命令行中使用for... in ...:后下一行要使用tab缩进
data.close()--文件处理完一定关闭
(":",1)--以：来分解,可选参数控制将数据行分为几部分，设为1可分为两部分
    (role,line_spoken) = each_line.split(':',1)
find(':')--找出一个字符串的子串，找不到返回-1，找到返回子串在原字符串中的索引位置
(tuple)--不可改变值
ValueError--数据格式不符合期望
IOError--数据无法正常访问
#### 异常处理

try：
    保护代码 
except：--要用一种不那么一般化的方式使用except--指定异常
    替代代码

import os 
if os.path.exists('sketch.txt'):--检查文件是否存在
    data = open('sketch.txt')
    .
    .
    .
else:
    print('The data file is missing!')

##### 特殊化异常

try:
    ...
except **ValueError**:--或者IOError
    pass

### 第四章
strip()--该方法从字符串中去除空白字符
out = open('data.out','w')--默认r，若以写模式使用w
    file参数指定数据文件对象
print("Norwegian Blues stun easily.",**file=out**)--file参数控制将数据发送/保存到哪里
str()访问任何数据对象(支持串转换)的串表示
out.close()--刷新输出！！
open的参数：
**w**:文件存在--清空其全部内容
  文件不存在--先创建这个文件，再打开文件写
访问模式**a**:追加到文件
**w+**:打开一个文件完成读写（不清除）

#### try中的finally扩展
--不论出现什么错误都必须运行finally中的代码
locals()--返回当前作用域中定义的所有名(变量)的一个集合
in --测试成员关系
+ --联接字符串，两数相加
##### 显示具体错误内容！！！

    try:
        data = open('missing.txt')
        print(data.readline(),end='')
    except IOError as err:#为异常对象给定一个名字
        print('File error：'+str(err))#err类型必须为str，可以知道具体哪里出了问题
    finally:
        if 'data'in locals():
            data.close()

#### with技术使代码简洁

使用with可以不考虑close(),可自动关闭已打开文件，即使异常也不例外，with也使用as关键字

#### 格式化输出

标准输出(standard output):sys.stdout
可从标准库的“sys”模块导入

使用之前定义的模块nester

print(value,sep='',end='\n',file=sys.stdout)有4个参数
只有缺省值不是想要的值时才需要提供值
调用时可以：
    print('Dead Parrot Sketch',file='myfavmonty.txt')

#### 持久存储

pickle--标准库，可保存加载py数据对象(包括列表)
    允许容易而高效地将py数据对象保存到磁盘以及从磁盘恢复

腌制--将数据对象保存到一个持久存储中的过程中
解除腌制--从持久态恢复到已保存的数据对象的过程
dump()--保存数据至硬盘
load()--从硬盘恢复数据

处理数据要求：以二进制访问模式打开 --open使用wb/rb

    import pickle #导入模块
        ...
    with open('mydata.pickle','wb') as mysavedata:# 保存用dump()
        pickle.dump([1,2,'three'],mysavadata)
        ...
    with open('mydata.pickle','rb') as myrestoredata:# 恢复用load()
        a_list = pickle.load(myrestoredata)
    print(a_list)

### 第五章 处理数据
方法串链：james = data.strip().split(',')--从左向右读
??有顺序要求吗--有啊，但是还不知道是啥样的要求
函数串联：对数据应用一系列函数--从右向左读
    嵌套

####排序
原地排序：排序并替换，原顺序丢失
    对于列表：sort()方法
复制排序：返回有序副本，原顺序保留
    sorted()BIF--注意BIF和方法使用方式不一样
    如果传入 reverse=True可按 **降序**排列数据
    data2 = sorted(data)
#### 推导列表
#####注意顺序：
james1 = sorted([sanitize(j) for j in james])--将规格化的数据排序
james1 = [sorted(sanitize(j)) for j in james]--将每个字符规格化排好序

####删除重复
#####方法一
    julie = sorted([sanitize(j) for j in julie])
    unique_julie = []
    for each_t in julie:
        if each_t not in unique_julie:
            unique_julie.append(each_t)
    print(unique_julie[0:3])
#####方法二：集合
创建空集合 set()BIF
    
    distances = set()
    distances ={10.6,11,8,10.6,"two",7}--重复项会被忽略
分片
   
    james2 = sorted(set(james1))[0:3]--利用sorted()生成的列表应用分片

### 第六章 定制数据对象
pop()--调用本方法将 删除并返回列表内指定数据项
    x = pop(0)--调用会删除第一个数据并把它赋给指定变量x
定义字典：

    cleese = {}
    cleese = dict()

#### 打包数据和代码：类
 对于面向对象，代码称为类的方法（method）数据称为类的属性（attribute）
 实例化的实例化的数据对象：实例（instance）

 定义类：
    class Athlete:
        def_init_(self):
            #初始化各对象的代码

__init__()方法的第一个参数都是self(调用对象实例)

![class](hfpy_class_down.png)

__init__里是强制绑定初始属性,**init左右各有两个下划线**
#####访问限制
内部属性：属性名称前加两个下划线__--私有变量
#####继承和多态
class AthleteList(list):
    def __init__(self,name):
        list.__init__([])
        self.name=name

### 第七章 web开发

