---
title: WPF深入5
date: 2022-06-23 12:53:23
tags: [教材,阶段一]
categories: c++
---

# WPF深入5

## 动画

动画可分为：`简单线性动画` `关键帧动画` `路径动画`

动画要素：针对对象的某一个属性连续变化（依赖属性）必须要有对应的类型动画类

|                类名                |               类名               |
| :--------------------------------: | :------------------------------: |
|   BooleanAnimationUsingKeyFrames   |          ByteAnimation           |
|    ByteAnimationUsingKeyFrames     |   CharAnimationUsingKeyFrames    |
|           ColorAnimation           |   ColorAnimationUsingKeyFrames   |
|          DecimalAnimation          |  DecimalAnimationUsingKeyFrames  |
|          DoubleAnimation           |  DoubleAnimationUsingKeyFrames   |
|      DoubleAnimationUsingPath      |          Int16Animation          |
|   Intl 6AnimationUsingKeyFrames    |          Int32Animation          |
|    Int32AnimationUsingKeyFrames    |          Int64Animation          |
|    Int64AnimationUsingKeyFrames    |  MatrixAnimationUsingKeyFrames   |
|      MatrixAnimationUsingPath      | ObjectAnimationUsingKeyFrames .  |
|           PointAnimation           |   PointAnimationUsingKeyFrames   |
|      PointAnimationUsingPath       |         Point3DAnimation         |
|   Point3DAnimationUsingKeyFrames   |       QuarternionAnimation       |
| QuarternionAnimationUsingKeyFrames |          RectAnimation           |
|    RectAnimationUsingKeyFrames     |       Rotation3DAnimation        |
| Rotation3DAnimationUsingKeyFrames  |         SingleAnimation          |
|   SingleAnimationUsingKeyFrames    |          SizeAnimation           |
|    SizeAnimationUsingKeyFrames     |  StringAnimationUsingKeyFrames   |
|         ThicknessAnimation         | ThicknessAnimationUsingKeyFrames |
|          VectorAnimation           |  VectorAnimationUsingKeyFrames   |
|         Vector3DAnimation          | Vector3DAnimationUsingKeyFrames  |

## 贪吃蛇

### 创建游戏区

让我们从 XAML 开始 - 一个在 Border 控件内带有 Canvas 面板的简单窗口，以创建游戏区域：

```xaml
<Window x:Class="WpfTutorialSamples.Games.SnakeWPFSample"       xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"     xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
        xmlns:local="clr-namespace:WpfTutorialSamples.Games"  
        mc:Ignorable="d"
        Title="贪吃蛇"
        SizeToContent="WidthAndHeight">  
    <Border BorderBrush="Black" BorderThickness="5">  
        <Canvas Name="GameArea" ClipToBounds="True" Width="400" Height="400">
        </Canvas>  
    </Border>  
</Window>
```

