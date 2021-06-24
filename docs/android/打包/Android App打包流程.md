---
layout: default
title: Android App打包流程
parent: Android
has_children: false
nav_order: 1
---

![Alt text](https://raw.githubusercontent.com/guozhf/guozhf.github.io/master/assets/images/package.jpg "打包流程图")

一图胜千言，Android官方给出的这张App 打包流程图，完整的描绘了打包的整个过程，其中方形的为App中的代码，第三方库代码和资源等，椭圆形为打包过程中使用到的工具。我们从上到下，大体的介绍下打包的整个流程。

## 1. 打包资源文件，生成R.java
图上的第一步，Application Resources(应用资源) 通过sdk提供的aapt(Android Asset Packaing Tool) Android资源打包工具生成了R.java。其中应用资源(图片除外)主要是指res下的资源和AndroidManifes文件，他们会被编译成二进制文件，并被分配一个resource id，应用通过resource id来访问相应的资源，如R.string.xxx.
Android应用在编译过程中aapt工具会对资源文件进行编译，还会生成一个resource.arsc文件，resource.arsc文件相当于一个文件索引表，记录了很多跟资源相关的信息。

## 2. 处理aidl文件，生成相应的Java文件
aidl(Android Interface Definition Language)文件是service用于进行进程间通信而创建的文件，他们定义了进程间通信的协议。但是他们不是Java代码，所以需要和处理资源文件一样，先生成java代码。主要通过sdk提供的aidl工具解析aidl文件，然后生成相应的Java Interfaces(Java接口代码)。

## 3. 编译项目源代码，生成class文件
到这里，资源代码已经生成了R.java， .aidl文件也解析成了Java接口代码，再加上我们自己编写的代码(Application Source Code)，这时候，我们的源代码就会通过Java Compiler(Java编译器)生成.class文件(字节码文件)，我们知道Android虚拟机没法直接运行字节码文件，所以还需要进行接下来的转换。

## 4. class文件转换成dex文件
系统通过sdk提供的dex工具，将所有的class文件(我们自己的和第三方库的)转换成了可以运行在Android虚拟机上的dex文件。

## 5. 打包生成APK文件
到这一步，代码都已经编译成了dex文件。Compiled Resources（所有没有编译的资源)，如images、assets目录下资源（该类文件是一些原始文件，APP打包时并不会对其进行编译，而是直接打包到APP中，对于这一类资源文件的访问，应用层代码需要通过文件名对其进行访问）；
编译过的资源和.dex文件都会被apkbuilder工具打包到最终的.apk文件中。

## 6. 对Apk文件进行签名
我们知道，没有签名的Apk安装包是无法安装到Android手机上的，所以在这一步，系统通过sdk提供的签名工具Jarsigner为Apk文件签名，生成签名安装包(Signed.apk)。

## 7. 对签名后的APK文件进行对齐处理
如果你发布的apk是正式版的话，就必须对APK进行对齐处理，用到的工具是zipalign。
对齐的主要过程是将APK包中所有的资源文件距离文件起始偏移为4字节整数倍，这样通过内存映射访问apk文件时的速度会更快。对齐的作用就是减少运行时内存的使用。

以上为Android打包的整个过程，接下来的章节，我们将详细介绍Android打包，安装到Android手机上的整个流程。