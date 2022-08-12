---
title: c++阶段三第十一讲
date: 2021-11-24 11:25:16
tags: [教材,阶段三]
categories: c++
---

# 第十一讲

## 推箱子

![image-20211124114903912](https://gitee.com/gaoxianglong/picgo/raw/master/img/image-20211124114903912.png)

以前画地图的方式

```c++
#include <iostream>
#include <conio.h>
using namespace std;
char a[10][10] = {
	{'q','q','q','q','q','q','q','q','q','q'},
	{'q','q','q','q','q','q','q','q','q','q'},
	{'q','q','q','q','q','q','q','q','q','q'},
	{'q','q','q','q','q','q','q','q','q','q'},
	{'q','q','q','q','q','q','q','q','q','q'},
	{'q','q','q','q','q','q','q','q','q','q'},
	{'q','q','q','q','q','q','q','q','q','q'},
	{'q','q','q','q','q','q','q','q','q','q'},
	{'q','q','q','q','q','q','q','q','q','q'},
	{'q','q','q','q','q','q','q','q','q','q'}
};
void show() {
	for (int i = 0; i < 10; i++)
	{
		for (int j = 0; j < 10; j++) {
			cout << a[i][j];
		}
		cout << endl;
	}
}
int main()
{
	while (true)
	{
		if (_getch()) {
			system("cls");
			show();
		}
	}
}
```

定点更新地图

```c++
#include <Windows.h>
// 获取控制台输出权限
HANDLE hout = GetStdHandle(STD_OUTPUT_HANDLE);
```

移动光标

```c++
// 将光标移动到指定的位置
SetConsoleCursorPosition(hout, { x,y });
```

边框绘制

```c++
#include <iostream>
#include <conio.h>
#include <Windows.h>
using namespace std;
// 创建人物坐标，地图坐标变量
short r_x = 0, r_y = 0, m_x = 20, m_y = 5;
// 获取控制台输出权限
HANDLE hout = GetStdHandle(STD_OUTPUT_HANDLE);
// 将光标移动到某一个坐标
void gotoxy(short x, short y) {
	// 将光标移动到指定的位置
	SetConsoleCursorPosition(hout, { x,y });
}
void show() {
	int i = 0;
	for (i = m_x; i < 40; i += 2)
	{
		gotoxy(i, m_y); // 20 22 24 26 28 30
		cout << "■";
		gotoxy(i, 14);
		cout << "■";
	}
	for (i = m_y + 1; i < 15; i++) {
		gotoxy(m_x, i);
		cout << "■";
		gotoxy(38, i);
		cout << "■";
	}

}
int main()
{
	while (true)
	{
		if (_getch()) {
			show();
		}
	}

}
```

关掉光标显示

```c++
//隐藏光标
void HideCursor()
{
    HANDLE handle = GetStdHandle(STD_OUTPUT_HANDLE);
    CONSOLE_CURSOR_INFO CursorInfo;
    GetConsoleCursorInfo(handle, &CursorInfo);//获取控制台光标信息
    CursorInfo.bVisible = false; //隐藏控制台光标
    SetConsoleCursorInfo(handle, &CursorInfo);//设置控制台光标状态
}
```



### 画地图

```c++
#include<iostream>
using namespace std;
int row, col;
int map[8][9] = {
{ 0, 0, 1, 1, 1, 1, 1, 0, 0 },
{ 0, 1, 1, 0, 0, 2, 1, 0, 0 },
{ 0, 1, 0, 4, 4, 0, 1, 0, 0 },
{ 0, 1, 0, 3, 2, 1, 1, 0, 0 },
{ 0, 1, 1, 1, 1, 1, 0, 0, 0 },
{ 0, 0, 0, 0, 0, 0, 0, 0, 0 },
{ 0, 0, 0, 0, 0, 0, 0, 0, 0 },
{ 0, 0, 0, 0, 0, 0, 0, 0, 0 }
};
void init()
{
	printf("*************************\n");
	printf("推箱子小游戏\n");
	printf("基础操作：w s a d \n");
	printf("*************************\n");
}
void showMap()
{
	init();//操作介绍
		   //遍历数组，打印形状
	for (int i = 0; i < 8; ++i)			 //利用多维数组map绘制地图
	{
		for (int j = 0; j < 9; ++j)
			switch (map[i][j])
			{
			case 0:
				cout<<"  ";//空地0
				break;
			case 1:
				cout << "■";//墙1
				break;
			case 2:
				cout << "○";//目的地2
				break;
			case 3:
				cout << "♀";//人3
				break;
			case 4:
				cout << "□";//箱子4
				break;
			default:
				break;
			}
		cout << endl;
	}
}
int main()
{
	showMap();
	return 0;
}


```

```
→↑↓←←↑→↑→↓
```



