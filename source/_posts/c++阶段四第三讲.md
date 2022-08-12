---
title: c++阶段四第三讲
date: 2022-03-03 10:16:14
tags: [教材,阶段四]
categories: c++
---

# 第三讲

## IP地址

IP地址（Internet Protocol Address），缩写为IP Adress，是一种在Internet上的给主机统一编址的地址格式，也称为网络协议（IP协议）地址。它为互联网上的每一个网络和每一台主机分配一个逻辑地址，常见的IP地址，分为IPv4与IPv6两大类，当前广泛应用的是IPv4，目前IPv4几乎耗尽，下一阶段必然会进行版本升级到IPv6；如无特别注明，一般我们讲的的IP地址所指的是IPv4。

ip地址分为五类A、B、C、D、E，其中A类、B类和C类属于基本类，D类用于多播发送，E类属于保留类。

| **类型** | **范围**                  |
| -------- | ------------------------- |
| A类      | 0.0.0.0~127.255.255.255   |
| B类      | 128.0.0.0~191.255.255.255 |
| C类      | 192.0.0.0~223.255.255.255 |
| D类      | 224.0.0.0~239.255.255.255 |
| E类      | 240.0.0.0~247.255.255.255 |

`127.0.0.1`：本机地址

`192.168.137.*`：共享热点网段地址

在`cmd`控制台中写入`ipconfig`可以查看电脑的**IP地址**

## 套接字

`socket`:用于电脑之间的连接，通信。

适用于windows的套接字叫做`Winsocket`

在c++中想要使用需要导入头文件`WinSock2.h`

```c++
#include <WinSock2.h>
#pragma comment(lib,"ws2_32.lib")
```

初始化socket

```c++
WSADATA wsd;
WSAStartup(MAKEWORD(2, 2), &wsd);
```

socket函数

```c++
SOCKET socket(int af, int type, int protocol);
```

| name     | 作用                                                         |
| -------- | ------------------------------------------------------------ |
| af       | 一个地址家族。通常为AF_INET。                                |
| type     | 套接字类型。如果为SOCK_STREAM，表示创建面向连接的流式套接字;为SOCK_DGRAM，表示创建面向无连接的数据报套接字;为SOCK_RAW，表示创建原始套接字。对于这些值，用户可以在 Winsock2.h头文件中找到。 |
| protocol | 套接口所用的协议。如果用户不指定，可以设置为0。              |
| 返回值   | 函数返回值是创建的套接字控制权。                             |

bind函数

该函数用于将套接字绑定到指定的端口和地址上。语法如下 :

```c++
int bind(SOCKET s, const struct sockaddr FAR* name, int namelen);
```

| name    | 作用                                                     |
| ------- | -------------------------------------------------------- |
| s       | 套接字标识                                               |
| name    | 一个sockaddr结构指针。该结构中包含了要结合的地址和端口号 |
| namelen | 确定name缓冲区的长度                                     |
| 返回值  | 如果函数执行成功，返回值为0，否则返回SOCKET_ERROR。      |

listen函数

该函数用于将套接字设置为监听模式。对于流式套接字，必须处于监听模式才能够接收客户端套接字的连接。语法如下 :

```c++
int listen(SOCKET s, int backlog);
```

| name    | 作用                                                         |
| ------- | ------------------------------------------------------------ |
| s       | 套接字标识                                                   |
| backlog | 等待连接的最大队列长度。例如，如果backlog被设置为2，此时有3个客户端同时发出连接请求，那么前两个客户端连接会放置在等待队列中，第3个客户端会得到错误信息。 |

accept函数

该函数用于接受客户端的连接。在流式套接字中，套接字处于监听状态才能接受客户端的连接。语法如下 :

```c++
SOCKET accept(SOCKET s, struct sockaddr FAR* addr, int FAR* addrlen);
```

| name    | 作用                                                         |
| ------- | ------------------------------------------------------------ |
| s       | 是一个套接字，它应处于监听状态。                             |
| addr    | 是一个sockaddr_in结构指针，包含一组客户端的端口号、IP地址等信息。 |
| addrlen | 用于接收参数addr的长度。                                     |
| 返回值  | 一个新的套接字，它对应于已经接受的客户端连接，对于该客户端的所有后续操作，都应使用这个新的套接字。 |

