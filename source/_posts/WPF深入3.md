---
title: WPF深入3
date: 2022-06-17 09:12:51
tags: [教材,阶段一]
categories: c++
---

# wpf深入3

## 圆

在Canvas中我们通过`Ellipse`就可以画一个圆出来

```xaml
<Ellipse
Fill="Yellow"
Height="100"
Width="200"
StrokeThickness="2"
Stroke="Black"/>
```

| 属性            | 作用         | 例子                  |
| --------------- | ------------ | --------------------- |
| Fill            | 圆的填充颜色 | `Fill="Yellow"`       |
| Height          | 圆的高度     | `Height="100"`        |
| Width           | 圆的宽度     | `Width="200"`         |
| StrokeThickness | 边框大小     | `StrokeThickness="2"` |
| Stroke          | 边框颜色     | `Stroke="Black"`      |

```c#
// 创建一个红色椭圆。
Ellipse myEllipse = new Ellipse();

// 创建一个红色的SolidColorBrush来填充椭圆。
SolidColorBrush mySolidColorBrush = new SolidColorBrush();

// 使用RGB值描述笔刷的颜色。
// 每个值的范围为0-255。
mySolidColorBrush.Color = Color.FromArgb(255, 255, 255, 0);
// 圆使用刚刚设置的颜色
myEllipse.Fill = mySolidColorBrush;
// 圆的边框大小
myEllipse.StrokeThickness = 2;
// 圆的边框颜色
myEllipse.Stroke = Brushes.Black;

// 设置椭圆的宽度和高度。
myEllipse.Width = 200;
myEllipse.Height = 100;

// 将椭圆添加到StackPanel。
myStackPanel.Children.Add(myEllipse);
```

## 路径

Path指定图形的路径是什么样的，可以通过`Path.Data`可以画出非常复杂的图形。

```xaml
<Path>
    <Path.Data>
    </Path.Data>
</Path>
```

### 线段、矩形和椭圆图形

线段

```xaml
<LineGeometry StartPoint="10,10" EndPoint="100,10"></LineGeometry>
```

| 属性       | 作用               | 例子                 |
| ---------- | ------------------ | -------------------- |
| StartPoint | 描述直线开始的坐标 | `StartPoint="10,10"` |
| EndPoint   | 描述直线结束的坐标 | `EndPoint="100,10"`  |

> 需要在path上设置边线颜色`Stroke`

```c#
// 创建线段对象
LineGeometry lineGeometry = new LineGeometry();
// 设置线段的开始坐标
lineGeometry.StartPoint = Point.Parse("10,10");
// 设置线段的结束坐标
lineGeometry.EndPoint = Point.Parse("100,10");
// 创建Path对象
Path path = new Path();
// 设置路径上的图形边线颜色
path.Stroke = Brushes.Pink;
// 设置路径上的图形边线大小
path.StrokeThickness = 5;
// 将路径设置为线段
path.Data = lineGeometry;
// 将当前窗口的内容修改为这个路径
this.Content = path;
```

矩形

```xaml
<RectangleGeometry Rect="0,0 100,50"></RectangleGeometry>
```

| 属性 | 作用                           | 例子                |
| ---- | ------------------------------ | ------------------- |
| Rect | 描述矩形的左上角和右下角的坐标 | `Rect="0,0 100,50"` |

> 需要在path上设置填充颜色`Fill`

```xaml
// 创建矩形对象
RectangleGeometry rectangleGeometry = new RectangleGeometry();
// 设置矩形左上角和右下角的坐标
rectangleGeometry.Rect = Rect.Parse("0,0 100,100");
// 创建Path对象
Path path = new Path();
// 设置路径上的图形填充颜色
path.Fill = Brushes.Pink;
// 将路径设置为线段
path.Data = rectangleGeometry;
// 将当前窗口的内容修改为这个路径
this.Content = path;
```

椭圆

