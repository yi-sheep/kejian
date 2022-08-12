---
title: c++阶段五第四讲
date: 2022-03-10 09:07:06
tags: [教材,阶段五]
categories: c++
---

# 第四讲

上节课代码

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

人机对战

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
			else if (qizi[i][j] == c || qizi[j][i] == c) {
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
int rjxiaqi() {
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
			x = (rand() % 20) + 1;
			y = (rand() % 20) + 1;
			if (qizi[x - 1][y - 1] == ' ') {
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
	srand(time(NULL));
	init();
	huaqipan();
	cout << "1.人机对战  2.玩家对战" << endl;
	int n;
	cin >> n;
	huaqipan();
	int a;
	if (n == 1) {
		a = rjxiaqi();
		if (a == 1) {
			cout << "玩家1获胜";
		}
		else if (a == 2) {
			cout << "玩家2获胜";
		}
	}
	else if (n == 2) {
		a = xiaqi();
		if (a == 1) {
			cout << "玩家1获胜";
		}
		else if (a == 2) {
			cout << "玩家2获胜";
		}
	}
	else {
		cout << "错误";
	}

}
```

棋子颜色

```c++
#include <iostream>
#include<Windows.h>
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
				if (qizi[i - 1][t] == 'x') {
					SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), 2);
				}
				else if(qizi[i - 1][t] == 'o'){
					SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), 4);
				}
				cout << qizi[i - 1][t];
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), 7);
				cout << " | ";
			}
			cout << "\n";
		}
		else {
			cout << i << "| ";
			for (int t = 0; t < 20; t++) {
				if (qizi[i - 1][t] == 'x') {
					SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), 2);
				}
				else if(qizi[i - 1][t] == 'o'){
					SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), 4);
					
				}
				cout << qizi[i - 1][t];
				SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), 7);
				cout << " | ";
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
			else if (qizi[i][j] == c || qizi[j][i] == c) {
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
int rjxiaqi() {
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
			x = (rand() % 20) + 1;
			y = (rand() % 20) + 1;
			if (qizi[x - 1][y - 1] == ' ') {
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
	srand(time(NULL));
	init();
	huaqipan();
	cout << "1.人机对战  2.玩家对战" << endl;
	int n;
	cin >> n;
	huaqipan();
	int a;
	if (n == 1) {
		a = rjxiaqi();
		if (a == 1) {
			cout << "玩家1获胜";
		}
		else if (a == 2) {
			cout << "玩家2获胜";
		}
	}
	else if (n == 2) {
		a = xiaqi();
		if (a == 1) {
			cout << "玩家1获胜";
		}
		else if (a == 2) {
			cout << "玩家2获胜";
		}
	}
	else {
		cout << "错误";
	}

}
```

