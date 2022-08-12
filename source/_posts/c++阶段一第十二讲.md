---
title: c++阶段一第十二讲
date: 2021-12-02 18:55:14
tags: [教材,阶段一]
categories: c++
---

# 第十二讲

## 开关语句

switch语句

公式：

```c++
switch(值){
    case 对比值:
        break;
    ...
    default:
		break;
}
```

例子：

```c++
switch(2){
    case 1:
        cout<<"1";
        break;
    case 2:
        cout<<"2";
        break;
    case 3:
        cout<<"3";
        break;
    default:
        cout<<"...";
		break;
}
```

作用：小括号里的值和下面每一个case对应的值依次比较是否相等，如果相等则会运行对应的代码块。

`switch`和`if`的区别：switch逻辑上和条件判断语句是一样的，不过它存在break这个特殊点就可以简化比较多的代码。if语句不只是判断相不相等。

练习：

评分系统，让用户输入一个成绩分数，判断这个分数是哪一个等级。

| 分数 | 等级        |
| ---- | ----------- |
| 90   | A（优秀）   |
| 80   | B（不错）   |
| 70   | C+（良好）  |
| 60   | C           |
| 其他 | D（不及格） |

```c++
int c = 0;
cout << "请输入最低分为0，满分为100的成绩：" << " ";
cin >> c;
int grade;
grade = (int)(c / 10);
switch (grade)
{
case 10:
	cout << "A+\n";
	break;
case 9:
	cout << "A\n";
	break;
case 8:
	cout << "B+\n";
	break;
case 7:
	cout << "B\n";
	break;
case 6:
	cout << "B-\n";
	break;
default:
	cout << "D\n";
	break;
}
```

## goto

公式：

```c++
标签名:
goto 标签名;
```

