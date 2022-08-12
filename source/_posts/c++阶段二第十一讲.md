---
title: c阶段二第十一讲
date: 2021-11-24 10:39:53
tags: [教材,阶段二]
categories: c++
---

# 第十一讲

最新的代码

```c++
#include <iostream>
using namespace std;
char qipan[3][3] = {
    {' ',' ',' '},
    {' ',' ',' '},
    {' ',' ',' '},
};
void huatu() {
    for (int i = 0; i < 8; i++) {
        if (i == 0) {
            cout << " | 1 | 2 | 3 |" << endl;
        }
        else if (i == 1 || i == 3 || i == 5 || i == 7) {
            cout << "-|---|---|---|" << endl;
        }
        else if (i == 2) {
            cout << "1| " << qipan[0][0] << " | " << qipan[0][1] << " | " << qipan[0][2] << " |" << endl;
        }
        else if (i == 4) {
            cout << "2| " << qipan[1][0] << " | " << qipan[1][1] << " | " << qipan[1][2] << " |" << endl;
        }
        else if (i == 6) {
            cout << "3| " << qipan[2][0] << " | " << qipan[2][1] << " | " << qipan[2][2] << " |" << endl;
        }
    }
}
int main()
{
    int x, y;
	while (true)
	{
		huatu();
		while (true) {
			cout << "玩家1：" << endl;
			cout << "请输入x：";
			cin >> x;
			cout << "请输入y：";
			cin >> y;
			x--;
			y--;
			if (x > -1 && x < 3 && y>-1 && y < 3) {
				if (qipan[x][y] == ' ') {
					break;
				}
				else {
					cout << "这个位置已经有棋子了" << endl;
				}
			}
			else {
				cout << "棋子超出范围" << endl;
			}
		}

		qipan[x][y] = 'o';
		huatu();
		while (true) {
			cout << "玩家2：" << endl;
			cout << "请输入x：";
			cin >> x;
			cout << "请输入y：";
			cin >> y;
			x--;
			y--;
			if (x > -1 && x < 3 && y>-1 && y < 3) {
				if (qipan[x][y] == ' ') {
					break;
				}
				else {
					cout << "这个位置已经有棋子了" << endl;
				}
			}
			else {
				cout << "棋子超出范围" << endl;
			}
		}

		qipan[x][y] = 'x';
	}

}
```

判断输赢

```c++
void shuyin() {
	for (int i = 0; i < 3; i++) {
		if (qipan[i][0] == 'o' && qipan[i][1] == 'o' && qipan[i][2] == 'o') {
			cout << "玩家1获胜" << endl;
		}
		if (qipan[0][i] == 'o' && qipan[1][i] == 'o' && qipan[2][i] == 'o') {
			cout << "玩家1获胜" << endl;
		}
	}
	if (qipan[0][0] == 'o' && qipan[1][1] == 'o' && qipan[2][2] == 'o') {
		cout << "玩家1获胜" << endl;
	}
	if (qipan[0][2] == 'o' && qipan[1][1] == 'o' && qipan[2][0] == 'o') {
		cout << "玩家1获胜" << endl;
	}

	for (int i = 0; i < 3; i++) {
		if (qipan[i][0] == 'x' && qipan[i][1] == 'x' && qipan[i][2] == 'x') {
			cout << "玩家1获胜" << endl;
		}
		if (qipan[0][i] == 'x' && qipan[1][i] == 'x' && qipan[2][i] == 'x') {
			cout << "玩家1获胜" << endl;
		}
	}
	if (qipan[0][0] == 'x' && qipan[1][1] == 'x' && qipan[2][2] == 'x') {
		cout << "玩家1获胜" << endl;
	}
	if (qipan[0][2] == 'x' && qipan[1][1] == 'x' && qipan[2][0] == 'x') {
		cout << "玩家1获胜" << endl;
	}
}
int main()
{
	int x, y;
	huatu();
	while (true)
	{
		
		while (true) {
			cout << "玩家1：" << endl;
			cout << "请输入x：";
			cin >> x;
			cout << "请输入y：";
			cin >> y;
			x--;
			y--;
			if (x > -1 && x < 3 && y>-1 && y < 3) {
				if (qipan[x][y] == ' ') {
					break;
				}
				else {
					cout << "这个位置已经有棋子了" << endl;
				}
			}
			else {
				cout << "棋子超出范围" << endl;
			}
		}

		qipan[x][y] = 'o';
		huatu();
		shuyin();
		while (true) {
			cout << "玩家2：" << endl;
			cout << "请输入x：";
			cin >> x;
			cout << "请输入y：";
			cin >> y;
			x--;
			y--;
			if (x > -1 && x < 3 && y>-1 && y < 3) {
				if (qipan[x][y] == ' ') {
					break;
				}
				else {
					cout << "这个位置已经有棋子了" << endl;
				}
			}
			else {
				cout << "棋子超出范围" << endl;
			}
		}
		qipan[x][y] = 'x';
		huatu();
		shuyin();

	}

}
```

