---
title: 阶段五第三讲
date: 2022-03-03 10:16:29
tags: [教材,阶段五]
categories: c++
---

# 五子棋

上节课的代码

```c++
#include <iostream>
using namespace std;
char qizi[20][20];
void init() {
	for (int i = 0; i < 20; i++) {
		for (int j = 0; j < 20; j++)
		{
			qizi[i][j] = ' ';
		}
	}
}
void huaqipan() {
	system("cls");
	cout << "\n\n";
	cout << "最新棋盘形势：\n";
	for (int i = 0; i <= 20; i++) {
		if (i == 0) {
			cout << "  | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |10 |11 |12 |13 |14 |15 |16 |17 |18 |19 |20 |\n";
		}
		else if (i < 10) {
			cout << " " << i << "| ";
			for (int t = 0; t < 20; t++) {
				cout << qizi[i - 1][t] << " | ";
			}
			cout << "\n";
		}
		else {
			cout << i << "| ";
			for (int t = 0; t < 20; t++) {
				cout << qizi[i - 1][t] << " | ";
			}
			cout << "\n";
		}
		cout << " -|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|\n";
	}
}
void xiaqi() {
	while (true)
	{
		int x = 0;
		int y = 0;
		while (true)
		{
			cout << "玩家1" << endl;
			cout << "请输入行";
			cin >> x;
			cout << "请输入列";
			cin >> y;
			if ((x >= 1 && x <= 20) && (y >= 1 && y <= 20) && (qizi[x - 1][y - 1] == ' ')) {
				qizi[x - 1][y - 1] = 'x';
				huaqipan();
				break;
			}
		}

		while (true)
		{
			cout << "玩家2" << endl;
			cout << "请输入行";
			cin >> x;
			cout << "请输入列";
			cin >> y;
			if ((x >= 1 && x <= 20) && (y >= 1 && y <= 20) && (qizi[x - 1][y - 1] == ' ')) {
				qizi[x - 1][y - 1] = 'o';
				huaqipan();
				break;
			}
		}
	
	}

}
int main()
{
	init();
	huaqipan();
	xiaqi();
}
```

## 判断输赢

```c++
#include <iostream>
using namespace std;
char qizi[20][20];
void init() {
	for (int i = 0; i < 20; i++) {
		for (int j = 0; j < 20; j++)
		{
			qizi[i][j] = ' ';
		}
	}
}
void huaqipan() {
	system("cls");
	cout << "\n\n";
	cout << "最新棋盘形势：\n";
	for (int i = 0; i <= 20; i++) {
		if (i == 0) {
			cout << "  | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |10 |11 |12 |13 |14 |15 |16 |17 |18 |19 |20 |\n";
		}
		else if (i < 10) {
			cout << " " << i << "| ";
			for (int t = 0; t < 20; t++) {
				cout << qizi[i - 1][t] << " | ";
			}
			cout << "\n";
		}
		else {
			cout << i << "| ";
			for (int t = 0; t < 20; t++) {
				cout << qizi[i - 1][t] << " | ";
			}
			cout << "\n";
		}
		cout << " -|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|\n";
	}
}
bool pdsy(char c) {
	int i, j, t, s = 0;
	for (i = 0; i < 20; i++) {
		for (j = 0; j < 20; j++) {
			if (s == 5) {
				return 1;
			}
			else if (qizi[i][j] == c||qizi[j][i]==c) {
				s++;
			}
			else {
				s = 0;
			}
		}
	}
	s = 0;
	for (i = 0; i < 16; i++) {
		for (j = 0; j < 16; j++) {
			for (t = 0; t < 5; t++) {
				if (s == 5) {
					return 1;
				}
				else if (qizi[i + t][j + t] == c) {
					s++;
				}
				else {
					s = 0;
				}
			}
		}
	}
	s = 0;
	for (i = 4; i < 20; i++) {
		for (j = 0; j < 20; j++) {
			for (t = 0; t < 5; t++) {
				if (s == 5) {
					return 1;
				}
				else if (qizi[i - t][j + t] == c) {
					s++;
				}
				else {
					s = 0;
				}
			}
		}
	}
	return 0;
}
int xiaqi() {
	while (true)
	{
		int x = 0;
		int y = 0;
		while (true)
		{
			cout << "玩家1" << endl;
			cout << "请输入行";
			cin >> x;
			cout << "请输入列";
			cin >> y;
			if ((x >= 1 && x <= 20) && (y >= 1 && y <= 20) && (qizi[x - 1][y - 1] == ' ')) {
				qizi[x - 1][y - 1] = 'x';
				huaqipan();
				if (pdsy('x')) {
					return 1;
				}
				break;
			}
		}

		while (true)
		{
			cout << "玩家2" << endl;
			cout << "请输入行";
			cin >> x;
			cout << "请输入列";
			cin >> y;
			if ((x >= 1 && x <= 20) && (y >= 1 && y <= 20) && (qizi[x - 1][y - 1] == ' ')) {
				qizi[x - 1][y - 1] = 'o';
				huaqipan();
				if (pdsy('o')) {
					return 2;
				}
				break;
			}
		}
	}

}
int main()
{
	init();
	huaqipan();
	int a = xiaqi();
	if (a == 1) {
		cout << "玩家1获胜";
	}
	else if (a == 2) {
		cout << "玩家2获胜";
	}

}
```

