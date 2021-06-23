---
layout: default
title: 准备
parent: 前端
has_children: false
nav_order: 1
---

# npm(Node Package Manager)
npm是使用JavaScript编写的，运行在Node.js当中的包管理器，用来管理前端开发中使用到的库的依赖，比如jquery，bootstrap等，作用和Java开发中
使用到的Maven基本一样。

NPM的思路大概是这样的：
1. 买个服务器作为代码仓库(registry),在里边放置需要被共享的代码
2. 发邮件通知各个库的作者，比如jquery，bootstrap等的作者，让他们使用 **npm publish** 将代码替吉奥到registry上，并分别取名jquery，bootstrap
3. 社区里的其它人如何想要使用这些代码，不用再去各个官方主页去下载，然后手动添加依赖，而是把想要的依赖写进**package.json**里，然后运行**npm install**，npm就会为他们下载代码
4. 下载完的代码就会出现在node_modules目录里，可以随意使用了。

这些可以被使用的代码被叫做包(package)或者库，这就是NPM名字的又来：Node Package Manager。

yarn是和npm一样的包管理器
