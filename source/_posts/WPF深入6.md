---
title: WPF深入6
date: 2022-06-27 09:44:44
tags: [教材,阶段一]
categories: c++
---

# WPF深入6

## 贪吃蛇

### 创造蛇

我们将使用名为 DrawSnake() 的方法绘制蛇——该方法实际上非常简单，但它确实需要很多额外的东西.

- 包括一个名为 SnakePart 的新类

  我们将一整条蛇分为每一小节，每一节都是一个方块组成，有各自的坐标（Point），这一节是否是头部。

  ```c#
  class SnakePart
  {
      public UIElement UiElement { get; set; } // 蛇身的控件
  
      public Point Position { get; set; } // 蛇身的位置坐标
  
      public bool IsHead { get; set; } // 是否是头部
  }
  ```

- 以及 Window 类上的一些额外字段。

  在窗口类中我们需要定义几个变量，蛇身的颜色、蛇头的颜色、蛇的整体列表。

  ```c#
  /// <summary>
  /// 蛇身的颜色
  /// </summary>
  private SolidColorBrush snakeBodyBrush = Brushes.Green;
  /// <summary>
  /// 蛇头的颜色
  /// </summary>
  private SolidColorBrush snakeHeadBrush = Brushes.YellowGreen;
  /// <summary>
  /// 蛇列表，保存整条蛇的信息
  /// </summary>
  private List<SnakePart> snakeParts = new List<SnakePart>();
  ```

我们现在可以实现我们的 DrawSnake() 方法：

```c#
/// <summary>
/// 绘制蛇
/// </summary>
private void DrawSnake()
{
    // 遍历整条蛇
    foreach (SnakePart snakePart in snakeParts)
    {
        // 看看当前这一节的控件是否为空
        if (snakePart.UiElement == null)
        {
            // 创建一个方块，设置宽度和高度和颜色
            snakePart.UiElement = new Rectangle()
            {
                Width = SnakeSquareSize,
                Height = SnakeSquareSize,
                Fill = (snakePart.IsHead ? snakeHeadBrush : snakeBodyBrush)
            };
            // 将这一节作为子控件添加到画板中
            GameArea.Children.Add(snakePart.UiElement);
            // 设置这一节的位置坐标
            Canvas.SetTop(snakePart.UiElement, snakePart.Position.Y);
            Canvas.SetLeft(snakePart.UiElement, snakePart.Position.X);
        }
    }
}
```

这里的技巧当然是蛇的实际部分将在别处定义，允许我们向蛇添加一个或几个部分，给它们所需的位置，然后让 DrawSnake() 方法为我们做实际的工作. 我们将把它作为用于移动蛇的相同过程的一部分。

验证

虽然现在运行程序没有效果，但是我们可以添加一下临时的测试代码

```c#
public partial class MainWindow : Window
{
    ...
    public MainWindow()
    {
        InitializeComponent();
        // 测试
        SnakePart snake = new SnakePart() { Position = new Point(SnakeSquareSize*5, SnakeSquareSize*5) };
        snakeParts.Add(snake);
    }
    /// <summary>
    /// 窗口内容渲染
    /// </summary>
    /// <param name="sender"></param>
    /// <param name="e"></param>
    private void Window_ContentRendered(object sender, EventArgs e)
    {
        DrawGameArea();
        //测试
        DrawSnake();
    }
    ...
}
```

![image-20220627113722069](https://s2.loli.net/2022/06/27/FvJs4Am2ZpO3LCd.png)
