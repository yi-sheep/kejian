---
title: c++阶段三第十讲
date: 2021-11-17 14:06:17
tags: [教材,阶段三]
categories: c++
---

# 第十讲

## 迭代器

公式：

`容器类型<数据类型>::iterator 迭代器名;`

例子：

```c++
#include <iostream>
#include <vector>
using namespace std;
int main()
{
	vector<int> v;
	v.push_back(1);
	v.push_back(2);
	v.push_back(3);
	v.push_back(4);
	for (vector<int>::iterator i = v.begin(); i != v.end(); i++) {
		cout << *i;
	}
}
```

## 异常处理：

在程序中有的代码常常会有可能出现异常，导致程序崩溃，其实这样的异常也是可以规避掉的。

### 抛出异常:

当程序执行到某一函数或方法内部时，程序本身出现了一些异常，但这些异常并不能由系统所捕获，这时就可以创建一个错误信息，再由系统捕获该错误信息并处理。创建错误信息并发送这一过程就是抛出异常。
抛出异常公式：
`throw 异常信息;`

例子：

```c++
double division(int a, int b)
{
   if( b == 0 )
   {
      throw "Division by zero condition!"; // 抛出异常
   }
   return (a/b);
}
```

### 异常捕获

catch 块跟在 try 块后面，用于捕获异常。您可以指定想要捕捉的异常类型，这是由 catch 关键字后的括号内的异常声明决定的。
公式：

```c++
try
{
   // 保护代码
}catch( ExceptionName e )
{
  // 处理 ExceptionName 异常的代码
}
```

例子：

```c++
#include <iostream>
using namespace std;

double division(int a, int b)
{
	if (b == 0)
	{
		throw "Division by zero condition!";
	}
	return (a / b);
}
int main()
{
	int x = 50;
	int y = 0;
	double z = 0;
	try {
		z = division(x, y);
		cout << z << endl;
	}
	catch (const char* msg) {
		cerr << msg << endl;
	}
	return 0;
}
```

多catch公式：

```c++
try
{
   // 保护代码
}catch(ExceptionName e )
{
  // 处理 ExceptionName 异常的代码
}catch(std::exception e)
{
 // 处理其他异常
}
```

