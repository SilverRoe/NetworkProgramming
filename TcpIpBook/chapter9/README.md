**第9章 套接字的多种可选项**
getsockopt & setsockopt
```
int getsockopt(SOCKET sock, int level, int optname, char* optval, int* optlen); // 成功返回0， 失败返回SOCKET_ERROR
// sock : 要查看可选项的套接字句柄
// level: 要查看的可选项协议层
// optname: 要查看的可选项名
// optval: 保存查看结果的缓冲地址值
// optlen: 向第四个参数optval传递的缓冲大小
```

`int setsockopt(SOCKET sock, int level, int optname, const char* optval, int optlen); // 成功时返回0， 失败时返回SOCKET_ERROR`

**SO_SNDBUF & SO_RCVBUF**
SO_RCVBUF : 输入缓冲大小相关可选项
SO_SNDBUF: 输出缓冲大小相关可选项
缓冲大小设置需要谨慎处理，因此不会完全按照我们的要求进行，只是通过调用setsockopt函数向系统传递我们的要求。

**SO_REUSEADDR**
Binding Error
Time-wait

**TCP_NODELAY**
Nagle算法： 只有收到前一数据的ACK消息时，Nagle算法才发送下一数据
不使用Nagle算法要比使用它时传输速度快；最典型的是“传输大文件数据”
将TCP_NODELAY 改为1，则禁用Nagle算法；
