---
layout: default
title: CSS简介
parent: 前端
has_children: true
nav_order: 1
---
CSS的全称为**Cascading Style Sheets**层叠样式表。

在前端开发中，html用于定义页面的结构(相当于Android layout文件)，JavaScript用于定义页面的行为(相当于Java代码)，而CSS用于定义页面的样式(相当于Android style文件)，CSS使枯燥的页面变得精彩。

----
## 一 CSS语法
CSS规则由两部分组成，**选择器**和**声明**，如下；
```css
h1 {
    color: blue;
    font-size: 12px;
}
```

从上边的例子可以看出，h1为选择器，后跟大括号为属性声明，每个声明由一个属性和属性值组成，每个声明用分号分割。其中选择器用来定位CSS作用的目标，比如h1表示作用于h1标签；属性声明用来定义标签内容的显示效果，比如上面的例子，颜色为蓝色，字体大小为12px。CSS样式主要就是给目标标签增加样式。

## 二 CSS创建

如何将CSS样式作用于html页面？
+ 外部样式表(External style sheet) 
+ 内部样式表(Internal style sheet) 
+ 内联样式(Inline style)

### 外部样式表
 外部样式表就是将CSS样式定义在后缀为.css的文件中，然后链接到目标html页面中，导入方式如下；
 ```html
<head>
    <link rel = "stylesheet" type="text/css" href="mystyle.css">
</head>
 ```
外部样式表的好处是可以定义一份样式，然后导入到多个html文件中，实现样式的复用。所以，当样式需要作用于多个页面的时候，最好使用外部样式表，可以实现改变一个样式表，同时改变多个页面的样式。

### 内部样式表
当样式具有特殊性，只需要作用于一个页面，没有复用的需求时，我们也可以直接在页面当中定义样式，这就是内部样式表。方式如下；
```html
<head>
    <style>
        p {color: green;}
        body{background-image:url("image/back40.gif");}
    </style>
</head>
```
### 内联样式
html的标签中有一个style属性，我们可以直接把样式声明到这里，这就是内联样式。由于内容和表现混杂在一起，内联样式会损失掉样式表的许多优势。对于一个页面中，只会对一个标签使用一次的样式可以这样做。方式如下；
```html
<p style="color:green;margin-left:20px">这是一个p标签</p>
```

上边讲的三种定义和插入样式表的方式，外部样式表可以认为是最抽象的样式表，它可以作用于多个页面；内部样式表是具体到某个页面的样式表，比外部样式表更具体；内联样式表作用域页面中某个具体的标签上，是最具体的声明样式的方式。于是我们可能会面临这样一种局面，**有一个标签被外部样式表和内部样式表同时影响，或者还有内联样式。那么如何确定这个标签最终的样式那？**

**最终，样式的属性值会从更具体的样式表中被继承过来。有点类似于java中类的继承，子类中定义的同名属性或者方法会重写父类中的同名属性或者方法。** 例如;
```css
/*外部样式表*/
p {
    color:red;
    text-align:left;
    font-size:8pt;
    }
/*某个页面内部也有一个样式表，并且这个页面也链接了上边的样式表*/    
p {
    text-align:right;
    font-size:20pt
    }
/*p标签内联样式*/
<p style="color:green">这是一个p标签</p>
```
那么最终这个页面的p标签得到的样式如下；
```css
p {
    color:green;
    text-align:right;
    font-size:20pt;
}
```
**可以看到，当有同名属性时，最终的样式属性为更具体的样式表中的属性值，不重复的则正常产生作用。**

**所以，样式表的优先级为：内联样式表 > 内部样式表 > 外部样式表**