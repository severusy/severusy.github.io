---
title: hexo 多台电脑 更新 GitHub 博客 （上）
date: 2019-10-21 21:27:57
tags: hexo
categories: techn
---

##### 准备工作

确保自己已经使用hexo在github搭建了个人博客

##### 新建备份分支

在GitHub的博客仓库（username.github.io）新建一个分支 “hexo”，切换到该分支，并在 仓库-> Settings->Branches->Default branch 中，将默认分支改为hexo，Update保存。

将该仓库克隆至本地，进入本地 username.github.io文件目录中。

git branch 查看当前所在分支，确认为hexo

![1571662421496](https://ftp.bmp.ovh/imgs/2019/10/1c952585fce33bcd.png)

##### 将本地博客部署文件拷贝到username.github.io文件目录

将之前hexo项目目录下的全部文件拷贝到username.github.io文件目录中。

进入username.github.io文件目录下，依次执行：

git add .

git commit -m 'back up'

git push

**问题来了**

![](https://ftp.bmp.ovh/imgs/2019/10/60e9ac2c005b86af.png)

每次使用git push 就会要求输入username for 'https://github.com': 以及密码

输入登录邮箱及密码后会显示出错，有人说使用：

```
git remote set-url origin git+ssh://git@github.com/username/reponame.git
```

使用后没有效果，也有说密码不是登录密码，是

GitHub账户的Settings->Developer settings中的Personal access tokens，然而我的Personal access tokens还不存在。。

后来找到了解决办法：

![](https://ftp.bmp.ovh/imgs/2019/10/6816124b42fc3a33.png)

更改了当前仓库下./git 中的config文件：

![](https://ftp.bmp.ovh/imgs/2019/10/83cbcd291bbf3d62.png)

后来使用 git push 时会有如下提示信息：

![](https://ftp.bmp.ovh/imgs/2019/10/4ae85979f984e6ff.png)

改成 git push origin hexo 就可以了



##### 网页端删除GitHub分支

![](https://ftp.bmp.ovh/imgs/2019/10/d718b549f487ab21.png)

windows使用Edge浏览器时，有垃圾桶按钮，可以删除，

Ubuntu使用Chrome浏览器时，无垃圾桶按钮。



##### 参考链接

https://blog.csdn.net/Zhangxiaorui_9/article/details/79723288

https://www.jianshu.com/p/0b1fccce74e0

https://stackoverflow.com/questions/10909221/why-is-github-asking-for-username-password-when-following-the-instructions-on-sc

网页端删除分支： https://blog.csdn.net/yanhanhui1/article/details/82819665

[本次使用的图床](https://imgurl.org/)

