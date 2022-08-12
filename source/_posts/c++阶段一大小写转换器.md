---
title: c++阶段一大小写转换器
date: 2021-11-03 11:27:22
tags: [教材,阶段一]
categories: c++
---

# 大小写转换器

思考：

```c++
double a = 1.0;
cout<<a;
```

自动类型转换：

c++中会将一些基础的数据类型进行转换，也方便程序更好的运行。

```c++
int b = 1.3;
cout<<b;
```

思考：我们需要转换一些数据类型的时候，刚好c++就没有自动类型转换怎么办呢？

强制类型转换：

(数据类型)值

作用：小括号里的数据类型就是我们想要将后面的值转换成什么类型。

练习：

```c++
char a = 100;
cout<<a;
```

将字符a,b,c,A,B,C转为int的值分别是多少？

## 测试项目：大小写转换器

![](https://gitee.com/gaoxianglong/picgo/raw/master/img/%E5%A4%A7%E5%B0%8F%E5%86%99%E8%BD%AC%E6%8D%A2%E5%99%A8%E6%BC%94%E7%A4%BA.gif)

```c++
#include <iostream>
using namespace std;

int main()
{
	char a = ' ';
	int b = 0;
	cout << "欢迎来到字母大小写转换器" << endl;
	while (true)
	{
		cout << "请输入一个字母，大小写都可以" << endl;
		cin >> a;
		b = a;
		if (b > 64 && b < 91) {
			cout << "检测到您输入的是" << a << "\n它的小写字母为" << (char)(b + 32) << endl;
		}
		else if (b > 96 && b < 123) {
			cout << "检测到您输入的是" << a << "\n它的大写字母为" << (char)(b - 32) << endl;
		}
		else {
			cout << "请按要求输入" << endl;
		}
		cout << "=============================================" << endl;
	}
}
```