```xaml
<EllipseGeometry Center="200,150" RadiusX="50" RadiusY="25"></EllipseGeometry>
```

| 属性    | 作用                  | 例子           |
| ------- | --------------------- | -------------- |
| Center  | 设置椭圆的开始坐标    | `Center="0,0"` |
| RadiusX | 设置椭圆的X轴上的长度 | `RadiusX="50"` |
| RadiusY | 设置椭圆的Y轴上的长度 | `RadiusY="25"` |

```c#
// 创建椭圆图形对象
EllipseGeometry ellipseGeometry = new EllipseGeometry();
// 设置椭圆开始坐标
ellipseGeometry.Center = Point.Parse("100,100");
// 设置椭圆X/Y轴上的长度
ellipseGeometry.RadiusX = 50;
ellipseGeometry.RadiusY = 20;
// 创建Path对象
Path path = new Path();
// 设置路径上的图形填充颜色
path.Fill = Brushes.Pink;
// 将路径设置为椭圆
path.Data = ellipseGeometry;
// 将当前窗口的内容修改为这个路径
this.Content = path;
```

### 使用GeometryGroup组合形状

如果窗口上有几百给图形，那么不仅要一个个写代码，而且在加载这些图形的时候也是一个个加载的，如果图形多了速度就会慢很多。

```xaml
<GeometryGroup FillRule="Nonzero">
    <EllipseGeometry Center="200,150" RadiusX="50" RadiusY="25"></EllipseGeometry>
    <RectangleGeometry Rect="200,150 250,200"></RectangleGeometry>
</GeometryGroup>
```

| 属性     | 作用                                                         | 例子                 |
| -------- | ------------------------------------------------------------ | -------------------- |
| FillRule | 设置图形重合后的显示方式，Nonzero：完全重合，EvenOdd：重合消除 | `FillRule="Nonzero"` |

```c#
// 创建矩形对象
RectangleGeometry rectangleGeometry = new RectangleGeometry();
// 设置矩形左上角和右下角的坐标
rectangleGeometry.Rect = Rect.Parse("0,0 100,100");
// 创建椭圆图形对象
EllipseGeometry ellipseGeometry = new EllipseGeometry();
// 设置椭圆开始坐标
ellipseGeometry.Center = Point.Parse("100,100");
// 设置椭圆X/Y轴上的长度
ellipseGeometry.RadiusX = 50;
ellipseGeometry.RadiusY = 20;
// 创建一个图形组合对象
GeometryGroup geometryGroup = new GeometryGroup();
// 将图形添加进组合对象
geometryGroup.Children.Add(rectangleGeometry);
geometryGroup.Children.Add(ellipseGeometry);
// 创建Path对象
Path path = new Path();
// 设置路径上的图形填充颜色
path.Fill = Brushes.Pink;
// 将路径设置为线段
path.Data = geometryGroup;
// 将当前窗口的内容修改为这个路径
this.Content = path;
```

### 使用CombinedGeometry融合几何形状

针对重合图形的特殊处理

```xaml
<CombinedGeometry GeometryCombineMode="Union">
    <CombinedGeometry.Geometry1>
        <EllipseGeometry Center="200,150" RadiusX="50" RadiusY="25"></EllipseGeometry>
    </CombinedGeometry.Geometry1>
    <CombinedGeometry.Geometry2>
        <RectangleGeometry Rect="200,150 250,200"></RectangleGeometry>
    </CombinedGeometry.Geometry2>
</CombinedGeometry>
```

| 属性                | 作用                          | 例子 |
| ------------------- | ----------------------------- | ---- |
| GeometryCombineMode | 设置重合图形的模式            |      |
| Union               | 重合                          |      |
| Exclude             | 消除`Geometry2`以及重合的部分 |      |
| Intersect           | 保留重合的部分                |      |
| Xor                 | 消除重合的部分                |      |

