---
title: WPF深入
date: 2022-06-16 16:42:00
tags: [教材,阶段一]
categories: c++
---

# wpf深入

## Canvas

画板布局：定义区域，子元素的显示位置，指定相对于画板的坐标，来定位子元素的位置

附加属性：

`Canvas.Left`设置控件在布局中距离左边的距离

`Canvas.Right`设置控件在布局中距离右边的距离

`Canvas.Top`设置控件在布局中距离上边的距离

`Canvas.Bottom`设置控件在布局中距离下边的距离

不能为子元素指定两个以上的附加属性，如果指定了，忽略后者

如

```xaml
<Canvas>
    <TextBlock 
               Canvas.Top="100" 
               Canvas.Left="240"/>
</Canvas>
```

当窗口大小变化，Canvas的尺寸就随之变动，子元素的位置也变化，坐标相对于Canvas没有变。支持负坐标。

重叠效果 优先显示：后添加的元素显示在上面，如果要改变默认优先级：Panel.Zlndex 默认值 0 

改变优先显示顺序 Panel.Zlndex值越大，就显示在最上边 Panel.Zlndex相同，后添加的在上边

## 线

在Canvas中我们通过`Line`就可以画一条线出来

```xaml
<Canvas Height="300" Width="300">

  <!-- 绘制一条对角线 (10,10) 到 (50,50). -->
  <Line
    X1="10" Y1="10"
    X2="50" Y2="50"
    Stroke="Black"
    StrokeThickness="4" />

  <!-- 绘制一条对角线 (10,10) 到 (50,50)
       并将其向右移动 100 像素。 -->
  <Line
    X1="10" Y1="10"
    X2="50" Y2="50"
    StrokeThickness="4"
    Stroke="Black"
    Canvas.Left="100"/>

  <!-- Draws a horizontal line from (10,60) to (150,60). -->
  <Line
     X1="10" Y1="60"
     X2="150" Y2="60"
     Stroke="Black"
     StrokeThickness="4"/>

</Canvas>
```

| 属性            | 作用       | 例子                  |
| --------------- | ---------- | --------------------- |
| X1，Y1          | 起点的坐标 | `X1="10" Y1="10"`     |
| X2，Y2          | 终点的坐标 | `X2="50" Y2="50"`     |
| StrokeThickness | 线的厚度   | `StrokeThickness="4"` |
| Stroke          | 线的颜色   | Stroke="Black"        |

练习：

在屏幕上显示一条线，要求：大小为2，颜色为蓝色

```xaml
<Line
     X1="10" Y1="60"
     X2="150" Y2="60"
     Stroke="Blue"
     StrokeThickness="2"/>
```

在屏幕上显示一个正方形（边框），要求边长为100，颜色为红色

```xaml
<Line
      X1="10" Y1="8"
      X2="10" Y2="52"
      Stroke="Black"
      StrokeThickness="4" />
<Line
      X1="10" Y1="10"
      X2="50" Y2="10"
      Stroke="Black"
      StrokeThickness="4" />
<Line
      X1="50" Y1="8"
      X2="50" Y2="52"
      Stroke="Black" 
      StrokeThickness="4" />
<Line
      X1="10" Y1="50"
      X2="50" Y2="50"
      Stroke="Black"
      StrokeThickness="4" />
```

## 后端程序中去画线

```c#
// Add a Line Element
myLine = new Line();
myLine.Stroke = Brushes.Black; // 设置颜色
// 设置开始坐标
myLine.X1 = 1;
myLine.Y1 = 1;
// 设置结束坐标
myLine.X2 = 50;
myLine.Y2 = 50;
// 设置垂直和横向的规则
myLine.HorizontalAlignment = HorizontalAlignment.Left;
myLine.VerticalAlignment = VerticalAlignment.Center;
// 线的宽度
myLine.StrokeThickness = 2;
// 将线添加进布局中
myGrid.Children.Add(myLine);
```

| 属性         | 作用                       | 例子                           |
| ------------ | -------------------------- | ------------------------------ |
| Brushes      | 选择颜色                   | `Brushes.Black`                |
| Children.Add | 向某一个布局中添加一个控件 | `myGrid.Children.Add(myLine);` |

在屏幕上显示一个正方形（实心），要求边长为100，边框颜色为红色，填充颜色为蓝色

