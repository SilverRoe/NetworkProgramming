**第4章 基于TCP的服务器端/客户端**
4.1 理解TCP和UDP
IP本身是面向消息的，不可靠的协议。IP协议无法应对数据错误。

**TCP/UDP 层**
应用层：选择数据传输路径，数据确认过程被隐藏到套接字内部。网络编程大部分内容就是设计并实现应用层协议。

4.2 实现基于TCP的服务器端/客户端
**TCP服务器端的默认函数调用顺序**
![image](https://user-images.githubusercontent.com/9459896/68635903-e6fd0000-0534-11ea-9159-5d59edd555ad.png)

**进入等待连接请求状态**
调用listen函数进入等待连接请求状态
```
int listen(int sock, int backlog); // 成功时返回0， 失败时返回-1
// sock: 希望进入等待连接请求状态的套接字头文件描述符
// backlog: 连接请求等待队列（Queue）的长度
```

**受理客户端连接请求**
受理意味着进入可接受数据的状态
`int accept(int sock, struct sockaddr* addr, socklen_t* addrlen); // 成功时返回创建的套接字文件描述符；失败返回-1
`
TCP客户端默认调用顺序
`int connect(int sock, struct sockaddr* servaddr, socklen_t addrlen); `
调用connect后，发生以下情况之一才会返回：
- 服务器端接收连接请求
- 发生断网等异常情况而中断连接请求

客户端套接字何时，何地，如何分配地址？
- 何时？调用connect函数时
- 何地？操作系统，更准确的说是在内核中
- 如何？IP用计算机（主机）的IP，端口随机

