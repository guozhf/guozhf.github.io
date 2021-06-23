---
layout: default
title: 前端
nav_order: 5
has_children: true
permalink: /docs/front
---

# 从Android到大前端的转型

Android和前端具有一样的开发模式，都是前后端分离的，后台提供服务，前台(Web/App)结合后台数据渲染UI。
对于请求后台数据，他们都有相应的请求库；
对于前台渲染，Android一般是xml布局文件构建布局，Activity处理逻辑，Style定义样式(xml中也会直接写一些样式，类似于内联Style)，不管是样式，布局，逻辑，还是请求后台数据，一般情况下都是在Activity中进行的，Activity是Android中一个页面的总管；而对于前端而言，具体是Vue项目，< template >相当于xml布局文件，用于构架UI结构，< script > 相当于Activity中的业务处理代码，< style > 相当于Android中的Style样式文件，用来定义样式，而这些都是定义在一个.vue文件中的，这个文件就相当于Android中的Activity，是一个页面的总管。

具体分析下一个.vue文件中的代码：
## < template>
< template> 编写UI代码，根目录必须为一个div，相当于Android中的布局根目录，在这个目录下可以使用html标签，和各种组件，而这些组件也是定义在一个个.vue文件中的，这些组件相当于Android中的系统控件和自定义控件，但是有一个重要的不同点是，在Android中，页面是Activity或者Activity嵌套的fragment，控件都继承自View；而在Vue中，页面和组件都是.vue文件，也就是说页面也相当于一个大的组件，一个大的组件由不同的小的组件组合而来，这一点非常像Android自定义控件时候使用的组合控件。对于这一部分，需要学习如何使用html标签，如何使用系统组件，并且能够自定义组件，组件承载了一个完整的功能模块，或者承载了整个页面，并且，一般项目中都会有一个根vue，这个根vue承载了整个应用。另外，在这一部分，会涉及到一些方法或者事件调用，这部分代码将出现在< script >中。

## < script>
这部分就相当于Activity中的业务逻辑代码部分，比如UI中调用的方法，点击事件等，同时可以定义变量，还可以调用其他模块的代码，也就是java中的import。

这一部分和Activity中的代码编写逻辑基本上是一样的，首先前几行是导包，import xxx from ...dir,接下来可以定义常量 const xxx = ...., 最后所有的代码都会被包含在export default {} 中，在这里边就是当前组件的业务逻辑代码了。首先是name属性，组件总要有个名字，这是必须的，组件也可以嵌套其他组件，然后在components中是嵌套的子组件。然后是computed，计算属性，这个和方法差不多，只不过使用了缓存，计算属性名字代表了一个属性，不过这个属性是动态生成的，并且有缓存。接下来是filter过滤器，顾名思义，就是用来过滤数据的，这个还没看，暂时不讲。接下来是data()方法，在里边声明了使用到的所有变量。data()方法后边是各种生命周期方法，接下来是methods，这里边用来定义方法。到此为止，< script>部分结束。

## < style>
这部分主要就是样式代码，没什么好说的。

通过和Android开发的对比，我们很容易的将陌生的前端开发映射到了Android开发中，能让我们先忽略细节，加快理解，迅速入门。
