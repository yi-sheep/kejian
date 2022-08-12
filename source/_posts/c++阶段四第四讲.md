---
title: c++阶段四第四讲
date: 2022-03-10 09:03:45
tags: [教材,阶段四]
categories: c++
---

# 第四讲

服务端

```c++
#include <WinSock2.h>
#include <errno.h>
#include <sys/types.h>
#include <thread>
#include <stdio.h>
#include <iostream>
#include <WS2tcpip.h>
#include<cstring>
#include<stdlib.h>
#include<Windows.h>
#pragma comment(lib,"ws2_32")
#pragma comment(lib,"ws2_32.lib")
using namespace std;
#define _WINSOCK_DEPRECATED_NO_WARNINGS
int main()
{
	WSADATA ws = {};
	WSAStartup(MAKEWORD(2, 2), &ws);
	SOCKET sockServer = socket(PF_INET, SOCK_STREAM, IPPROTO_TCP);
	//SOCKET sockServer = socket(PF_INET, SOCK_DGRAM, IPPROTO_UDP);
	sockaddr_in adServer = {};
	adServer.sin_family = PF_INET;
	adServer.sin_addr.S_un.S_addr = inet_addr("192.168.137.1");//设置服务器电脑的IP地址 
	adServer.sin_port = htons(10000);//设置接收数据的端口号 
	int bin = bind(sockServer, (SOCKADDR*)&adServer, sizeof(adServer));//启动监听程序 
	if (bin != 0) {
		cout << "启动监听失败！" << endl;
	}
	listen(sockServer, 2);//等待另一台计算机连接 
	SOCKET sock = {};
	SOCKADDR adClient = {};
	int nSzie = sizeof(adClient);
	sock = accept(sockServer, &adClient, &nSzie);
	if (sock != INVALID_SOCKET) {  //判断连接是否成功 
		cout << "连接成功" << endl;
	}
	else {
		printf("连接失败");
	}
	string str = "连接成功";
	send(sock, str.c_str(), str.length(), NULL);  //发送字符串变量str给另一台计算机 
	while (1)
	{
		char buf[1024];
		int len = recv(sock, buf, 1024, 0); //接收另一台计算机发送的数据并保存到buf字符数组里 
		cout << "客户端：";
		for (int s = 0; s < len; s++) {    //输出buf数组 
			cout << buf[s];
		}
		cout << endl;

	}
	closesocket(sockServer);
	closesocket(sock);
	WSACleanup();

	return 0;
}
```

