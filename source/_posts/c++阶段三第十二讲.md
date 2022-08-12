---
title: c++阶段三第十二讲
date: 2021-12-03 09:55:34
tags: [教材,阶段三]
categories: c++
---

# 第十二讲

## 上节课的代码

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

## 角色移动

```c++
#include<iostream>
#include <conio.h>
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
	for (int i = 0; i < 8; ++i)			 //利用多维数组map绘制地图
	{
		for (int j = 0; j < 9; ++j)
			switch (map[i][j])
			{
			case 0:
				cout << "  ";//空地0
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
void move() {
	int c = _getch();
	switch (c)
	{
	case 'w':
		map[row][col] = 0;
		map[row-1][col] = 3;
		row--;
		break;
	case 's':
		map[row][col] = 0;
		map[row + 1][col] = 3;
		row++;
		break;
	case 'a':
		map[row][col] = 0;
		map[row][col-1] = 3;
		col--;
		break;
	case 'd':
		map[row][col] = 0;
		map[row][col+1] = 3;
		col++;
		break;
	default:
		break;
	}
}
int main()
{
	init();//操作介绍
		   //遍历数组，打印形状
	row = 3;
	col = 3;
	while (true)
	{
		showMap();
		move();
	}
	
	return 0;
}
```

边界问题

```c++
#include<iostream>
#include <conio.h>
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
	for (int i = 0; i < 8; ++i)			 //利用多维数组map绘制地图
	{
		for (int j = 0; j < 9; ++j)
			switch (map[i][j])
			{
			case 0:
				cout << "  ";//空地0
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
void move() {
	int c = _getch();
	switch (c)
	{
	case 'w':
		if (row-1 >= 0 && row-1 < 8) {
			map[row][col] = 0;
			map[row - 1][col] = 3;
			row--;
		}
		break;
	case 's':
		if (row+1 >= 0 && row+1 < 8) {
			map[row][col] = 0;
			map[row + 1][col] = 3;
			row++;
		}
		break;
	case 'a':
		if (col-1 >= 0 && col-1 < 9) {
			map[row][col] = 0;
			map[row][col - 1] = 3;
			col--;
		}
		break;
	case 'd':
		if (col+1 >= 0 && col+1 < 9) {
			map[row][col] = 0;
			map[row][col + 1] = 3;
			col++;
		}
		break;
	default:
		break;
	}
}
int main()
{
	init();//操作介绍
		   //遍历数组，打印形状
	row = 3;
	col = 3;
	while (true)
	{
		showMap();
		move();
	}

	return 0;
}
```

第二个方法

```c++
#include<iostream>
#include <conio.h>
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
	for (int i = 0; i < 8; ++i)			 //利用多维数组map绘制地图
	{
		for (int j = 0; j < 9; ++j)
			switch (map[i][j])
			{
			case 0:
				cout << "  ";//空地0
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
void move() {
	int c = _getch();
	switch (c)
	{
	case 'w':
		if (map[row-1][col]==0) {
			map[row][col] = 0;
			map[row - 1][col] = 3;
			row--;
		}
		break;
	case 's':
		if (map[row+1][col]==0) {
			map[row][col] = 0;
			map[row + 1][col] = 3;
			row++;
		}
		break;
	case 'a':
		if (map[row][col-1]==0) {
			map[row][col] = 0;
			map[row][col - 1] = 3;
			col--;
		}
		break;
	case 'd':
		if (map[row][col+1]==0) {
			map[row][col] = 0;
			map[row][col + 1] = 3;
			col++;
		}
		break;
	default:
		break;
	}
}
int main()
{
	init();//操作介绍
		   //遍历数组，打印形状
	row = 3;
	col = 3;
	while (true)
	{
		showMap();
		move();
		system("cls");
	}

	return 0;
}
```

