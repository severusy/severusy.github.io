---
title: HEXO相关错误
date: 2017-05-20 17:26:10
tags: hexo
categories: techn
---
## hexo搭建博客

这个网上一搜就有，我用的是[windows](http://www.jianshu.com/p/e99ed60390a8)，我就不赘述了。
单说一下在搭建博客时出现的坑：

1、误用linux的安装方式来安装，返回错误

    bush：sudo command not found

还以为环境变量出了问题一直在修改path

经[长航大佬](https://iamsail.github.io/) 指点换了另外的安装姿势

详见[代码咖啡](http://www.jianshu.com/p/e99ed60390a8).这才顺利安装完毕 $

2、用淘宝NPM镜像安装node.js package management[可能]

[链接](http://npm.taobao.org/)

安装方法就是先安装cnpm

    $ npm install -g cnpm --registry=https://registry.npm.taobao.org

然后安装你要安装的那一块内容

    $ cnpm install hexo-renderer-sass --save               
                   [     要安装的那个模块    ]

剩下的部分还没有试，但要安装的已经安装完毕

3、部署到github上时出现错误

在执行 hexo deploy 后

出现 error deployer not found:git 的错误

经查询，hexo更新到3.0后deploy的type应改成git

我的hexo已经是3.0以上版本，type也已是git，仍失败

根据返回错误分析，应该是git这种deploy方法没有找到

于是使用

    npm install hexo-deployer-git --save

之后解决，解决方法来源于[Melodic]()

4、在hexo中插入图片

使用了插件 **asset-image**

利用了hexo的创建资源文件夹

详见[在hexo中无痛插入图片](http://www.tuicool.com/articles/umEBVfI)

不过后来我改成用图床上传图片然后用链接来上传图片了

最后膜拜一个非常厉害的大佬[iIimeTraveler](https://github.com/iTimeTraveler)
和一篇文章[Hexo常见问题解决方案](http://wp.huangshiyang.com/hexo%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88)