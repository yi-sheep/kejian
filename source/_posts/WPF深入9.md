---
title: WPF深入9
date: 2022-06-28 08:52:26
tags: [教材,阶段一]
categories: c++
---

# WPF深入9

## 贪吃蛇

### 按键移动

大多数 WPF 控件都有用于从鼠标和键盘接收输入的事件。因此，根据您想要检查输入的位置，您可以为一个或多个控件订阅这些事件，然后在那里执行逻辑。然而，由于这是一个游戏，我们希望无论焦点在哪里都能捕捉到键盘输入，所以我们将直接在 Window 上订阅事件。

对于我们想要完成的事情，**KeyUp**（按键抬起）事件非常适合。因此，找到您的 Window 的 XAML 文件并修改 Window 标记，使其包含 KeyUp 事件，如下所示：

```c#
<Window x:Class="te.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:te"
        mc:Ignorable="d"
        Title="贪吃蛇"
        SizeToContent="WidthAndHeight"
        ContentRendered="Window_ContentRendered"
        KeyUp="Window_KeyUp">
</Window>
```

在您的后端代码，添加**Window_KeyUp()**事件处理程序，如下所示：

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
    }
    // 方向和当选方向不同再移动
    if (snakeDirection != originalSnakeDirection)
    {
        MoveSnake();
    }
}
```

我们要做的第一件事是保存对蛇行进的当前方向的引用 - 我们需要这样做来确保玩家不会尝试做我们不允许的事情，例如在蛇的身体上倒车（例如从右到左）。换句话说，如果蛇在垂直移动而玩家想要改变方向，它必须先水平移动——你不能直接从上到下或从左到右。

接下来是一个**switch**语句，我们检查按下了哪个键。在这里，我们检查是否按下了其中一个箭头键（**Up**、**Down**、**Left**、**Right**）——如果按下了，它们可以改变蛇的方向，除非这种改变在物理上是不可能的，如上所述。另请注意，我添加了对**Space**键的检查：它将调用 StartNewGame() 方法，以允许玩家选择游戏何时开始，而不是自动开始。它还允许玩家在上一场比赛结束后开始新的比赛。

在方法结束时，我们检查方向与原始方向相比是否发生了变化——如果发生了变化，我们调用**MoveSnake()**方法，以便立即反映变化。

我们之前在**Window_ContentRendered**事件中添加了对**StartNewGame()**方法的**调用**- 您现在可以删除它，而是通过按 Space 键来启动游戏。现在你瞧，蛇是可以控制的——它现在接近于一个真正的游戏，而不仅仅是一条动画蛇！