胜利后停掉比赛

```c++
bool shuyin() {
	for (int i = 0; i < 3; i++) {
		if (qipan[i][0] == 'o' && qipan[i][1] == 'o' && qipan[i][2] == 'o') {
			cout << "玩家1获胜" << endl;
			return 1;
		}
		if (qipan[0][i] == 'o' && qipan[1][i] == 'o' && qipan[2][i] == 'o') {
			cout << "玩家1获胜" << endl;
			return 1;
		}
	}
	if (qipan[0][0] == 'o' && qipan[1][1] == 'o' && qipan[2][2] == 'o') {
		cout << "玩家1获胜" << endl;
		return 1;
	}
	if (qipan[0][2] == 'o' && qipan[1][1] == 'o' && qipan[2][0] == 'o') {
		cout << "玩家1获胜" << endl;
		return 1;
	}

	for (int i = 0; i < 3; i++) {
		if (qipan[i][0] == 'x' && qipan[i][1] == 'x' && qipan[i][2] == 'x') {
			cout << "玩家2获胜" << endl;
			return 1;
		}
		if (qipan[0][i] == 'x' && qipan[1][i] == 'x' && qipan[2][i] == 'x') {
			cout << "玩家2获胜" << endl;
			return 1;
		}
	}
	if (qipan[0][0] == 'x' && qipan[1][1] == 'x' && qipan[2][2] == 'x') {
		cout << "玩家2获胜" << endl;
		return 1;
	}
	if (qipan[0][2] == 'x' && qipan[1][1] == 'x' && qipan[2][0] == 'x') {
		cout << "玩家2获胜" << endl;
		return 1;
	}
	return 0;
}
int main()
{
	int x, y;
	huatu();
	while (true)
	{
		
		while (true) {
			cout << "玩家1：" << endl;
			cout << "请输入x：";
			cin >> x;
			cout << "请输入y：";
			cin >> y;
			x--;
			y--;
			if (x > -1 && x < 3 && y>-1 && y < 3) {
				if (qipan[x][y] == ' ') {
					break;
				}
				else {
					cout << "这个位置已经有棋子了" << endl;
				}
			}
			else {
				cout << "棋子超出范围" << endl;
			}
		}

		qipan[x][y] = 'o';
		huatu();
		if (shuyin()) {
			break;
		}
		while (true) {
			cout << "玩家2：" << endl;
			cout << "请输入x：";
			cin >> x;
			cout << "请输入y：";
			cin >> y;
			x--;
			y--;
			if (x > -1 && x < 3 && y>-1 && y < 3) {
				if (qipan[x][y] == ' ') {
					break;
				}
				else {
					cout << "这个位置已经有棋子了" << endl;
				}
			}
			else {
				cout << "棋子超出范围" << endl;
			}
		}
		qipan[x][y] = 'x';
		huatu();
		if (shuyin()) {
			break;
		}

	}

}
```

优化代码

