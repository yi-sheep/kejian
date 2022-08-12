---
title: WPF深入2
date: 2022-06-16 17:49:00
tags: [教材,阶段一]
categories: c++
---

# wpf深入2

## 矩形

在Canvas中我们通过`Rectangle`就可以画一个矩形出来

```xaml
<Rectangle
     Width="100"
     Height="100"
     RadiusX="5"
     RadiusY="5"
     Fill="Blue"
     Stroke="Black"
     Canvas.Left="0"
     Canvas.Top="0"/>
```

| 属性    | 作用           | 例子             |
| ------- | -------------- | ---------------- |
| Width   | 矩形的宽度     | `Width="100"`    |
| Height  | 矩形的高度     | `Height="100"`   |
| RadiusX | 上下的圆角弧度 | `RadiusX="5"`    |
| RadiusY | 左右的圆角弧度 | `RadiusY="5"`    |
| Fill    | 填充颜色       | `Fill="Blue"`    |
| Stroke  | 边线颜色       | `Stroke="Black"` |

后端程序

```c#
Rectangle rect;//创建一个方块作为演示对象
rect = new Rectangle();
rect.Fill = Brushes.Red;
rect.Width = 50;
rect.Height = 50;
rect.RadiusX = 5;
rect.RadiusY = 5;
Carrier.Children.Add(rect);
```

练习：

画一个，长为200，宽为100，圆角为10，无填充的红色矩形

```xaml
<Rectangle
     Width="200"
     Height="100"
     RadiusX="10"
     RadiusY="10"
     Stroke="Red"
     Canvas.Left="0"
     Canvas.Top="0"/>
```

## 多边形

在Canvas中我们通过`Polygon`就可以画一个多边形出来

```xaml
<Polygon  
     Points="200,200 300,125 300,275 200,200"  
     Stroke="Purple"
     StrokeThickness="2">
     <Polygon.Fill>
           <SolidColorBrush Color="Blue" Opacity="0.1"/>
     </Polygon.Fill>
</Polygon>
```

| 属性            | 作用                     | 例子                                       |
| --------------- | ------------------------ | ------------------------------------------ |
| Points          | 设置多边形每一个点的坐标 | `Points="200,200 300,125 300,275 200,200"` |
| Stroke          | 多边形线的颜色           | `Stroke="Purple"`                          |
| Polygon.Fill    | 多边形填充颜色           | `<Polygon.Fill></Polygon.Fill>`            |
| SolidColorBrush | 控制颜色值               | `<SolidColorBrush Color="Blue"/>`          |
| Opacity         | 颜色的透明度             | `Opacity="0.1"`                            |

```c#
Polygon p = new Polygon();
// 通过p.Points.Add一个端点一个端点的添加
p.Points.Add(new Point(300, 200));
p.Points.Add(new Point(400, 125));
p.Points.Add(new Point(400, 275));
p.Points.Add(new Point(300, 200));
p.Stroke = new SolidColorBrush(Colors.White);
p.StrokeThickness = 2;
p.Fill = new SolidColorBrush(Colors.Red);
p.Fill.Opacity = 0.3;
this.Content = p;
```

练习

让用户决定图形的相关属性

![image-20220617112752804](https://s2.loli.net/2022/06/17/Gk18HgNjAfJqR9o.png)

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
    <Grid>
        <TextBlock HorizontalAlignment="Left" Margin="84,56,0,0" TextWrapping="Wrap" VerticalAlignment="Top"><Run Language="zh-cn" Text="长"/></TextBlock>
        <TextBox Name="j_w" HorizontalAlignment="Left" Margin="101,55,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="47"/>
        <TextBlock HorizontalAlignment="Left" Margin="164,56,0,0" TextWrapping="Wrap" VerticalAlignment="Top"><Run Language="zh-cn" Text="高"/></TextBlock>
        <TextBox Name="j_h" HorizontalAlignment="Left" Margin="181,55,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="47"/>
        <TextBlock HorizontalAlignment="Left" Margin="233,56,0,0" TextWrapping="Wrap" VerticalAlignment="Top"><Run Language="zh-cn" Text="圆角"/></TextBlock>
        <TextBox Name="j_r" HorizontalAlignment="Left" Margin="261,55,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="47"/>
        <TextBlock HorizontalAlignment="Left" Margin="84,85,0,0" TextWrapping="Wrap" VerticalAlignment="Top"><Run Language="zh-cn" Text="X"/></TextBlock>
        <TextBox Name="j_x" HorizontalAlignment="Left" Margin="101,84,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="47"/>
        <TextBlock HorizontalAlignment="Left" Margin="164,84,0,0" TextWrapping="Wrap" VerticalAlignment="Top"><Run Language="zh-cn" Text="Y"/></TextBlock>
        <TextBox Name="j_y" HorizontalAlignment="Left" Margin="181,83,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="47"/>
        <Button Content="添加" HorizontalAlignment="Left" Margin="245,81,0,0" VerticalAlignment="Top" Click="Button_Click_add_1"/>
        <TextBlock HorizontalAlignment="Left" Margin="80,158,0,0" TextWrapping="Wrap" VerticalAlignment="Top"><Run Language="zh-cn" Text="端点"/></TextBlock>
        <TextBox x:Name="p_dian" HorizontalAlignment="Left" Margin="108,157,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="200"/>
        <TextBlock HorizontalAlignment="Left" Margin="80,201,0,0" TextWrapping="Wrap" VerticalAlignment="Top"><Run Language="zh-cn" Text="颜色"/></TextBlock>
        <TextBox x:Name="p_color" HorizontalAlignment="Left" Margin="108,200,0,0" TextWrapping="Wrap" VerticalAlignment="Top" Width="47"/>
        <Button Content="添加" HorizontalAlignment="Left" Margin="176,199,0,0" VerticalAlignment="Top" Click="Button_Click_add_2"/>

        <Canvas x:Name="canvas" HorizontalAlignment="Right" Height="300" Width="300">
            <Border BorderBrush="Black" BorderThickness="1" Height="300" Width="300"/>
        </Canvas>
    </Grid>
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

        private void Button_Click_add_1(object sender, RoutedEventArgs e)
        {
            Rectangle rect;//创建一个方块作为演示对象
            rect = new Rectangle();
            rect.Fill = Brushes.Black;
            rect.Width = int.Parse(j_w.Text);
            rect.Height = int.Parse(j_h.Text);
            rect.RadiusX = int.Parse(j_r.Text);
            rect.RadiusY = int.Parse(j_r.Text);
            Canvas.SetTop(rect, int.Parse(j_h.Text));
            Canvas.SetLeft(rect, int.Parse(j_x.Text));
            canvas.Children.Add(rect);
        }
        private void Button_Click_add_2(object sender, RoutedEventArgs e)
        {
            Polygon p = new Polygon();
            string[] a = p_dian.Text.Split(' ');
            for(int i = 0; i < a.Length; i++)
            {
                int x = int.Parse(a[i].Split(',')[0]);
                int y = int.Parse(a[i].Split(',')[1]);
                p.Points.Add(new Point(x, y));

            }
            if (p_color.Text == "红")
            {
                p.Stroke = Brushes.Red;
            }
            p.StrokeThickness = 2;
            canvas.Children.Add(p);
        }

    }
}
```

