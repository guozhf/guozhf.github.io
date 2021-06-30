---
layout: default
title: 计算机网络
parent: 面试
has_children: false
nav_order: 1
---

# 计算机网络

### 介绍下5层网络模型。

答：从上到下依次为：应用层->传输层->网络层->数据链路层->物理层
https://www.cnblogs.com/blknemo/p/10079644.html

### Http/Https协议工作在那一层？
答：应用层
### TCP/UDP协议工作在哪一层？
答：传输层
### 说一下三次握手和四次挥手
TCP要建立稳定的连接需要进行三次握手，断开连接需要进行四次挥手。
三次握手过程：
    Client想Server发送连接请求报文，Server收到请求后回复ACK报文，并且为这次连接分配资源。Client收到Server回复的ACK报文后也想Server发送ACK报文，并分配资源，这样TCP连接就建立了。
四次挥手过程：
    假设Client端发起终端连接请求，也就是发送FIN报文。Server收到FIN报文后，意思是说“Client已经没有数据要发送给Server端了”，但是Server端如果有数据要发送的话，还可以继续发送，所以不必着急关闭Socket。所以Server端先发送ACK，告诉Client，你的请求我已经收到，但是我还没有准备好，请继续等待我的消息。这个时候Client端就进入了FIN_WAIT状态，继续等待Server端的FIN报文。当Server端确定数据已经发送完成后，则向Client发送FIN报文，告诉Client，我已经发送完成，准备关闭连接。Client端收到FIN报文后，就知道可以关闭连接了，但是它还是不相信网络，怕Server端不知道要关闭，所以发送ACK后进入TIME_WAIT状态，如果Server端没有收到ACK则可以重传。Server端收到ACK后，就知道可以断开连接了。Client端等待了2MSL后依然没有收到回复，说明Server端已经正常关闭，所以Clinent也可以关闭连接了。至此，TCP连接关闭。


