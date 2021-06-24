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

package.json用来配置依赖等，node_modules用来存放依赖的包。

yarn是和npm一样的包管理器

# webpack
本质上，webpack 是一个用于现代 JavaScript 应用程序的 静态模块打包工具。当 webpack 处理应用程序时，它会在内部构建一个 依赖图(dependency graph)，此依赖图对应映射到项目所需的每个模块，并生成一个或多个 bundle。作用类似于Gradle，但是它只负责打包，不负责管理依赖，而Gradle除了负责打包以外，还间接通过Maven等仓库来管理依赖。

可以说： Gradle = npm + webpack
就了解这么多就行了。

# javascript如何实现的异步
JavaScript本身是单线程的，从语言层面上讲谈不上异步，实现异步的是其它一些基础设施，例如setTimeout，setInterval。在web范畴内有XHR的onreadystatchange，dom事件，html5里的background worker等等，放大nodejs范畴内则有其它API做了异步，放到其它JS运行环境则可以有其它异步机制。

或者可以这样简单的理解，异步都是靠native提供的，封装成了js可用的API，你没法通过这些API以外的方式自己实现异步操作。
JavaScript是轻量级的脚本语言，也是"嵌入式"的语言，可以嵌入到其它环境内部，JavaScript本身是单线程的，不可能实现异步，而它所嵌入的环境却可以实现异步，比如浏览器或者node中，然后这些环境将异步操作封装成了js可用的API，看起来好像是js实现了异步，实际上并不是。JavaScript线程会同步的执行代码，当遇到异步操作的时候，它会发送
一个异步请求给异步API，而这个异步API由其环境来实现，这个环境可以是多线程的。然后JavaScript并不能异步的结果，而是继续执行下面的代码.当异步任务结束后，就会将回调加入到queque(队列)中，当JavaScript代码执行完毕以后，就会通过Event Loop(事件循环)去读取队列中的回调函数，并且执行。对于JavaScript代码来说，看起来一直是同步的。这里需要注意，是JavaScript将所有同步代码执行完，才会去执行消息队列里的回调函数，所以回调函数总是在最后调用的。

代码实验：
```javascript

function timeout() {
    setTimeout(() => {
        console.log('timeout')
    }, 0)
}

function someTime() {
    let s = Date.now()
    while(true) {
        if (Date.now() - s > 2000) {
            console.log('some time')
            break
        }
    }
}
console.log(1)
timeout()
someTime()
console.log(3)

// 执行结果 1 - some time - 3 - timeout，印证了我们上面的观点
```

我们已经指导了JavaScript是脚本语言，它需要"嵌入"到一个环境中去运行，我们称这个环境为宿主环境，对于前端开发而言，这个宿主环境显然就是浏览器！
虽说JavaScript是单线程的，然后浏览器却不是!

![Alt text](https://github.com/guozhf/guozhf.github.io/blob/master/assets/images/browser.jpg?raw=true)

如图所示，JavaScript引擎线程称为主线程，它负责解析JavaScript代码；其它可以称为辅助线程，这些辅助线程便是JavaScript实现异步的关键。

上边例子中，主线程负责自上而下顺序执行，当遇到setTimeout函数后，便将其交给定时器线程去执行，自己继续执行下面的代码，从而达到异步的目的。
当定时器线程计时完成后，会将回调函数放入**任务队列**中，这些任务加入到任务队列中以后不会立即执行，而是处于等待轧辊台，等到主线程处理完了自己的事情后，才会执行任务队列中的任务。未完待续。。。

https://juejin.cn/post/6844904159385223175