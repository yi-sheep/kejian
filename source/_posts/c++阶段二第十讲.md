---
title: c++阶段二第十讲
date: 2021-11-17 13:09:23
tags: [教材,阶段二]
categories: c++
---

# 第十讲

下棋

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
        cout << "请输入x：";
        cin >> x;
        cout << "请输入y：";
        cin >> y;
        qipan[x][y] = 'o';
        huatu();
        cout << "请输入x：";
        cin >> x;
        cout << "请输入y：";
        cin >> y;
        qipan[x][y] = 'x';
    }
    
}
```

## bug

下棋超出范围

```c++
while (true)
    {
        huatu();
        while (true) {
            cout << "请输入x：";
            cin >> x;
            cout << "请输入y：";
            cin >> y;
            if (x > 0 && x < 4 && y>0 && y < 4) {
                break;
            }
            else {
                cout << "棋子超出范围" << endl;
            }
        }
        x--;
        y--;
        qipan[x][y] = 'o';
        huatu();
        while (true) {
            cout << "请输入x：";
            cin >> x;
            cout << "请输入y：";
            cin >> y;
            if (x > 0 && x < 4 && y>0 && y < 4) {
                break;
            }
            else {
                cout << "棋子超出范围" << endl;
            }
        }
        x--;
        y--;
        qipan[x][y] = 'x';
    }
```

- 顶掉别的棋子

```c++
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
```

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

