---
title: 数组深入EasyX图形库1
date: 2022-06-16 14:18:49
tags: [教材,数组深入] 
categories: c++
---

## 安装EasyX图像库

[EasyX Graphics Library for C++](https://easyx.cn/)

## 创建窗口

### initgraph

这个函数用于初始化绘图窗口。

```cpp
HWND initgraph(
	int width,
	int height,
	int flag = NULL
);
```

#### 参数

##### width

绘图窗口的宽度。

##### height

绘图窗口的高度。

##### flag

绘图窗口的样式，默认为 NULL。可为以下值：

| 值             | 含义                           |
| -------------- | ------------------------------ |
| EW_DBLCLKS     | 在绘图窗口中支持鼠标双击事件。 |
| EW_NOCLOSE     | 禁用绘图窗口的关闭按钮。       |
| EW_NOMINIMIZE  | 禁用绘图窗口的最小化按钮。     |
| EW_SHOWCONSOLE | 显示控制台窗口。               |

#### 返回值

返回新建绘图窗口的句柄。

#### 示例

以下代码片段创建一个尺寸为 640x480 的绘图窗口：

```cpp
initgraph(640, 480);
```

以下代码片段创建一个尺寸为 640x480 的绘图窗口，同时显示控制台窗口：

```cpp
initgraph(640, 480, EW_SHOWCONSOLE);
```

以下代码片段创建一个尺寸为 640x480 的绘图窗口，同时显示控制台窗口，并禁用关闭按钮：

```cpp
initgraph(640, 480, EW_SHOWCONSOLE | EW_NOCLOSE);
```

### closegraph

这个函数用于关闭绘图窗口。

## 图形

### arc

这个函数用于画椭圆弧。

```c++
void arc(
	int left,
	int top,
	int right,
	int bottom,
	double stangle,
	double endangle
);
```

#### 参数

##### left

圆弧所在椭圆的外切矩形的左上角 x 坐标。

##### top

圆弧所在椭圆的外切矩形的左上角 y 坐标。

##### right

圆弧所在椭圆的外切矩形的右下角 x 坐标。

##### bottom

圆弧所在椭圆的外切矩形的右下角 y 坐标。

##### stangle

圆弧起始角的弧度。

##### endangle

圆弧终止角的弧度。

![image-20220616150949104](https://s2.loli.net/2022/06/16/bLorMP8IX4NpgRH.png)

![image-20220616150230726](https://s2.loli.net/2022/06/16/m8ngQBipz7fXbUd.png)

### circle

这个函数用于画无填充的圆。

```c++
// 在100，100这个坐标上显示一个半径为20的圆
circle(100, 100, 20);
```

![image-20220616151355984](https://s2.loli.net/2022/06/16/C5ERv8y4GAbtBeI.png)

### clearcircle

这个函数用于清空圆形区域。

```c++
// 清理刚刚画的圆，需要将清理范围变大一点的
clearcircle(100, 100, 21);
```

## line

这个函数用于画直线。

```cpp
void line(
	int x1,
	int y1,
	int x2,
	int y2
);
```

### 参数

#### x1

直线的起始点的 x 坐标。

#### y1

直线的起始点的 y 坐标。

#### x2

直线的终止点的 x 坐标。

#### y2

直线的终止点的 y 坐标。

### 颜色

#### setfillcolor

这个函数用于设置当前设备填充颜色。

```c++
setfillcolor(BLUE);
```

