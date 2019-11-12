**第8章 域名及网络地址**
**DNS服务器**
浏览器地址栏中输入域名后，浏览器通过默认DNS服务器获取该域名对应的IP地址信息，之后才能真正接入网络
ping www.naver.com

`struct hostent* gethostbyname(const char* name);`
`struct hostent* gethostbyaddr(const char* addr, int len, int type);`
