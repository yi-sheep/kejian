---
title: WPF深入8
date: 2022-06-27 14:05:22
tags: [教材,阶段一]
categories: c++
---

# WPF深入8

## 定时器

在wpf应用中，拥有定时器的概念，什么是定时器呢？

wpf中的定时器对象**DispatcherTimer**它不是写在xaml文件中，而是在后端程序中创建并使用。

**DispatcherTimer**类的工作方式：

1. 创建定时器对象

   ```c#
   DispatcherTimer timer = new DispatcherTimer();
   ```

2. 设置一个间隔时间

   ```c#
   timer.Interval = TimeSpan.FromSeconds(1); // 秒
   timer.Interval = TimeSpan.FromMilliseconds(1); // 毫秒
   timer.Interval = TimeSpan.FromMinutes(1); // 分钟
   ```

3. 设置间隔时间到了触发的事件

   ```c#
   timer.Tick += timer_Tick;
   void timer_Tick(object sender, EventArgs e)
   {
       
   }
   ```

4. 启动定时器

   ```c#
   timer.Start();
   // 或者
   timer.IsEnabled = true;
   ```

## 设置定时器

创建出一个定时器的对象

```c#
/// <summary>
/// 定时器
/// </summary>
private DispatcherTimer dispatcher = new DispatcherTimer();
```

需要创建一个常量去保存蛇是多少时间移动一次

```c#
/// <summary>
/// 蛇移动的间隔时间
/// </summary>
const int SnakeStartSpeed = 400;
```

我们现在需要订阅它的一个也是唯一的事件：**Tick**事件。我们将在 Window 的构造函数中进行：

```c#
public MainWindow()
{
    InitializeComponent();
    dispatcher.Tick += GameTickTimer_Tick;
}
/// <summary>
/// 定时器的Tick事件
/// </summary>
/// <param name="sender"></param>
/// <param name="e"></param>
private void GameTickTimer_Tick(object sender, EventArgs e)
{
    MoveSnake();
}
```

因此，每次计时器滴答时，都会调用 Tick 事件，它反过来调用我们之前实现的 MoveSnake() 方法。为了最终看到我们所有辛勤劳动的结果并拥有一条可视的、移动的蛇，我们基本上只需要创建初始的蛇部分，然后启动计时器。我们将创建一个名为**StartNewGame()**的方法，我们将使用该方法开始第一场比赛以及玩家死亡时任意数量的其他新游戏。不过，我们将从它的一个非常基本的版本开始，然后随着我们的发展，我将用更多的功能扩展它——现在，让我们让这条蛇动起来！

让我们按照承诺添加 StartNewGame() 方法的简单实现：

```c#
/// <summary>
/// 初始化蛇
/// </summary>
private void StartNewGame()
{
    // 将长度设置为初始的长度
    snakeLength = SnakeStartLength;
    // 设置蛇的初始方向
    snakeDirection = SnakeDirection.Right;
    // 给蛇的列表添加一个内容，相当于蛇有内容了
    snakeParts.Add(new SnakePart() { Position = new Point(SnakeSquareSize * 5, SnakeSquareSize * 5) });

    // 设置定时器的间隔时间
    dispatcher.Interval = TimeSpan.FromMilliseconds(SnakeStartSpeed);
    // 画蛇  
    DrawSnake();
    // 启用定时器 
    dispatcher.IsEnabled = true;
}
```

我们首先根据初始值设置**snakeLength**和**snakeDirection**。然后我们将一个控件添加到**snakeParts**列表（稍后会详细介绍），为它提供一个很好的向右移动的开始位置 - 我们将再次使用**SnakeSquareSize**常量来帮助计算正确的位置。有了这个，我们可以通过调用 DrawSnake() 方法来绘制蛇，然后启用计时器，这将基本上开始蛇的运动。

```c#
/// <summary>
/// 窗口内容渲染
/// </summary>
/// <param name="sender"></param>
/// <param name="e"></param>
private void Window_ContentRendered(object sender, EventArgs e)
{
    DrawGameArea();
    StartNewGame();
}
```

![动图](https://pic4.zhimg.com/v2-83741583b595702be33eef84ad8459c3_b.webp)