```c#
// 创建矩形对象
RectangleGeometry rectangleGeometry = new RectangleGeometry();
// 设置矩形左上角和右下角的坐标
rectangleGeometry.Rect = Rect.Parse("0,0 100,100");
// 创建椭圆图形对象
EllipseGeometry ellipseGeometry = new EllipseGeometry();
// 设置椭圆开始坐标
ellipseGeometry.Center = Point.Parse("100,100");
// 设置椭圆X/Y轴上的长度
ellipseGeometry.RadiusX = 50;
ellipseGeometry.RadiusY = 20;
// 创建图形融合对象
CombinedGeometry combinedGeometry = new CombinedGeometry();
// 设置第一个图形
combinedGeometry.Geometry1 = rectangleGeometry;
// 设置第二个图形
combinedGeometry.Geometry2 = ellipseGeometry;
// 设置图形融合模式
combinedGeometry.GeometryCombineMode = GeometryCombineMode.Xor;
// 创建Path对象
Path path = new Path();
// 设置路径上的图形填充颜色
path.Fill = Brushes.Pink;
// 将路径设置为线段
path.Data = combinedGeometry;
// 将当前窗口的内容修改为这个路径
this.Content = path;
```

### 使用PathGeometry绘制曲线和直线

PathGeometry可以画出上面的所有图形

线段

```xaml
<PathGeometry>
    <PathFigure StartPoint="0,0">
        <LineSegment Point="100,100"></LineSegment>
    </PathFigure>
</PathGeometry>
```

| 属性        | 作用                 | 例子               |
| ----------- | -------------------- | ------------------ |
| StartPoint  | 设置路径的起点       | `StartPoint="0,0"` |
| IsFilled    | 设置是否显示填充颜色 |                    |
| IsClosed    | 设置是否自动闭合路径 |                    |
| LineSegment | 线段路径             |                    |
| Point       | 设置端点坐标         | `Point="100,100"`  |

曲线

```xaml
<PathGeometry>
    <PathFigure StartPoint="0,0">
        <ArcSegment Point="100,100" Size="200,500" IsLargeArc="True"></ArcSegment>
        <ArcSegment Point="200,0" Size="200,500" IsLargeArc="True"></ArcSegment>
    </PathFigure>
</PathGeometry>
```

| 属性       | 作用                      | 例子                |
| ---------- | ------------------------- | ------------------- |
| Point      | 设置路径端点的坐标        | `Point="100,100"`   |
| Size       | 设置曲线的椭圆的X/Y的半径 | `Size="200,500"`    |
| IsLargeArc | 设置大圆还是小圆          | `IsLargeArc="True"` |

### 微语言几何图形

线段

```xaml
<Path Fill="Yellow" Stroke="Pink" Data="M0,0 L0,100 100,100 100,0 Z"></Path>
```

弧线

```xaml
<Path Fill="Yellow" Stroke="Pink" Data="M0,100 A50,25,0,0,1,100,100 Z"></Path>
```

| 属性                                    | 作用                                                         | 例子                     |
| --------------------------------------- | ------------------------------------------------------------ | ------------------------ |
| F v                                     | 设置图形重合后的显示方式，Nonzero(1)：完全重合，EvenOdd(0)：重合消除 | `F0`                     |
| M x,y                                   | 描述几何图形的开始坐标                                       | `M0,0`                   |
| L x,y                                   | 创建一个线段的端点                                           | `L10,10`                 |
| H x                                     | 创建一条横线，指定x的长度即可                                | `H100`                   |
| V y                                     | 创建一条竖线，指定y的长度即可                                | `V100`                   |
| A rx,ry,Angle,ArcFlag,DirectionFlag,x,y | 创建一条圆弧参数依次是：x半径，y半径，偏移角度，弧度大小标志，方向标志 | `A50,25,0,0,1,100,100 Z` |
| Z                                       | 结束当前几何图形路径                                         | `Z`                      |