![image-20220627095620717](https://s2.loli.net/2022/06/27/anmhPlQWZpOrDEU.png)

我们使用 Canvas 作为实际的游戏区域，因为它允许我们向其中添加控件，我们可以完全控制位置。我们稍后会使用它，但现在，请注意以下事项：

- 没有为窗口定义宽度/高度 - 相反，我们为画布定义了它，因为这是我们需要完全控制的部分。然后，我们通过将**SizeToContent**属性设置为**WidthAndHeight**来确保 Window 将相应地调整其大小。如果我们改为定义窗口的宽度/高度，则其中的可用空间将取决于操作系统用于 Windows 的边框大小，这可能取决于主题等。
- 我们将Canvas的**ClipToBounds**属性设置为 True - 这很重要，否则我们添加的控件将能够扩展到 Canvas 面板的边界之外

### 绘制背景

我想要游戏区域的棋盘背景。它由许多正方形组成，因此从后端代码中添加它会更容易（或使用图像，但这不是那么动态！）。我们需要在 Window 内的所有控件都初始化/渲染后立即执行此操作，对我们来说幸运的是，Window 有一个事件：**ContentRendered**事件。我们将在 Window 标签中订阅它：

```xaml
<Window 
    ...
    ContentRendered="Window_ContentRendered">
    ...
</Window>
```

首先，我们需要定义在绘制蛇、背景方块等时使用的大小。它可以在 Window 类的顶部完成：

```c#
public partial class MainWindow : Window
{
    /// <summary>
    /// 蛇身每一个方块的大小
    /// </summary>
    const int SnakeSquareSize = 20;
    public MainWindow()
    {
        InitializeComponent();
    }
}
```

现在，在我们的**ContentRendered**事件中，我们将调用**DrawGameArea()**方法，它将完成所有地图绘制工作。它看起来像这样：

```c#
/// <summary>
/// 窗口内容渲染
/// </summary>
/// <param name="sender"></param>
/// <param name="e"></param>
private void Window_ContentRendered(object sender, EventArgs e)
{
    DrawGameArea();
}
/// <summary>
/// 地图绘制
/// </summary>
private void DrawGameArea()
{
    // 即将要画的图形坐标
    int nextX = 0, nextY = 0;
    // 创建一个方块对象
    Rectangle rect = new Rectangle();
    // 方块的宽度
    rect.Width = SnakeSquareSize;
    // 方块的高度
    rect.Height = SnakeSquareSize;
    // 方块的填充颜色
    rect.Fill = Brushes.Black;

    // 将方块作为子控件添加到画板中
    GameArea.Children.Add(rect);
    // 给当前这个方块设置位置坐标
    Canvas.SetTop(rect, nextY);
    Canvas.SetLeft(rect, nextX);
}
```

画完整的地图

```c#
/// <summary>
/// 地图绘制
/// </summary>
private void DrawGameArea()
{
    // 是否绘制完成
    bool doneDrawingBackground = false;
    // 即将要画的图形坐标
    int nextX = 0, nextY = 0;

    // 循环直到绘图完成
    while (!doneDrawingBackground)
    {
        // 创建一个方块对象
        Rectangle rect = new Rectangle();
        // 方块的宽度
        rect.Width = SnakeSquareSize;
        // 方块的高度
        rect.Height = SnakeSquareSize;
        // 方块的填充颜色
        rect.Fill = Brushes.Black;

        // 将方块作为子控件添加到画板中
        GameArea.Children.Add(rect);
        // 给当前这个方块设置位置坐标
        Canvas.SetTop(rect, nextY);
        Canvas.SetLeft(rect, nextX);
        // 将下一个要画的方块x坐标更改为下一个坐标
        nextX += SnakeSquareSize;
        // 检测是否达到最右边
        if (nextX >= GameArea.ActualWidth)
        {
            // 将下一个的x坐标变为0
            nextX = 0;
            // 将下一个的y坐标增加
            nextY += SnakeSquareSize;
        }
        // 检测是否达到最下边
        if (nextY >= GameArea.ActualHeight)
        {
            // 设置绘图完成
            doneDrawingBackground = true;
        }
    }
}
```

![image-20220627103047015](https://s2.loli.net/2022/06/27/cgqxIGuDQtjTMi8.png)

黑白地图

```c#
/// <summary>
/// 地图绘制
/// </summary>
private void DrawGameArea()
{
    // 是否绘制完成
    bool doneDrawingBackground = false;
    // 即将要画的图形坐标
    int nextX = 0, nextY = 0;
    // 即将要画的方块是否是第奇数个
    bool nextIsOdd = false;

    // 循环直到绘图完成
    while (!doneDrawingBackground)
    {
        // 创建一个方块对象
        Rectangle rect = new Rectangle();
        // 方块的宽度
        rect.Width = SnakeSquareSize;
        // 方块的高度
        rect.Height = SnakeSquareSize;
        // 方块的填充颜色
        rect.Fill = nextIsOdd ? Brushes.White : Brushes.Black;

        // 将方块作为子控件添加到画板中
        GameArea.Children.Add(rect);
        // 给当前这个方块设置位置坐标
        Canvas.SetTop(rect, nextY);
        Canvas.SetLeft(rect, nextX);
        // 将下一个要画的方块x坐标更改为下一个坐标
        nextX += SnakeSquareSize;
        // 切换一下奇偶
        nextIsOdd = !nextIsOdd;
        // 检测是否达到最右边
        if (nextX >= GameArea.ActualWidth)
        {
            // 将下一个的x坐标变为0
            nextX = 0;
            // 将下一个的y坐标增加
            nextY += SnakeSquareSize;
            // 切换一下奇偶
            nextIsOdd = !nextIsOdd;
        }
        // 检测是否达到最下边
        if (nextY >= GameArea.ActualHeight)
        {
            // 设置绘图完成
            doneDrawingBackground = true;
        }
    }
}
```

![image-20220627103310428](https://s2.loli.net/2022/06/27/q5Lpc9XGDQZ2wMo.png)
