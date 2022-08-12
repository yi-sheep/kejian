---
title: WPF深入10
date: 2022-06-28 09:30:29
tags: [教材,阶段一]
categories: c++
---

# WPF深入10

## 贪吃蛇

### 添加食物

我们现在有一个棋盘背景作为游戏区域，还有一条可爱的绿蛇在它周围移动。然而，正如介绍中提到的，游戏的目的是让蛇吃一些食物——在我们的版本中它是红苹果！

所以现在是时候开始向游戏区添加一些食物了。我们将通过在 GameArea Canvas 边界内的某处随机添加一个红色圆圈来实现，但我们需要确保我们没有将其放置在游戏区的非蛇的区域。

我们需要一个随机数对象

```c#
/// <summary>
/// 随机数对象
/// </summary>
private Random rnd = new Random();
```

现在就可以先产生一个食物的坐标

```c#
/// <summary>
/// 产生食物坐标
/// </summary>
/// <returns></returns>
private Point GetNextFoodPosition()
{
    // 最大的X
    int maxX = (int)(GameArea.ActualWidth / SnakeSquareSize);
    // 最大的Y
    int maxY = (int)(GameArea.ActualHeight / SnakeSquareSize);
    // 随机产生一个食物的坐标
    int foodX = rnd.Next(0, maxX) * SnakeSquareSize;
    int foodY = rnd.Next(0, maxY) * SnakeSquareSize;

    // 检测食物坐标是否和蛇身重合
    foreach (SnakePart snakePart in snakeParts)
    {
        if ((snakePart.Position.X == foodX) && (snakePart.Position.Y == foodY))
            return GetNextFoodPosition(); // 如果重合就再调用一下自己重新产生一个坐标，并且作为返回值
    }
    // 返回正确的坐标
    return new Point(foodX, foodY);
}
```

有了这些，我们就可以添加将在新计算的位置添加食物的代码 - 我们将通过一个名为**DrawSnakeFood()**的方法来**完成**。*GetNextFoodPosition()*已经完成了坐标的工作，它非常简单，但首先，请务必声明用于保存对食物的引用的字段，以及用于绘制食物的 SolidColorBrush，以及其他字段/常量声明：

```c#
/// <summary>
/// 食物的控件
/// </summary>
private UIElement snakeFood = null;
/// <summary>
/// 食物的颜色
/// </summary>
private SolidColorBrush foodBrush = Brushes.Red;
```

现在可以编写用于绘制食物的方法了：

```c#
/// <summary>
/// 画食物
/// </summary>
private void DrawSnakeFood()
{
    // 获取食物坐标
    Point foodPosition = GetNextFoodPosition();
    // 设置食物控件
    snakeFood = new Ellipse()
    {
        Width = SnakeSquareSize,
        Height = SnakeSquareSize,
        Fill = foodBrush
    };
    // 将食物添加到画板上
    GameArea.Children.Add(snakeFood);
    // 设置位置
    Canvas.SetTop(snakeFood, foodPosition.Y);
    Canvas.SetLeft(snakeFood, foodPosition.X);
}
```

有了这个，我们真的只需要调用 DrawSnakeFood() 方法来查看我们的工作结果。这将在两种情况下完成：在游戏开始时和蛇“吃”食物时（稍后会详细介绍）。现在，让我们在**StartNewGame()**方法中添加对它的调用：

```c#
/// <summary>
/// 开始新游戏
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
    // 画食物
    DrawSnakeFood();
    // 启用定时器 
    dispatcher.IsEnabled = true;
}
```

