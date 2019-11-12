**第6章 基于UDP的服务器端/客户端**
TCP比UDP慢的原因通常有以下两点：
- 收发数据前后进行的连接设置及清除过程
- 收发数据过程中为保证可靠性而添加的流控制

**基于UDP的数据I/O函数**
// 成功返回传输字节数；失败返回SOCKET_ERROR
int sendto(SOCKET s, const char* buf, int len, int flags, const struct sockaddr* to, int tolen);
// 成功时返回接收的字节数，失败时返回SOCKET_ERROR
int recvfrom(SOCKET s, char* buf, int len, int flag, struct sockaddr* from, int* fromlen);

**UDP客户端套接字的地址分配**
调用sendto函数时自动分配IP和端口号，IP用主机IP， 端口号选尚未使用的任意端口号

**存在数据边界的UDP套接字**
TCP数据传输中不存在边界，表示“数据传输过程中调用I/O函数的次数不具有任何意义”
相反，UDP是具有数据边界的协议，传输中调用I/O函数的次数非常重要。因此输入函数的调用次数应与输出函数的调用次数完全一致，这样才能保证接收全部已发送数据。

**已连接(connected)UDP套接字与未连接（unconnected）UDP套接字**
通过sendto函数传输数据大致可分为以下3个阶段：
- 向UDP套接字注册目标IP和端口号
- 传输数据
- 删除UDP套接字中注册的目标地址信息

可以重复利用同一UDP套接字向不同目标传输数据。这种未注册目标地址信息的套接字称为未连接套接字。反之，注册了目标地址的套接字称为连接connected套接字。
