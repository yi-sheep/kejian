---
title: c++阶段一第七讲
date: 2021-10-28 09:18:35
tags: [教材,阶段一]
categories: c++
---

# 第七讲

用户输入一个年份，判断这个年份是闰年还是平年？

闰年发判断条件：

1：能被4整除但是不能被100整除

2：能被400整除

输入：

2000，2004，2008，2012，2016，2020，2024，2028，2032

都应该是闰年

```c++
#include<iostream>
#include<cstring>
using namespace std;

int main()
{
	int a = 0;
	cin >> a;
	if (a % 400 == 0||a % 4 == 0 && a % 100 != 0) {
		cout << "闰年" << endl;
	}
	else {
		cout << "平年" << endl;
	}

}
```

让用户输入一个月份，判断这个月份有多少天。（2月统一28天）

```c++
#include<iostream>
#include<cstring>
using namespace std;

int main()
{
	int a = 0;
	cin >> a;
	if (a==2) {
		cout << "28" << endl;
	}
	else if(a==4||a==6||a==9||a==11){
		cout << "30" << endl;
	}
	else if (a == 1 || a == 3 || a == 5 || a == 7 || a == 8 || a == 10 || a == 12) {
		cout << "31" << endl;
	}
	else {
		cout << "请输入正确的数据";
	}

}
```

让用户输入一个年份，和一个月份去判断这个年的这个月有多少天。

```c++
#include<iostream>
#include<cstring>
using namespace std;

int main()
{
	int a = 0,b=0;
	cout << "请输入一个年份:";
	cin >> b;
	cout << "请输入一个月份:";
	cin >> a;
	if (a==2) {
		if (b % 400 == 0 || b % 4 == 0 && b % 100 != 0) {
			cout << "29" << endl;
		}
		else
		{
			cout << "28" << endl;
		}
	}
	else if(a==4||a==6||a==9||a==11){
		cout << "30" << endl;
	}
	else if (a == 1 || a == 3 || a == 5 || a == 7 || a == 8 || a == 10 || a == 12) {
		cout << "31" << endl;
	}
	else {
		cout << "请输入正确的数据";
	}

}
```

## 三目运算符

三目运算符：也叫三元运算符。这个运算符的符号是： ? :

语法：

   `表达式1 ? 表达式2 : 表达式3;`

语义：

   先执行表达式1，执行完毕，表达式1的结果如果为真，那么执行表达式2，整个三目表达式的结果就是表达式2的结果，否则执行表达式3，整个三目表达式的结果就是表达式3的结果

练习：

```c++
cout<<(1?10:20);
```

```c++
int res = 0?10:20;
cout<<res;
```

```c++
int num1 = 10,num2=20,num3=30;
int res = num1?num1+num2:num1+num3;
cout<<res;
```

```c++
int num1=10,num2=20,num3=30;
int res = 0;
if(num1){
res = num1 + num2;
}else{
res = num1 + num3;
}
cout<<res;
```

```c++
int num1=10,num2=20;
int res = num1 > num2 ? num1++ : num2++;
cout<<res;
```

## 嵌套

三目运算符的嵌套和条件判断语句类似

1?0?1:0:1

可以看作1?(0?1:0):1

如果外层的条件成立那么就会执行这里小括号里的内容
