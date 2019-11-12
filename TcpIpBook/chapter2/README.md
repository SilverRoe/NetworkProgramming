**第2章 套接字类型与协议设置**
**创建套接字**
```
int socket(int domain, int type, int prorocol); // 成功时返回文件描述符，失败时返回-1
// domain: 套接字中使用的协议族(Protocol Family)信息
// type: 套接字数据传输类型信息
// protocol: 计算机间通信中使用的协议信息
```

协议族
PE_INET; PE_INET6; PF_LOCAL; PF_PACKAGE; PF_IPX

**套接字类型**
2种典型数据传输方式：
面向连接套接字(SOCK_STREAM)：理解为传送带；“可靠的，按序传递的，基于字节的面向连接的数据传输方式”
面向消息套接字（SOCK_DGRAM）理解为快递包裹；“不可靠的，不按序传递的，以数据高速传输为目的的套接字”

协议的最终选择
大部分情况可以向第三个参数protocol传递0；除非遇到以下情况“同一协议族中存在多个数据传输方式相同的协议”
