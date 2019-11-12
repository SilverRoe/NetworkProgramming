**第3章 地址族与数据序列**
struct sockaddr_in{
    sa_family_t     sin_family;  // 地址族(Address Family)
    uint16_t        sin_port;    // 16位 TCP/UDP 端口号
    struct in_addr  sin_addr;    // 32位IP地址
    char            sin_zero[8]; // 不使用
};
struct in_addr{
    in_addr_t        s_addr; // 32位IPv4地址
};

-  sin_family ： 地址族 AF_INET, AF_INET6, AF_LOCAL
-  sin_port : 端口号
-  sin_addr: 32位地址信息
-  sin_zero: 必须填充0

网络字节序：统一为大端序（高位字节存放在低位地址）；
字节序转换
unsigned short htons(unsigned short);
unsigned short ntohs(unsigned short);
unsigned long htonl(unsigned long);
unsigned long ntohl(unsigned long);
-  htons 中 h代表主机（host）字节序
-  htons 中 n代表网络（network）字节序
-  s 指的是 short，l指的是long

htons 可以理解为 “把 short 型数据从主机字节序转换为网络字节序”
ntohs 可以理解为 “把short 型数据从网络字节序转换为主机字节序”

网络地址的初始化与分配
将字符串形式IP地址转为32位整数型数据。此函数在转换类型的同时进行网络字节序转换
`in_addr_t inet_addr(const char* string);`
inet_aton函数与inet_addr函数在功能上完全相同，直接利用in_addr结构体，使用频率更高
`int inet_aton(const char* string, struct in_addr* addr); // 成功时返回1；失败时返回0`
inet_ntoa : 可以把网络字节序整数型IP转换为我们熟悉的字符串
`char* inet_ntoa(struct in_addr adr);`

总结，常见的网络地址初始化方法：
```
struct sockaddr_in addr;
char* serv_ip = "211.217.168.13";
char* serv_port = "9190";
memset(&addr, 0, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_addr.s_addr = inet_addr(serv_ip);
addr.sin_port = htons(atoi(serv_port));
```

**客户端地址信息初始化**
服务器端准备工作通过bind函数完成；而客户端则通过connect函数完成。
1_服务器端声明sockaddr_in 结构体变量，将其初始化为赋予服务器端IP和套接字的端口号，然后调用bind函数；
2_客户端声明sokaddr_in结构体，并初始化为要与之连接的服务器端套接字的IP和端口号，然后调用connect函数。

**INADDR_ANY**
采用这种方式可自动获取运行服务器端的计算机IP地址，不必亲自输入；服务器端优先考虑

**向套接字分配网络地址**
`int bind(int sockfd, struct sockaddr* myaddr, socklen_t addrlen); // 成功时返回0， 失败时返回-1`

**WSAStringToAddress & WSAAddressToString**
这两个转换函数功能上与inet_ntoa和inet_addr完全相同，但优点在于支持多种协议，在IPv4和IPv6中均可使用。
将地址信息字符串适当填入结构体变量
```
INT WSAStringToAddress(
    LPTSTR AddressString, INT AddressFamily, LPWSAPROTOCOL_INFO lpProtocolInfo,
    LPSOCKADDR lpAddress, LPINT lpAddressLength
); // 成功返回0， 失败时返回SOCKET_ERROR
// AddressString: IP和端口号的字符串地址值
// AddressFamily: 第一个参数地址所属的地址族信息
// lpProtocolInfo: 设置协议提供者（Provider），默认为NULL
// lpAddress: 保存地址信息的结构体变量地址值
// lpAddressLength
```

将结构体中的地址信息转换成字符串形式
```
INT WSAAddressToString(
    LPSOCKADDR lpsaAddress, DWORD dwAddressLength,
    LPWSAPROTOCOL_INFO lpProtocolInfo, LPSTR lpszAddressString,
    LPDWORD lpdwAddressStringLength
);
```