```c#
int x1 = 10, x2 = 10;
for(int i = 0; i < 6; i++)
{
    Line p = new Line();
    p.StrokeThickness = 8;
    p.Stroke = Brushes.Black;
    p.Y1 = 8;
    p.Y2 = 52;
    p.X1 = x1;
    p.X2 = x2;
    canvas.Children.Add(p);
    x1 += 7;
    x2 += 7;
}
```

实现让用户输入线的参数

![image-20220616174523031](https://s2.loli.net/2022/06/16/1o3aVQkrbc8KwHv.png)

前端

```xaml
<Window x:Class="暑假.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:暑假"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Canvas x:Name="canvas" HorizontalAlignment="Right" Height="300" Width="300">
        <TextBlock Canvas.Left="-422" TextWrapping="Wrap" Canvas.Top="54"><Run Language="zh-cn" Text="X1"/></TextBlock>
        <TextBlock Canvas.Left="-327" TextWrapping="Wrap" Canvas.Top="54" HorizontalAlignment="Left" VerticalAlignment="Top"><Run Language="zh-cn" Text="Y"/><Run Text="1"/></TextBlock>
        <TextBox x:Name="x1" Canvas.Left="-399" TextWrapping="Wrap" Canvas.Top="54" Width="52" HorizontalAlignment="Left" VerticalAlignment="Top"/>
        <TextBox x:Name="y1" Canvas.Left="-298" TextWrapping="Wrap" Canvas.Top="54" Width="52" HorizontalAlignment="Left" VerticalAlignment="Top"/>
        <TextBlock Canvas.Left="-422" TextWrapping="Wrap" Canvas.Top="85" HorizontalAlignment="Center" VerticalAlignment="Top"><Run Text="X"/><Run Language="zh-cn" Text="2"/></TextBlock>
        <TextBlock Canvas.Left="-327" TextWrapping="Wrap" Canvas.Top="85" HorizontalAlignment="Center" VerticalAlignment="Top"><Run Text="Y"/><Run Language="zh-cn" Text="2"/></TextBlock>
        <TextBox x:Name="x2" Canvas.Left="-399" TextWrapping="Wrap" Canvas.Top="85" Width="52" HorizontalAlignment="Center" VerticalAlignment="Top"/>
        <TextBox x:Name="y2" Canvas.Left="-298" TextWrapping="Wrap" Canvas.Top="85" Width="52" HorizontalAlignment="Center" VerticalAlignment="Top"/>
        <TextBlock Canvas.Left="-422" TextWrapping="Wrap" Canvas.Top="117" HorizontalAlignment="Center" VerticalAlignment="Top"><Run Language="zh-cn" Text="线的宽度"/></TextBlock>
        <TextBox x:Name="width" Canvas.Left="-365" TextWrapping="Wrap" Canvas.Top="116" Width="52" HorizontalAlignment="Left" VerticalAlignment="Top"/>
        <TextBlock Canvas.Left="-422" TextWrapping="Wrap" Canvas.Top="139" HorizontalAlignment="Center" VerticalAlignment="Top"><Run Text="线的"/><Run Language="zh-cn" Text="线的颜色"/></TextBlock>
        <TextBox x:Name="color" Canvas.Left="-345" TextWrapping="Wrap" Canvas.Top="139" Width="52" HorizontalAlignment="Left" VerticalAlignment="Top"/>
        <TextBlock Canvas.Left="-404" TextWrapping="Wrap" Canvas.Top="154" FontSize="9"><Run Language="zh-cn" Text="红绿蓝选一个"/></TextBlock>
        <Button Content="确定" Canvas.Left="-363" Canvas.Top="205" Click="Button_Click"/>
        <Border BorderBrush="Black" BorderThickness="1" Height="300" Width="300"/>
    </Canvas>

</Window>
```

后端

```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace 暑假
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {

        public MainWindow()
        {
            InitializeComponent();
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            Line p = new Line();
            p.X1 = int.Parse(x1.Text);
            p.Y1 = int.Parse(y1.Text);
            p.X2 = int.Parse(x2.Text);
            p.Y2 = int.Parse(y2.Text);
            p.StrokeThickness = int.Parse(width.Text);
            if (color.Text == "红")
            {
                p.Stroke = Brushes.Red;
            }
            else if (color.Text == "绿")
            {
                p.Stroke = Brushes.Green;
            }
            else if (color.Text == "蓝")
            {
                p.Stroke = Brushes.Blue;
            }
            canvas.Children.Add(p);
        }
    }
}
```

