---
title: WPF深入12
date: 2022-06-28 10:21:10
tags: [教材,阶段一]
categories: c++
---

# WPF深入12

## 贪吃蛇

随着吃掉的食物越多，蛇的速度应该越来越快

```c#
/// <summary>
/// 用于更具时间推移的加速值
/// </summary>
const int SnakeSpeedThreshold = 100;
/// <summary>
/// 吃掉食物后
/// </summary>
private void EatSnakeFood()
{
    // 长度增加
    snakeLength++;
    // 成绩增加
    currentScore++;
    // 计算新的刷新时间
    int timerInterval = Math.Max(SnakeSpeedThreshold, (int)dispatcher.Interval.TotalMilliseconds - (currentScore * 2));
    dispatcher.Interval = TimeSpan.FromMilliseconds(timerInterval);
    // 删除食物
    GameArea.Children.Remove(snakeFood);
    // 重新产生食物
    DrawSnakeFood();
    UpdateGameStatus();
}
```

## 按空格开始新游戏

```c#
/// <summary>
/// Window按键抬起事件
/// </summary>
/// <param name="sender"></param>
/// <param name="e"></param>
private void Window_KeyUp(object sender, KeyEventArgs e)
{
    // 保存一下当前蛇的方向
    SnakeDirection originalSnakeDirection = snakeDirection;
    // 判断当前按键方向
    // 方向不能相反
    switch (e.Key)
    {
        case Key.Up:
            if (snakeDirection != SnakeDirection.Down)
            {
                snakeDirection = SnakeDirection.Up;
            }
            break;
        case Key.Down:
            if (snakeDirection != SnakeDirection.Up)
            {
                snakeDirection = SnakeDirection.Down;
            }
            break;
        case Key.Left:
            if (snakeDirection != SnakeDirection.Right)
            {
                snakeDirection = SnakeDirection.Left;
            }
            break;
        case Key.Right:
            if (snakeDirection != SnakeDirection.Left)
            {
                snakeDirection = SnakeDirection.Right;
            }
            break;
        case Key.Space:
            StartNewGame();
            break;
    }
    // 方向和当选方向不同再移动
    if (snakeDirection != originalSnakeDirection)
    {
        MoveSnake();
    }
}
```

## 重新开始游戏时

清理地图

```c#
// 删除现有的蛇以及食物
foreach (SnakePart snakeBodyPart in snakeParts)
{
    if (snakeBodyPart.UiElement != null){ 				GameArea.Children.Remove(snakeBodyPart.UiElement);
    }
}
snakeParts.Clear();
if (snakeFood != null){
    GameArea.Children.Remove(snakeFood);
}
```

成绩归零

```c#
// 成绩归零
currentScore = 0;
```

更新游戏状态

```c#
// 更新游戏状态
UpdateGameStatus();
```

