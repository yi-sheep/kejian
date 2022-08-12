---
title: c++阶段三迷宫
date: 2021-11-04 09:22:38
tags: [教材,阶段三]
categories: c++
---

# 期中测试---迷宫

二维数组：

定义公式：

`数据类型 数组名[行大小][列大小];`

例子：

```c++
int a[3][3] = {
    {1,2,3},
    {6,5,4},
    {7,8,9},
};
```

`a[0][2]`的值是？

`a[2][1]`的值是？

`a[1][0]`的值是？

获取键盘事件：

`_getch();`

使用前要调用一个文件`conio.h`

例子：

```c++
#include <iostream>
#include <conio.h>
using namespace std;

int main()
{
	int a = _getch();
	if (a == 'w') {
		cout << "w";
	}
}
```

完成小练习：判断用户是否按下w、a、s、d这几个按键。

```c++
#include <iostream>
#include <conio.h>
using namespace std;

int main()
{
	int a = _getch();
	if (a == 'w') {
		cout << "w";
	}
	if (a == 'a') {
		cout << "a";
	}
	if (a == 's') {
		cout << "s";
	}
	if (a == 'd') {
		cout << "d";
	}
}
```

## 测试项目：

![](https://gitee.com/gaoxianglong/picgo/raw/master/img/%E8%BF%B7%E5%AE%AB%E6%BC%94%E7%A4%BA.gif)

```c++
#include <iostream>
#include <cstdio>
#include <Windows.h>
#include <conio.h>

//8*12
char a[50][50] = {
	"############",
	"#O#    #   #",
	"#   ## # # #",
	"#####    # #",
	"#     #### #",
	"# #####  # #",
	"#       ##  ",
	"############"
};

void Welcome()//欢迎界面 
{
	printf("\n\n           走 迷 宫");
	printf("\n\n        请按任意键开始");
	getch();
	system("cls");
}


int main()
{
	Welcome();
	int x = 1, y = 1;
	char ch;
	for (int i = 0; i <= 7; i++)
		puts(a[i]);
	while (1)
	{
		ch = getch();
		if (ch == 's')//下
		{
			if (a[x + 1][y] == ' ')
			{
				a[x][y] = ' ';
				x++;
				a[x][y] = 'O';
			}
		}
		else if (ch == 'w')//上
		{
			if (a[x - 1][y] == ' ')
			{
				a[x][y] = ' ';
				x--;
				a[x][y] = 'O';
			}
		}
		else if (ch == 'a')//左
		{
			if (a[x][y - 1] == ' ')
			{
				a[x][y] = ' ';
				y--;
				a[x][y] = 'O';
			}
		}
		else if (ch == 'd')//右
		{
			if (a[x][y + 1] == ' ')
			{
				a[x][y] = ' ';
				y++;
				a[x][y] = 'O';
			}
		}
		system("cls");
		for (int i = 0; i <= 7; i++)
			puts(a[i]);
		if (x == 6 && y == 11)
			break;
	}
	printf("你赢了！");
	Sleep(10000);
	return 0;
}
```