```c++
bool shuyin(char a) {
	for (int i = 0; i < 3; i++) {
		if (qipan[i][0] == a && qipan[i][1] == a && qipan[i][2] == a) {
			return 1;
		}
		if (qipan[0][i] == a && qipan[1][i] == a && qipan[2][i] == a) {
			return 1;
		}
	}
	if (qipan[0][0] == a && qipan[1][1] == a && qipan[2][2] == a) {
		return 1;
	}
	if (qipan[0][2] == a && qipan[1][1] == a && qipan[2][0] == a) {
		return 1;
	}
	return 0;
}
int main()
{
	int x, y;
	huatu();
	while (true)
	{
		
		while (true) {
			cout << "玩家1：" << endl;
			cout << "请输入x：";
			cin >> x;
			cout << "请输入y：";
			cin >> y;
			x--;
			y--;
			if (x > -1 && x < 3 && y>-1 && y < 3) {
				if (qipan[x][y] == ' ') {
					break;
				}
				else {
					cout << "这个位置已经有棋子了" << endl;
				}
			}
			else {
				cout << "棋子超出范围" << endl;
			}
		}

		qipan[x][y] = 'o';
		huatu();
		if (shuyin('o')) {
			cout << "玩家1获胜" << endl;
			break;
		}
		while (true) {
			cout << "玩家2：" << endl;
			cout << "请输入x：";
			cin >> x;
			cout << "请输入y：";
			cin >> y;
			x--;
			y--;
			if (x > -1 && x < 3 && y>-1 && y < 3) {
				if (qipan[x][y] == ' ') {
					break;
				}
				else {
					cout << "这个位置已经有棋子了" << endl;
				}
			}
			else {
				cout << "棋子超出范围" << endl;
			}
		}
		qipan[x][y] = 'x';
		huatu();
		if (shuyin('x')) {
			cout << "玩家2获胜" << endl;
			break;
		}

	}

}
```

清屏

```c++
#include <iostream>
using namespace std;
char qipan[3][3] = {
	{' ',' ',' '},
	{' ',' ',' '},
	{' ',' ',' '},
};
void huatu() {
	for (int i = 0; i < 8; i++) {
		if (i == 0) {
			cout << " | 1 | 2 | 3 |" << endl;
		}
		else if (i == 1 || i == 3 || i == 5 || i == 7) {
			cout << "-|---|---|---|" << endl;
		}
		else if (i == 2) {
			cout << "1| " << qipan[0][0] << " | " << qipan[0][1] << " | " << qipan[0][2] << " |" << endl;
		}
		else if (i == 4) {
			cout << "2| " << qipan[1][0] << " | " << qipan[1][1] << " | " << qipan[1][2] << " |" << endl;
		}
		else if (i == 6) {
			cout << "3| " << qipan[2][0] << " | " << qipan[2][1] << " | " << qipan[2][2] << " |" << endl;
		}
	}
}
bool shuyin(char a) {
	for (int i = 0; i < 3; i++) {
		if (qipan[i][0] == a && qipan[i][1] == a && qipan[i][2] == a) {
			return 1;
		}
		if (qipan[0][i] == a && qipan[1][i] == a && qipan[2][i] == a) {
			return 1;
		}
	}
	if (qipan[0][0] == a && qipan[1][1] == a && qipan[2][2] == a) {
		return 1;
	}
	if (qipan[0][2] == a && qipan[1][1] == a && qipan[2][0] == a) {
		return 1;
	}
	return 0;
}
int main()
{
	int x, y;
	huatu();
	while (true)
	{
		
		while (true) {
			cout << "玩家1：" << endl;
			cout << "请输入x：";
			cin >> x;
			cout << "请输入y：";
			cin >> y;
			x--;
			y--;
			if (x > -1 && x < 3 && y>-1 && y < 3) {
				if (qipan[x][y] == ' ') {
					break;
				}
				else {
					cout << "这个位置已经有棋子了" << endl;
				}
			}
			else {
				cout << "棋子超出范围" << endl;
			}
		}

		qipan[x][y] = 'o';
		system("cls");
		huatu();
		if (shuyin('o')) {
			cout << "玩家1获胜" << endl;
			break;
		}
		while (true) {
			cout << "玩家2：" << endl;
			cout << "请输入x：";
			cin >> x;
			cout << "请输入y：";
			cin >> y;
			x--;
			y--;
			if (x > -1 && x < 3 && y>-1 && y < 3) {
				if (qipan[x][y] == ' ') {
					break;
				}
				else {
					cout << "这个位置已经有棋子了" << endl;
				}
			}
			else {
				cout << "棋子超出范围" << endl;
			}
		}
		qipan[x][y] = 'x';
		system("cls");
		huatu();
		if (shuyin('x')) {
			cout << "玩家2获胜" << endl;
			break;
		}

	}

}
```