closesocket函数

该函数用于关闭套接字。语法如下 : 

```c++
int closesocket(SOCKET S);
```

| name | 作用                                                         |
| ---- | ------------------------------------------------------------ |
| s    | 标识一个套接字,如果参数s设置为SO_DONTLINGER选项，则调用该函数后会立即返回，但此时如果有数据尚未传送完毕，会继续传递数据，然后才关闭套接字。 |

connect函数

该函数用于发送一个连接请求。语法如下 :

```c++
int connect(SOCKET s, const struct sockaddr FAR* name, int namelen);
```

| name    | 作用                                                         |
| ------- | ------------------------------------------------------------ |
| s       | 是一个套接字。                                               |
| name    | 套接字s想要连接的主机地址和端口号。                          |
| namelen | name缓冲区的长度。                                           |
| 返回值  | 如果函数执行成功，返回值为0，否则返回SOCKET_ERROR。用户可以通过WSAGETLASTERROR得到其错误描述。 |

htons函数

该函数用于设置连接端口号

```c++
u_short htons(u_short hostshort);
```

inet_addr函数

该函数用于设置连接的ip地址

```c++
unsigned long inet_addr(const char FAR* cp);
```

| name | 作用                |
| ---- | ------------------- |
| cp   | 一个P地址的字符串。 |

recv函数

该函数用于从面向连接的套接字中接收数据。语法如下 : 

```c++
int recv(SOCKET s.char FAR* buf, int len, int flags);
```

| name  | 作用                |
| ----- | ------------------- |
| s     | 一个套接字。        |
| buf   | 接收数据的缓冲区。  |
| len   | buf的长度。         |
| flags | 函数的调用方式。写0 |

send函数

该函数用于在面向连接方式的套接字间发送数据。语法如下 : 

```c++
int send(SOCKET s.const char FAR* buf, int len, int flags);
```

| name  | 作用                     |
| ----- | ------------------------ |
| s     | 一个套接字。             |
| buf   | 存放要发送数据的缓冲区。 |
| len   | 缓冲区长度。             |
| flags | 函数的调用方式,NULL      |

客户端

```c++
#include <WinSock2.h>
#include <windows.h>
#include <process.h>
#include <iostream>
#include <errno.h>
#include <sys/types.h>
#include <thread>
#include <stdio.h>
#include< WS2tcpip.h >
#include<cstring>
#pragma comment(lib,"ws2_32.lib")
#define _WINSOCK_DEPRECATED_NO_WARNINGS
using namespace std;
#pragma comment(lib,"ws2_32")
int main()
{
	// 初始化套接字
	WSADATA wsaDate;
	WSAStartup(MAKEWORD(2, 2), &wsaDate);
	SOCKET sockClient = socket(PF_INET, SOCK_STREAM, IPPROTO_TCP); // 创建一个socket端
	sockaddr_in aServer = {};
	aServer.sin_family = PF_INET;
	aServer.sin_addr.S_un.S_addr = inet_addr("192.168.137.42");//设置要连接的计算机的IP地址
	aServer.sin_port = htons(10000);  //设置要连接的计算机的端口号
	//建立连接并判断连接是否失败
	if (connect(sockClient, (SOCKADDR*)&aServer, sizeof(aServer)) == SOCKET_ERROR) {
		cout << "连接错误" << endl;
	}
	//connect(sockClient, (SOCKADDR*)&aServer, sizeof(aServer));
	int len;
	//接受服务器消息
	char b[1024];
	len = recv(sockClient, b, 1024, 0);//接收另一台计算机发送过来的数据
	cout << "服务端：";
	for (int s = 0; s < len; s++) {
		cout << b[s];
	}
	cout << "\n";
	string s = "000";
	while (1)
	{
		cout << "请输入你要发送的信息:\n";
		cin >> s;
		len = send(sockClient, s.c_str(), s.length(), NULL);//连接成功后发送数据
	}
	// 关闭套接字
	closesocket(sockClient);
	WSACleanup();
	return 0;
}
```



