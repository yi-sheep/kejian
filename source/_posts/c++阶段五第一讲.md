---
title: c++阶段五第一讲
date: 2022-02-18 14:02:46
tags: [教材,阶段五]
categories: c++
---

# 第一讲

## 棋

### 井字棋

![](https://gitee.com/gaoxianglong/picgo/raw/master/img/image-20211111153025496.png)

画图:

```c++
#include <iostream>
using namespace std;
char qizi[9][9];
void init() {
	for (int i = 0; i < 9; i++) {
		for (int j = 0; j < 9; j++)
		{
			qizi[i][j] = ' ';
		}
	}
}
void huaqipan() {
	system("cls");
	cout << "\n\n";
	cout << "最新棋盘形势：\n";
	for (int i = 0; i < 4; i++)
	{
		if (i == 0) {
			cout << " | 1 | 2 | 3 |\n";
		}
		else {
			cout << i << "|   |   |   |\n";
		}
		cout << "-|---|---|---|\n";
	}
}
int main()
{
	init();
	huaqipan();
}
```

### 五子棋

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

