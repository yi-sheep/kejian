---
title: c++阶段一第六讲
date: 2021-10-21 11:22:17
tags: [教材,阶段一] 
categories: c++
---

# 第六讲

## 复习

让用户输入两个数，计算这个两个数的结果。

```c++
#include <iostream>
using namespace std;
int main()
{
	int a = 0,b = 0;
	cout << "请输入第一个数:";
	cin >> a;
	cout << "请输入第二个数:";
	cin >> b;
	cout << (a + b);
}
```

让用户输入一个数判断这个数，是不是等于0，等于0就输出等于0，不等于0就输出不等于0。

```c++
#include <iostream>
#include <conio.h>
using namespace std;

int main()
{
	int a = 0;
	cout << "请输入第一个数:";
	cin >> a;
	if (a == 0) {
		cout << "等于0";
	}
	else {
		cout << "不等于0";
	}
}
```

## 多条件判断语句

公式：

```c++
if(布尔表达式){
    代码段;
}else if(布尔表达式){
    代码段;
}else ...{
    代码段;
}else {
    代码段;
}
```

作用：

每一个布尔表达式按顺序去判断，如果成立就执行对应大括号里的代码段，如果不成立就执行对应else后面的东西。

练习：

让用户输入两个数，去判断这个两个数的关系

```c++
#include <iostream>
#include <conio.h>
using namespace std;

int main()
{
	int a = 0,b=0;
	cout << "请输入第一个数:";
	cin >> a;
	cout << "请输入第二个数:";
	cin >> b;
	if (a > b) {
		cout << "第一个数大";
	}
	else if(a<b){
		cout << "第二个数大";
	}
	else {
		cout << "相等";
	}
}
```

## 嵌套

公式：

```c++
if(布尔表达式){
    if(布尔表达式){
    }
}
```

作用：嵌套使用时会优先判断最外层的条件判断语句，当最外层的成立时，才会再次判断里面的条件判断语句，如果连外面的都不成立，那么里面的条件判断语句连判断的机会都没有。当最外面的不成立时，会执行最外面的else里的代码。

练习：

让用户输入一个年份，去判断这个年份是闰年还是平年？

闰年发判断条件：

1：能被4整除但是不能被100整除

2：能被400整除

```c++
#include <iostream>
using namespace std;

int main()
{
	int year;
	cout << "请输入一个年份：";
	cin >> year;
	if (year % 4 == 0) {
		if (year % 100 == 0) {
			if (year % 400 == 0) {
				cout << "是润年！";
			}
			else {
				cout << "不是润年！";
			}
		}
		else {
			cout << "是润年！";
		}
	}
	else {
		cout << "不是润年！";
	}
}
```

