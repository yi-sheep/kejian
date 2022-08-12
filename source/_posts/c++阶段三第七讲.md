---
title: c++阶段三第七讲
date: 2021-10-28 11:25:30
tags: [教材,阶段三] 
categories: c++
---

# 第七讲

## 模板

### 函数模板

利用函数去解决计算两个数相加。（两个数可以是小数，整数。得到的结果也必须要是对应的）

作用：

模板往往作用在函数或类中，一些数据类型没法马上确定，就可以使用模板去暂时顶替该数据类型。

函数模板公式：

```c++
template <typename 类型名> 
返回值类型 函数名(){

}
```

```c++
template <class 类型名> 
返回值类型 函数名(){
    
}
```

如果用函数模板来解决上面的问题

```c++
#include<iostream>
#include<Windows.h>
using namespace std;
template <typename T> 
T add(T a, T b) {
	return a + b;
}
int main()
{
	cout << add(1, 2)<<endl;
	cout << add(1.1, 1.2);
}
```

练习

利用函数去完成两个变量的值交换

要求：

```c++
int main()
{
	int a = 1;
	int b = 3;
	jh(a,b);
	cout << a << " " << b; // 输出 3 1
}
```

```c++
#include<iostream>
#include<Windows.h>
using namespace std;
template <typename T> 
void jh(T &a, T &b) {
	T c = a;
	a = b;
	b = c;
}
int main()
{
	int a = 1;
	int b = 3;
	jh(a,b);
	cout << a << " " << b; // 输出 3 1
}
```

### 模板类

模板类公式：

```c++
template <class T>
class A{
    
}
```

案例

```c++
template<class NameType,class AgeType>
class Person{
public:
Person(NameType name, AgeType age)
{
this->m_Name = name;
this->m_age = age;
}
NameType m_Name;
AgeType m_age;
}
int main(){
  Person<string,int> p1("孙悟空",999);
}
```



