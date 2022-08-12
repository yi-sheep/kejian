---
title: c++阶段五第二讲
date: 2022-02-24 14:58:45
tags: [教材,阶段五]
categories: c++
---

# 第二讲

**上节课代码：**

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
        }else if (i < 10) {
            cout << " " << i  << "| ";
            for (int t = 0; t < 20; t++) {
                cout << qizi[i-1][t] << " | ";
            }
            cout << "\n";
        }
        else {
            cout << i  << "| ";
            for (int t = 0; t < 20; t++) {
                cout << qizi[i-1][t] << " | ";
            }
            cout << "\n";
        }
        cout << " -|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|\n";
    }
}
int main()
{
    init();
    huaqipan();
}
```

## 下棋

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

