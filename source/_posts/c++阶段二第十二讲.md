---
title: c++阶段二第十二讲
date: 2021-12-03 09:19:50
tags: [教材,阶段二]
categories: c++
---

# 第十二讲

## 人机对战

上节课的程序

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

随机数：

需要种子

`srand(tiem(NULL));`

产生随机数

`rand()%5;`

人机下棋：

```c++
void renjiduizhan() {  //人机对战函数
    srand(time(NULL));
    while (true) {
        huachangdi();
        cout << "请玩家输入棋子的横坐标： ";
        int x = 0;
        cin >> x;
        cout << "请玩家输入棋子的纵坐标： ";
        int y = 0;
        cin >> y;
        if (x >= 1 && x <= 3 && y >= 1 && y <= 3) {
            if (qizizhuangtai[y - 1][x - 1] == '\0') {
                qizizhuangtai[y - 1][x - 1] = 'Q';
            }
            else {
                cout << "\n此棋位已被棋子占领，请重新选择棋位。\n";
            }
        }
        else {
            cout << "坐标输入错误，请重新输入。";
        }
        huachangdi();
        if (shuyingjiance() == 1) {
            cout << "游戏结束，玩家获胜！";
            break;
        }
        int jiqirenx = rand() % 3;
        int jiqireny = rand() % 3;
        while (true) {
            if (qizizhuangtai[jiqireny][jiqirenx] =='\0') {
                break;
            }
            jiqirenx = rand() % 3;
            jiqireny = rand() % 3;
        }
        qizizhuangtai[jiqireny][jiqirenx] = 'X';   
        if (shuyingjiance() == 2) {
            cout << "游戏结束,计算机获胜！";
            break;
        }
    }
}
```

