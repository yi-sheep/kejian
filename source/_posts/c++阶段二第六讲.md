---
title: c++阶段二第六讲
date: 2021-10-21 12:57:04
tags: [教材,阶段二] 
categories: c++
---

# 第六讲

## 指针

尝试：

定义一个数组a，直接输出这个a的值，不用去管房间号。

思考：

这个结果到底是什么？为什么会输出这个样的一个结果？

这个结果是一个地址，是a数组的地址，准确的说其实是数组中第一个房间的地址。

这个样的地址是可以被保存下来的，但是想要特殊的方式去保存！这个方式就是指针变量。

### 指针变量的定义

`数据类型* 指针变量名;`

如：

`int* p;`声明一个整形的指针

>  指针变量只能保存地址

### 指针的赋值

`&`:取地址符，使用在变量名的前面。

+ 指针可以在声明的时候赋值

  ```c++
  int a = 0;
  int* p = &a;
  ```

- 指针还可以在声明之后去赋值

  ```c++
  int a = 0;
  int* p;
  p = &a;
  ```

> 通过变量访问另一个变量是直接的访问，通过指针访问一个变量是间接的。

### 指针的使用

```c++
int a = 1;
int* p = &a;
```

创建完后我们去输出p，就能直接输出地址

`cout<<p;`

我们还可以使用`*p`去访问到这个地址的值

`cout<<*p`

`*p = 2;`

练习：

定义一个变量，一个指针，让用户输入一个值保存在这个变量里，这个变量的地址保存在指针中，利用指针输出变量中的值是多少。

```c++
#include <iostream>
using namespace std;

int main()
{
	int a = 1;
	int* p = &a;
	cin >> a;
	cout << *p;
}
```

指针变量不能对他直接赋值

定义一个指针变量，然后为其直接赋值，看程序是否会报错。

```c++
#include<iostream>
using namespace std;
int main()
{
	int *p;
	p=100;
	cout<<*p;
}
```

创建一个常量，一个指针，常量的地址保存在指针里

```c++
#include <iostream>
using namespace std;
const int a = 1;
int main()
{
	const int* p = &a;
	cout << *p;
}
```

常量指针是指一个普通的指针，指向的地址是一个常量的地址。

特点：其地址可以修改，但是其指向的地址中的值无法改变。

` int const* p;  const int* p;`

例子：

```c++
#include <iostream>
using namespace std;
const int a = 1;
int main()
{
	int b = 2;
	int const* p = &b;
	p = &a;
	cout << *p;
}
```

指针常量是指指针本身就是一个常量，但是指向的地址不是常量的地址。

`int* const p;`

例子：

```c++
#include <iostream>
using namespace std;
const int a = 1;
int main()
{
	int b = 2;
	int* const p = &b;
	*p = 3;
	cout << *p;
}
```

特点：指向的地址中的值可以修改，但是地址无法修改。

指向常量的指针常量：其地址无法修改且地址中的值也无法修改
