---
title: c++阶段二第十三讲
date: 2021-12-09 15:13:58
tags: [教材,阶段二]
categories: c++
---

# 第十三讲

## 手速检测器

```c++
#include <iostream>
#include<ctime>
int main(){
    clock_t start,finish;
    double time = 0;
    start = clock();
    while(time<10){
        finish = clock();
        time = (double)(finish-start) / CLOCKS_PER_SEC;
    }
    cout<<time;
}
```

clock_t：处理器运行频率的类型

clock()：读取处理器当前的运行次数

做完后的时间-做之前的时间

/ CLOCKS_PER_SEC：转为以秒为单位的时间

_getch()：读取键盘上的某个按键

```
char a = _getch();
```

```c++
﻿#include <iostream>
#include<conio.h>
#include<stdlib.h>
#include<Windows.h>
#include<ctime>
using namespace std;
int main()
{
	cout << "欢迎来到手速检测器！连续多次按下s键即可\n";
	Sleep(3000);
	cout << "准备开始倒计时！";
	Sleep(1000);
	cout << 3 << "\n";
	Sleep(1000);
	cout << 2 << "\n";
	Sleep(1000);
	cout << 1 << "\n";
	Sleep(1000);
	cout << "开始!" << "\n";
	system("cls");
	clock_t start, finish;
	double totaltime = 0;
	int sum = 0;
	start = clock();
	while (totaltime < 60) {
		if (_getch() == 's') {
			sum++;
			system("cls");
			cout << sum;
		}
		finish = clock();
		totaltime = (double)(finish - start) / CLOCKS_PER_SEC;//CLOCKS_PER_SEC是标准c的time.h头函数中宏定义的一个常数，表示一秒钟内CPU运行的时钟周期数，用于将clock()函数的结果转化为以秒为单位的量
	}
	cout << "\n时间到！";
	Sleep(2500);
	cout << "\n你的手速为每分钟" << sum << "次";
}
```

