---
title: c++阶段三第四讲
date: 2021-09-29 10:40:52
tags: [教材,阶段三] 
categories: c++
---

# 第四讲

## 面向对象

### 静态

在类中我们可以去声明某一个成员或函数为静态的，被所有对象共享。

**静态成员：**

`static int a;`

**静态函数：**

```c++
static void fun(){
    
}
```

现在去创建一个学生类，有`班级` `姓名` 两个属性，但是`班级`属性需要是静态的。然后在主函数里创建出两个学生类的对象分别给他们的属性赋值。最后输出出来。

```c++
#include<iostream>
using namespace std;
class Student {
public:
	static string banji;
	string name;
	void print() {
		cout << banji << " " << name;
	}
};
string Student::banji = " ";
int main(int argc, char** argv) {
	Student s1; 
	Student s2;
	s1.banji = "三年级3班";
	s1.name = "小魏";
	s2.banji = "三年级2班";
	s2.name = "小袁";
	s1.print();
	s2.print();
	return 0;
}
```

静态成员必须要进行特殊的初始化，在类创建完成后就要做这个操作.

`数据类型 类名::静态成员 = 值;`

## 内部类

在一个类中定义另一个类，称为内部类。

内部类可以很好的访问到外部类的**任何属性**其中也包括私有的。必须是静态的。

练习：

在刚刚的学生类中新建一个成绩类，这个类里有`语文` `数学` `英语`三个属性，还有一个函数用于打印信息，格式要求  我叫`姓名`，来自`班级` 语文成绩：`语文`,数学成绩：`数学`,英语成绩：`英语`

## 局部类

我们将类创建到函数中，那么这个类就称为局部类，这类的可被访问的范围就仅限于当前这个函数。

例子：

```c++
#include <iostream>
using namespace std;
int main(int argc, char** argv){
	class renlei{
	public:
  string xingming;
	int nianling;
	int shenggao; 
	void shuohua(string shuo){
		cout<<shuo; 
	}
	void zoulu(int zou){
		cout<<"走了"<<zou<<"步"<<"\n";
	}
	 void getxingming(){
		cout<<"我叫"<<xingming<<"\n";
	}
}; 
	renlei s;   
	s.xingming="小杨";
	s.getxingming(); 
	return 0;
}
```

