---
title: c++阶段三第十三讲
date: 2021-12-12 11:23:37
tags: [教材,阶段三]
categories: c++
---

# 第十三讲

## 推箱子

箱子类

```c++
class Box {
public:
	int box_x, box_y;
	void printBox(int x, int y) {
		box_x = x;
		box_y = y;
		gotoxy(x, y);
		cout << "□";
	}
	void printTarget(int x, int y) {
		box_x = x;
		box_y = y;
		gotoxy(x, y);
		cout << "○";
	}
	/// <summary>
	/// 检测是否碰撞
	/// </summary>
	/// <param name="x">箱子的x</param>
	/// <param name="y">箱子的y</param>
	/// <param name="bl">箱子容器引用</param>
	/// <param name="tl">目的地容器引用</param>
	/// <returns>是否移动</returns>
	int isCollision(int x, int y, vector<Box>& bl, vector<Box>& tl)
	{
		for (int i = 0; i < bl.size(); i++)
		{
			if (x == bl[i].box_x && y == bl[i].box_y) {
				return 0;
			}
			if (x == tl[i].box_x && y == tl[i].box_y) {
				gotoxy(x, y);
				cout << "  ";
				return 1;
			}
			if (x <= 20 || x >= 38 || y <= 5 || y >= 14) {
				return 1;
			}
		}
		return 0;
	}
	/// <summary>
	/// 箱子移动
	/// </summary>
	/// <param name="d">移动方向</param>
	/// <param name="bl">箱子容器引用</param>
	/// <param name="tl">目的地容器引用</param>
	/// <returns>是否移动成功</returns>
	bool BoxMove(char d, vector<Box>& bl, vector<Box>& tl)
	{
		switch (d)
		{
		case 'w':
			if (!isCollision(box_x, box_y - 1, bl, tl)) {
				gotoxy(box_x, box_y);
				cout << "  ";
				gotoxy(box_x, --box_y);
				cout << "□";
				return 1;
			}
			break;
		case 'a':
			if (!isCollision(box_x - 2, box_y, bl, tl)) {
				gotoxy(box_x, box_y);
				cout << "  ";
				gotoxy(box_x - 2, box_y);
				box_x -= 2;
				cout << "□";
				return 1;
			}
			break;
		case 's':
			if (!isCollision(box_x, box_y + 1, bl, tl)) {
				gotoxy(box_x, box_y);
				cout << "  ";
				gotoxy(box_x, ++box_y);
				cout << "□";
				return 1;
			}
			break;
		case 'd':
			if (!isCollision(box_x + 2, box_y, bl, tl)) {
				gotoxy(box_x, box_y);
				cout << "  ";
				gotoxy(box_x + 2, box_y);
				box_x += 2;
				cout << "□";
				return 1;
			}
			break;
		default:
			break;
		}
		return 0;
	}
};
```

人物类

```c++
class User {
public:
	int u_x, u_y;
	char direction;
	void printUser(int x, int y) {
		u_x = x;
		u_y = y;
		gotoxy(x, y);
		cout << "♀";
	}
	/// <summary>
	/// 检测是否碰撞
	/// </summary>
	/// <param name="x">玩家的x</param>
	/// <param name="y">玩家的y</param>
	bool isCollision(int x, int y)
	{
		for (int i = 0; i < BoxList.size(); i++)
		{
			if (x == BoxList[i].box_x && y == BoxList[i].box_y) {
				return 0;
			}
			if (x == TarList[i].box_x && y == TarList[i].box_y) {
				return 0;
			}
			if (x <= 20 || x >= 38 || y <= 5 || y >= 14) {
				return 1;
			}
		}
		return 0;
	}
	/// <summary>
	/// 判断目标地是否是箱子
	/// </summary>
	/// <param name="x">人物目标x</param>
	/// <param name="y">人物目标y</param>
	/// <returns></returns>
	bool isBlock(int x, int y)
	{
		for (int i = 0; i < BoxList.size(); i++)
		{
			if (x == BoxList[i].box_x && y == BoxList[i].box_y) {
				if (BoxList[i].BoxMove(direction,BoxList, TarList))
				{
					return 1;
				}
			}
		}
		return 1;
	}
	/// <summary>
	/// 人物移动
	/// </summary>
	void move() {
		direction = _getch();
		switch (direction)
		{
		case 'w':
			if (!isCollision(u_x, u_y - 1)) {
				if (isBlock(u_x, u_y - 1)) {
					gotoxy(u_x, u_y);
					cout << "  ";
					gotoxy(u_x, --u_y);
					cout << "♀";
				}
			}
			break;
		case 'a':
			if (!isCollision(u_x - 2, u_y)) {
				if (isBlock(u_x-2, u_y)) {
					gotoxy(u_x, u_y);
					cout << "  ";
					gotoxy(u_x - 2, u_y);
					u_x -= 2;
					cout << "♀";
				}
			}
			break;
		case 's':
			if (!isCollision(u_x, u_y + 1)) {
				if (isBlock(u_x, u_y + 1)) {
					gotoxy(u_x, u_y);
					cout << "  ";
					gotoxy(u_x, ++u_y);
					cout << "♀";
				}

			}
			break;
		case 'd':
			if (!isCollision(u_x + 2, u_y)) {
				if (isBlock(u_x + 2, u_y)) {
					gotoxy(u_x, u_y);
					cout << "  ";
					gotoxy(u_x + 2, u_y);
					u_x += 2;
					cout << "♀";
				}
			}
			break;
		default:
			break;
		}
	}
};
```

显示地图

```c++
void show() {
	// 20,5        38,5
	// 20,14       38,15
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
	Box b;
	b.printTarget(24, 6);
	TarList.push_back(b);
	b.printTarget(28, 6);
	TarList.push_back(b);
	b.printTarget(32, 6);
	TarList.push_back(b);
	b.printBox(24, 10);
	BoxList.push_back(b);
	b.printBox(28, 10);
	BoxList.push_back(b);
	b.printBox(32, 10);
	BoxList.push_back(b);
	User u;
	u.printUser(28, 12);
	UserList.push_back(u);
}
```

检测是否按下按键

```c++
int main()
{
	HideCursor();
	show();

	while (true)
	{
		if (_kbhit()) {
			UserList[0].move();
		}
	}
}
```

