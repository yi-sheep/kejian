---
title: c++阶段二第八讲
date: 2021-10-28 10:20:30
tags: [教材,阶段二] 
categories: c++
---

# 第八讲

![](https://gitee.com/gaoxianglong/picgo/raw/master/img/%E8%AE%A1%E6%97%B6%E5%99%A81%E6%BC%94%E7%A4%BA.gif)

## 分析项目

+ 用户提示
  + 感谢您选择华为牌计时器!
  + 请输入您需要计时的分钟数：
  + 请输入您需要计时的秒数：
  + 时间到！
  + 感谢您的使用！欢迎下次再来！
+ 用户输入
  + 输入分整数
  + 输入秒整数
+ 清屏
  + 开始计时的时候
  + 每一次显示新的时间的时候
+ 计时
  + 判断秒有没有到用户输入的
  + 判断分有没有到用户输入的

## 初始化

+ 创建变量
  + 保存用户输入的分
  + 保存用户输入的秒
  + 保存当前计时到第几分
  + 保存当前计时到第几秒
+ 做开始的用户提示
  + 感谢您选择华为牌计时器!
+ 用户输入
  + 输入分
  + 输入秒
  + 中间穿插用户提示

## 功能实现

- 用户输入了多少分钟就循环多少次

  > 当前外层循环第几次就表示当前是第几分钟

- 内层循环中根据用户输入的秒进行循环

  > 当前内层循环第几次就表示当前是第几分钟

- 内层循环中每一次循环等待一秒，并且清空控制台重新显示当前内外层的循环次数，也就是当前的时间

## 收尾

+ 循环完毕后表示时间到了，我们来一个用户提示就行。

计时器完整项目:

```c++
#include<iostream>
#include<Windows.h>
using namespace std;
int main()
{
	int fen = 0;
	int miao = 0;
	int kongzhifen = 0;
	int kongzhimiao = 0;
	cout << "感谢您选择华为牌计时器!\n";
	cout << "请输入您需要计时的分钟数：";
	cin >> kongzhifen;
	cout << "请输入您需要计时的秒数：";
	cin >> kongzhimiao;
	for (fen = 0; fen <= kongzhifen; fen++)
	{
		for (miao = 0; miao < kongzhimiao; miao++)
		{
			Sleep(10);
			system("cls");
			cout << fen << ":" << miao << "\n";
		}
	}
	Sleep(10);
	system("cls");
	cout << fen - 1 << ":" << miao << "\n";
	cout << "时间到！\n感谢您的使用！欢迎下次再来！\n";
}
```

修改计时器项目为多少秒倒计时。

要求：

输入格式`100`

输出格式`1:40`

