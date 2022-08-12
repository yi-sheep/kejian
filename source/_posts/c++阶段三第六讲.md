---
title: c++阶段三第六讲
date: 2021-10-21 14:50:10
tags: [教材,阶段三]
categories: c++
---
# 第六讲

## 命名空间

命名空间：其作用是帮助区分同名的全局对象等。

公式：

```C++
namespace 空间名{
    
};
```

调用命名空间的格式：`空间名::成员名;`

案例：

```c++
代码案例：
#include<iostream>
namespace MyName  //定义命名空间
{
int iValue=10;  //定义整型变量
}
using namespace std;  //使用命名空间std
using namespace MyName;  //使用命名空间MyName
int main()
{
    cout<<iValue<<endl; //输出命名空间中的变量
    return 0;
}
```

练习：

给刚刚的类创建两个同名的对象，分别放在两个命名空间里。

## 类

一个类的完整结构

```c++
class MyClass
{
public:
    // 只定义了未实现这两个函数
	MyClass(); // 构造函数 
	~MyClass(); // 析构函数

private:

};
/*
 * 实现了MyClass中的构造函数MyClass()
 */
MyClass::MyClass()
{
}
/*
 * 实现了MyClass中的析构函数~MyClass()
 */
MyClass::~MyClass()
{
}
```

### 构造函数

类的**构造函数**是类的一种特殊的成员函数，它会在每次创建类的新对象时执行。

构造函数的名称与类的名称是完全相同的，并且不会返回任何类型，也不会返回 void。构造函数可用于为某些成员变量设置初始值。

```c++
#include <iostream>
 
using namespace std;
 
class Line
{
   public:
      void setLength( double len );
      double getLength( void );
      Line();  // 这是构造函数
 
   private:
      double length;
};
 
// 成员函数定义，包括构造函数
Line::Line(void)
{
    cout << "Object is being created" << endl;
}
 
void Line::setLength( double len )
{
    length = len;
}
 
double Line::getLength( void )
{
    return length;
}
// 程序的主函数
int main( )
{
   Line line;
 
   // 设置长度
   line.setLength(6.0); 
   cout << "Length of line : " << line.getLength() <<endl;
 
   return 0;
}
```

### 带参数的构造函数

默认的构造函数没有任何参数，但如果需要，构造函数也可以带有参数。这样在创建对象时就会给对象赋初始值，如下面的例子所示：

```c++
#include <iostream>
 
using namespace std;
 
class Line
{
   public:
      void setLength( double len );
      double getLength( void );
      Line(double len);  // 这是构造函数
 
   private:
      double length;
};
 
// 成员函数定义，包括构造函数
Line::Line( double len)
{
    cout << "Object is being created, length = " << len << endl;
    length = len;
}
 
void Line::setLength( double len )
{
    length = len;
}
 
double Line::getLength( void )
{
    return length;
}
// 程序的主函数
int main( )
{
   Line line(10.0);
 
   // 获取默认设置的长度
   cout << "Length of line : " << line.getLength() <<endl;
   // 再次设置长度
   line.setLength(6.0); 
   cout << "Length of line : " << line.getLength() <<endl;
 
   return 0;
}
```

### 析构函数

类的**析构函数**是类的一种特殊的成员函数，它会在每次删除所创建的对象时执行。

析构函数的名称与类的名称是完全相同的，只是在前面加了个波浪号（~）作为前缀，它不会返回任何值，也不能带有任何参数。析构函数有助于在跳出程序（比如关闭文件、释放内存等）前释放资源。

## 类的继承

继承是从已有的类那里得到已有的特性，已有的类称为基类或父类，新类被称为派生类或子类。

继承的实质就是用已有的数据类型创建新的数据类型，并保留已有数据类型的特点，以旧类为基础创建新类，新类包含了旧类的数据成员和成员函数，并可以在新类中添加新的成员。

继承方式也有三种：

共有型继承：public

受保护型继承：protected

私有型继承：private

继承后的可访问性问题：

共有型继承：父类中对于子类的public成员，在子类中依然是public，对于子类中的private成员，在子类中依然是private。

私有型继承：父类中的public、protected成员，子类中可以访问，父类中private的成员，子类不能访问。

保护型继承：父类中public、protected的成员，在子类中都是protected。Protected的成员在子类中可以访问，但是子类的对象不能访问。Protected的成员可以被父类的所有子类使用。

类的继承的公式：

```c++
class 子类名:继承方式 父类名{
}
```

类继承的案例：

```c++
#include <iostream>
using namespace std;
const int a = 1;
class A
{
public:
	string name;
};
class B:public A {
public:
	void fun() {
		name = "小猫";
		cout << name;
	}
};
int main()
{
	B b;
	b.fun();
}
```

分析案例

```c++
#include <iostream>
#include<cstring> 
using namespace std;
class CEmployee   //定义员工类
{
public:
    int m_ID;     //定义员工ID
    char m_Name[128];  //定义员工姓名
    char m_Depart[128];   //定义所属部门
    CEmployee()   //定义默认构造函数
    {
        memset(m_Name,0,128);   //初始化m_Name
        memset(m_Depart,0,128);  //初始化m_Depart
    }
    void OutputName()   //定义共有成员函数
    {
        cout <<"员工姓名"<<m_Name<<endl;//输出员工姓名
    }
};
class COperator :public CEmployee //定义一个操作员类，从CEmployee类派生而来
{
public:
    char m_Password[128];  //定义密码
    bool Login()    //定义登录成员函数
    {
        if (strcmp(m_Name,"MR")==0 && //比较用户名
                strcmp(m_Password,"KJ")==0)        //比较密码
        {
            cout<<"登录成功!"<<endl;            //输出信息
            return true;                    //设置返回值
        }
        else
        {
            cout<<"登录失败!"<<endl;            //输出信息
            return false;                    //设置返回值
        }
    }
};
int main(int argc, char* argv[])
{
    COperator optr;                     //定义一个COperator类对象
    strcpy(optr.m_Name,"MR");             //访问基类的m_Name成员
    strcpy(optr.m_Password,"KJ");           //访问m_Password成员
    optr.Login();               //调用COperator类的Login成员函数
    optr.OutputName();                        //调用基类CEmployee的OutputName成员函数
    return 0;
}
```

