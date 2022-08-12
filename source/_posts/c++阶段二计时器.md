---
title: c++阶段二计时器
date: 2021-10-28 10:20:30
tags: [教材,阶段二] 
categories: c++
---



# 第七讲

我们所学习的C++中有很多便于使用的函数，这些函数都是其它人为了便于使用而创造的，我们可以在自己的项目中直接调用这些函数，那么本节课我们就一起来看一些有趣又实用的函数。

首先要调用一个头文件

`Windows.h`

## Sleep()

```c++
for(int i = 0;i<10;i++){
cout<<i;
Sleep(1000);
}
```

作用：

这个函数其实就是让我们的程序在这个地方等待多少毫秒。单位是毫秒。

## system()

```c++
for(int i = 0;i<10;i++){
system(“cls”);
cout<<i;
Sleep(1000);
}
```

作用：

这个函数其实是让我们的程序在这个地方清空控制台上的东西。

练习：

倒计时30秒的小项目

```c++
cout << "30秒倒计时开始" << endl;
for (int i = 30; i > -1; i--) {
	system("cls");
	cout << i;
	Sleep(100);
}
cout << "\a\n时间到";
```

## 项目

![](https://gitee.com/gaoxianglong/picgo/raw/master/img/%E8%AE%A1%E6%97%B6%E5%99%A81%E6%BC%94%E7%A4%BA.gif)

```c++
#include<iostream>
#include<Windows.h>
using namespace std;
int main()
{
	int fen = 0;
	int miao = 0;
	int kongzhifen = 0;
	int kongzhimiao = 0;
	cout << "感谢您选择华为牌计时器!\n";
	cout << "请输入您需要计时的分钟数：";
	cin >> kongzhifen;
	cout << "请输入您需要计时的秒数：";
	cin >> kongzhimiao;
	for (fen = 0; fen <= kongzhifen; fen++)
	{
		if (fen == kongzhifen) {
			for (miao = 0; miao < kongzhimiao; miao++)
			{
				Sleep(1000);
				system("cls");
				cout << fen << ":" << miao << "\n";
			}
		}
		else {
			for (miao = 0; miao < 60; miao++)
			{
				Sleep(1000);
				system("cls");
				cout << fen << ":" << miao << "\n";
			}
		}
	}
	Sleep(1000);
	system("cls");
	cout << fen - 1 << ":" << miao << "\n";
	cout << "时间到！\n感谢您的使用！欢迎下次再来！\n";
}
```

