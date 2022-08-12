---
title: 阶段二第十四讲
date: 2022-06-17 14:35:27
tags: [教材,阶段二]
categories: c++
---

# 第十四讲

会发现，方向键对应的整数分别是

上：72  下：80   左：75   右：77

但是由于按键检测本身的机制，方向键会检测两次，例如方向上键就是244一次，72一次，方向下键就是244一次，80一次。 244是多出来的一次，可以再单独使用_getch检测一次，就可以抵消掉244。

代码案例：

```c++
int a = '0';

  a = _getch();

  a = _getch();

  cout << a;
```



这个时候，每个方向键对应的整数分别就如下所示了：

上：72  下：80   左：75   右：77

```c++
#include <iostream>
#include <windows.h>
#include <conio.h>
using namespace std;
int main() {
	system("title 反应练习器！");
	int a = 0, b = 0, c = 0, sum = 0;
	double d = 0;
	srand(time(NULL));
	clock_t start, finish, start2, finish2;
	double time = 0;
	cout << "请选择挑战难度：\n" << "1:低   2:中  3:高\n";
	cin >> c;
	if (c == 1) {
		d = 2.5;
	}
	if (c == 2) {
		d = 1.1;
	}
	if (c == 3) {
		d = 0.8;
	}
	system("cls");
	cout << "准备开始倒计时！\n";
	Sleep(1000);
	system("color 6");
	cout << "3\n";
	Sleep(1000);
	system("color 2");
	cout << "2\n";
	Sleep(1000);
	system("color 4");
	cout << "1\n";
	Sleep(1000);
	cout << "开始！\n";
	Sleep(1000);
	system("cls");
	start = clock();
	while (time < 60) {
		b = (rand() % 4) + 1;
		if (b == 1) {
			system("color A");
			cout << "↑";
			start2 = clock();
			a = _getch();
			a = _getch();//上：72   下：80      左：75      右：77
			finish2 = clock();
			if (a == 72 && (double)(finish2 - start2) / CLOCKS_PER_SEC < d) {
				cout << "   正确！\n";
				sum++;
			}
			else {
				cout << "   错误！\n";
			}
		}
		if (b == 2) {
			system("color B");
			cout << "↓";
			start2 = clock();
			a = _getch();
			a = _getch();    //上：72   下：80      左：75      右：77
			finish2 = clock();
			if (a == 80 && (double)(finish2 - start2) / CLOCKS_PER_SEC < d) {
				cout << "   正确！\n";
				sum++;
			}
			else {
				cout << "   错误！\n";
			}
		}
		if (b == 3) {
			system("color C");
			cout << "←";
			start2 = clock();
			a = _getch();
			a = _getch();    //上：72   下：80      左：75      右：77
			finish2 = clock();
			if (a == 75 && (double)(finish2 - start2) / CLOCKS_PER_SEC < d) {
				sum++;
				cout << "   正确！\n";
			}
			else {
				cout << "   错误！\n";
			}
		}
		if (b == 4) {
			system("color D");
			cout << "→";
			start2 = clock();
			a = _getch();
			a = _getch();    //上：72   下：80      左：75      右：77
			finish2 = clock();
			if (a == 77 && (double)(finish2 - start2) / CLOCKS_PER_SEC < d) {
				cout << "   正确！\n";
				sum++;
			}
			else {
				cout << "   错误！\n";
			}
		}
		finish = clock();
		time = (double)(finish - start) / CLOCKS_PER_SEC;
	}
	cout << "你在一分钟内一共挑战成功" << sum << "个！";

}
```



```c++
﻿#include <iostream>
#include <Windows.h>
#include<conio.h>
#include<ctime>
using namespace std;
int main()
{
	srand(time(NULL));
	string zhi[] = { "红","黄","蓝","绿","黑","白" };
	int color[] = { 1,2,4,0 };
	clock_t start, finish;
	double totaltime = 0;
	int sum = 0;
	start = clock();
	int sum2 = 0;
	while (totaltime < 30)
	{
		int c = color[rand() % 4];
		SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | c);
		cout << zhi[rand() % 6] << endl;
		int a = _getch();

		// 检测按键
		switch (c)
		{
		case 0:
			if (a == 'w') {
				cout << "yes";
				Sleep(500);
				sum2++;
			}
			break;
		case 1:
			if (a == 'b') {
				cout << "yes";
				Sleep(500);
				sum2++;
			}
			break;
		case 2:
			if (a == 'g') {
				cout << "yes";
				Sleep(500);
				sum2++;
			}
			break;
		case 4:
			if (a == 'r') {
				cout << "yes";
				Sleep(500);
				sum2++;
			}
			break;
		default:
			break;
		}
		sum++;
		finish = clock();
		totaltime = (double)(finish - start) / CLOCKS_PER_SEC;
		system("cls");
	}
	cout << "你一共猜了" << sum << "你正确了" << sum2<<endl;
}
```

