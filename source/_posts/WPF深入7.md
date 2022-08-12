---
title: WPF深入7
date: 2022-06-27 11:21:50
tags: [教材,阶段一]
categories: c++
---

# WPF深入7

## 贪吃蛇

## 移动蛇

为了给 DrawSnake() 方法提供一些东西，我们需要填充**snakeParts**列表。这个列表一直作为绘制蛇的每个元素的基础，所以我们也将使用它来为蛇创建运动属性，需要有

- 蛇的方向

  ```c#
  /// <summary>
  /// 枚举，表示蛇的方向
  /// </summary>
  public enum SnakeDirection { Left, Right, Up, Down };
  ```

- 蛇的初始方向

  ```c#
  /// <summary>
  /// 设置初始蛇的方向
  /// </summary>
  private SnakeDirection snakeDirection = SnakeDirection.Right;
  ```

- 蛇的长度

  ```c#
  /// <summary>
  /// 蛇的初始长度
  /// </summary>
  const int SnakeStartLength = 3;
  /// <summary>
  /// 表示当前蛇的长度
  /// </summary>
  private int snakeLength;
  ```

有了这些，我们就可以为蛇初始化一个部分了，在**StartNewGame()**方法中完成。

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

    // 画蛇  
    DrawSnake();
}
```

现在，我们就可以实现**MoveSnake()**方法了。它有点长，所以我为它的每个重要部分添加了内联注释：

```c#
// <summary>
/// 蛇移动
/// </summary>
private void MoveSnake()
{
    // 尾尾头
    // 删除掉超过蛇身当前长度的部分
    while (snakeParts.Count >= snakeLength)
    {
        GameArea.Children.Remove(snakeParts[0].UiElement);
        snakeParts.RemoveAt(0);
    }

    // 将目前蛇列表全部变为蛇的身体 
    foreach (SnakePart snakePart in snakeParts)
    {
        (snakePart.UiElement as Rectangle).Fill = snakeBodyBrush;
        snakePart.IsHead = false;
    }

    // 获取到蛇列表中最新的一个，方便我们设置蛇头的位置  
    SnakePart snakeHead = snakeParts[snakeParts.Count - 1];
    double nextX = snakeHead.Position.X;
    double nextY = snakeHead.Position.Y;
    // 根据方向设置蛇头的位置
    switch (snakeDirection)
    {
        case SnakeDirection.Left:
            nextX -= SnakeSquareSize;
            break;
        case SnakeDirection.Right:
            nextX += SnakeSquareSize;
            break;
        case SnakeDirection.Up:
            nextY -= SnakeSquareSize;
            break;
        case SnakeDirection.Down:
            nextY += SnakeSquareSize;
            break;
    }

    // 将蛇头添加到蛇列表
    snakeParts.Add(new SnakePart()
                   {
                       Position = new Point(nextX, nextY),
                       IsHead = true
                   });
    // 画一下蛇
    DrawSnake();
}
```

移动的原理就是在开始移动前看看蛇列表的长度是不是和蛇当前长度一致，不一致说明第0下标的元素是多余的（一会解释）

将列表里的元素全部转换为“身体”，然后将列表里最后面一个位置的坐标保存起来，根据方向键改变坐标，再将改变完成后的添加到列表里（列表最后）这样列表中的元素个数和蛇当前长度就不一致了，下一次在调用**MoveSnake()**方法时就会删除多出来的。
