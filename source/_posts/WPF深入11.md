---
title: WPF深入11
date: 2022-06-28 09:50:49
tags: [教材,阶段一]
categories: c++
---

# WPF深入11

## 贪吃蛇

### 碰撞检测

现在我们已经实现了游戏区域、食物和蛇，以及蛇的连续运动，我们只需要最后一件事来使这个看起来和行为像一个真正的游戏：**碰撞检测**。这个概念围绕着不断检查我们的 Snake 是否只是撞到了什么东西而演变，我们目前需要它有两个目的：查看 Snake 是刚吃了一些食物还是撞到了障碍物（墙壁或自己的尾巴）。

碰撞检测将在名为**DoCollisionCheck()**的方法中执行，因此我们需要实现它。这是它目前的样子：

#### 碰撞食物

```c#
/// <summary>
/// 碰撞检测
/// </summary>
private void DoCollisionCheck()
{
    // 获取到蛇头的信息
    SnakePart snakeHead = snakeParts[snakeParts.Count - 1];
    // 将蛇头的位置和食物的位置进行比较
    if ((snakeHead.Position.X == Canvas.GetLeft(snakeFood)) && (snakeHead.Position.Y == Canvas.GetTop(snakeFood)))
    {
        // 吃掉食物后的处理
        return;
    }
}
```

碰撞食物后应该需要重新，长度增加，分数增加等工作，这些工作可以在**EatSnakeFood()**方法中去完成

```c#
/// <summary>
/// 当前成绩
/// </summary>
private int currentScore = 0;
...
/// <summary>
/// 吃掉食物后
/// </summary>
private void EatSnakeFood()
{
    // 长度增加
    snakeLength++;
    // 成绩增加
    currentScore++;
    // 删除食物
    GameArea.Children.Remove(snakeFood);
    // 重新产生食物
    DrawSnakeFood();
    // 更新游戏状态
    UpdateGameStatus();
}
```

有了成绩我们需要更新到窗口的标题栏上，这个工作我们在**UpdateGameStatus()**方法中完成：

```c#
/// <summary>
/// 更新游戏状态
/// </summary>
private void UpdateGameStatus()
{
    this.Title = "贪吃蛇 - 成绩: " + currentScore;
}
```

改变**DoCollisionCheck()**方法：

```c#
/// <summary>
/// 碰撞检测
/// </summary>
private void DoCollisionCheck()
{
    // 获取到蛇头的信息
    SnakePart snakeHead = snakeParts[snakeParts.Count - 1];
    // 将蛇头的位置和食物的位置进行比较
    if ((snakeHead.Position.X == Canvas.GetLeft(snakeFood)) && (snakeHead.Position.Y == Canvas.GetTop(snakeFood)))
    {
        // 吃掉食物后的处理
        EatSnakeFood();
        return;
    }
}
```

#### 碰撞边缘

```c#
/// <summary>
/// 碰撞检测
/// </summary>
private void DoCollisionCheck()
{
    // 获取到蛇头的信息
    SnakePart snakeHead = snakeParts[snakeParts.Count - 1];
    // 将蛇头的位置和食物的位置进行比较
    if ((snakeHead.Position.X == Canvas.GetLeft(snakeFood)) && (snakeHead.Position.Y == Canvas.GetTop(snakeFood)))
    {
        // 吃掉食物后的处理
        EatSnakeFood();
        return;
    }

    // 蛇头的位置是否超过边缘
    if ((snakeHead.Position.Y < 0) || (snakeHead.Position.Y >= GameArea.ActualHeight) ||
        (snakeHead.Position.X < 0) || (snakeHead.Position.X >= GameArea.ActualWidth))
    {
        // 结束游戏
    }
}
```

结束游戏的方法：

```c#
/// <summary>
/// 结束游戏
/// </summary>
private void EndGame()
{
    dispatcher.IsEnabled = false;
    MessageBox.Show("噢，你死了！", "贪吃蛇");
}
```

改变**DoCollisionCheck()**方法：

```c#
/// <summary>
/// 碰撞检测
/// </summary>
private void DoCollisionCheck()
{
    // 获取到蛇头的信息
    SnakePart snakeHead = snakeParts[snakeParts.Count - 1];
    // 将蛇头的位置和食物的位置进行比较
    if ((snakeHead.Position.X == Canvas.GetLeft(snakeFood)) && (snakeHead.Position.Y == Canvas.GetTop(snakeFood)))
    {
        // 吃掉食物后的处理
        return;
    }

    // 蛇头的位置是否超过边缘
    if ((snakeHead.Position.Y < 0) || (snakeHead.Position.Y >= GameArea.ActualHeight) ||
        (snakeHead.Position.X < 0) || (snakeHead.Position.X >= GameArea.ActualWidth))
    {
        // 结束游戏
        EndGame();
    }
}
```

#### 碰撞自己

```c#
/// <summary>
/// 碰撞检测
/// </summary>
private void DoCollisionCheck()
{
    // 获取到蛇头的信息
    SnakePart snakeHead = snakeParts[snakeParts.Count - 1];
    // 将蛇头的位置和食物的位置进行比较
    if ((snakeHead.Position.X == Canvas.GetLeft(snakeFood)) && (snakeHead.Position.Y == Canvas.GetTop(snakeFood)))
    {
        // 吃掉食物后的处理
        return;
    }

    // 蛇头的位置是否超过边缘
    if ((snakeHead.Position.Y < 0) || (snakeHead.Position.Y >= GameArea.ActualHeight) ||
        (snakeHead.Position.X < 0) || (snakeHead.Position.X >= GameArea.ActualWidth))
    {
        // 结束游戏
        EndGame();
    }

    // 蛇头有没有碰到自己的身体
    foreach (SnakePart snakeBodyPart in snakeParts.Take(snakeParts.Count - 1))
    {
        if ((snakeHead.Position.X == snakeBodyPart.Position.X) && (snakeHead.Position.Y == snakeBodyPart.Position.Y))
        {
            // 结束游戏
            EndGame();
        }
    }
}
```

### 移动之后碰撞检测

```c#
/// <summary>
/// 蛇移动
/// </summary>
private void MoveSnake()
{
    ...
    // 检测碰撞
    DoCollisionCheck();
}
```

