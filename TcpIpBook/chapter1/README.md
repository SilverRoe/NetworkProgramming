**第1章 理解网络编程和套接字**
基于Windows的I/O函数

`int send(SOCKET s, const char* buf, int len, int flags); // 成功时返回传输字节数，失败时返回SOCKET_ERROR`

`int recv(SOCKET s, const char* buf, int len, int flags); // 成功时返回接收的字节数（收到EOF时为0），失败时返回SOCKET_ERROR`
