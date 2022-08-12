---
title: c++阶段五第十一讲
date: 2022-05-19 19:36:49
tags: [教材,阶段五]
categories: c++
---

# 第十一讲

## StackPanel

这是一个布局

使用方法如下

```xaml
<StackPanel>
            
</StackPanel>
```

在这个布局中可以写下一些控件，比如

```xaml
<StackPanel>
    <Button Content="按钮1" Width="80" Height="30"/>
    <Button Content="按钮2" Width="80" Height="30"/>
    <Button Content="按钮3" Width="80" Height="30"/>
    <Button Content="按钮4" Width="80" Height="30"/>
</StackPanel>
```

![image-20220519194917195](https://s2.loli.net/2022/05/19/Jv3pinOf87WzKwl.png)

可以看出来写在`StackPanel`中的按钮控件被整齐的竖直排列了，当然也可以横向只需要在标签上设置`Orientation="Horizontal"`

```xaml
<StackPanel Orientation="Horizontal">
    <Button Content="按钮1" Width="80" Height="30"/>
    <Button Content="按钮2" Width="80" Height="30"/>
    <Button Content="按钮3" Width="80" Height="30"/>
    <Button Content="按钮4" Width="80" Height="30"/>
</StackPanel>
```

![image-20220519195225309](https://s2.loli.net/2022/05/19/meWOlbHwYaJSIgf.png)

## 练习

```xaml
<Window x:Class="图库.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:图库"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Grid>
        <StackPanel Orientation="Horizontal">
            <StackPanel HorizontalAlignment="Left">
                <Button Content="按钮1" Width="80" Height="30"/>
                <Button Content="按钮2" Width="80" Height="30"/>
                <Button Content="按钮3" Width="80" Height="30"/>
                <Button Content="按钮4" Width="80" Height="30"/>
            </StackPanel>
            <StackPanel>
            </StackPanel>
        </StackPanel>
        
    </Grid>
</Window>
```

## 图片

`Image`:单标签，用于加载图片

| 名称   | 作业     |
| ------ | -------- |
| Source | 加载图片 |

加载网络图片

```xmal
<Image Source="网络图片地址"/>
```

加载本地图片

```xmal
<Image Source="本地图片地址"/>
```

后端程序加载图片

```cs
// image.Source = "地址"; 是不行的
// 创建一个位图对象
BitmapImage i = new BitmapImage(new Uri("图片的地址"));
image.Source = i;
```

Uri对象接收两个参数

第一个参数：图片的地址

第二个参数：图片地址规则，有Absolute（绝对定位）Relative（相对位置）RelativeOrAbsolute（相对和绝对）

```
https://images6.alphacoders.com/122/thumb-1920-1224268.jpg
https://images8.alphacoders.com/121/thumb-1920-1214264.jpg
https://images5.alphacoders.com/120/thumb-1920-1205663.jpg
https://images2.alphacoders.com/122/thumb-1920-1224918.jpg
https://images4.alphacoders.com/121/thumb-1920-1217455.jpg
```

## 练习

<img src="https://mfiles.alphacoders.com/971/thumb-1920-971566.jpg" style="zoom:25%;" />

![image-20220519201406356](https://s2.loli.net/2022/05/19/8ZhWQGLV3i4JuRk.png)

前端

```xaml
<Window x:Class="图库.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:图库"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Grid>
        <StackPanel Orientation="Horizontal">
            <StackPanel HorizontalAlignment="Left">
                <Button Content="按钮1" Width="80" Height="30"/>
                <Button Content="按钮2" Width="80" Height="30"/>
                <Button Content="按钮3" Width="80" Height="30"/>
                <Button Content="按钮4" Width="80" Height="30"/>
            </StackPanel>
            <StackPanel>
                <StackPanel Orientation="Horizontal">
                    <Image x:Name="img1" Width="120" Height="200"/>
                    <Image x:Name="img2" Width="120" Height="200"/>
                    <Image x:Name="img3" Width="120" Height="200"/>
                    <Image x:Name="img4" Width="120" Height="200"/>
                    <Image x:Name="img5" Width="120" Height="200"/>
                    <Image x:Name="img6" Width="120" Height="200"/>
                </StackPanel>
                <StackPanel Margin="0,10,0,0"  Orientation="Horizontal">
                    <Image x:Name="img7" Width="120" Height="200"/>
                    <Image x:Name="img8" Width="120" Height="200"/>
                    <Image x:Name="img9" Width="120" Height="200"/>
                    <Image x:Name="img10" Width="120" Height="200"/>
                    <Image x:Name="img11" Width="120" Height="200"/>
                    <Image x:Name="img12" Width="120" Height="200"/>
                </StackPanel>
            </StackPanel>
        </StackPanel>
        
    </Grid>
</Window>
```

后端

```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace 图库
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
            BitmapImage i = new BitmapImage(new Uri("https://mfiles.alphacoders.com/971/thumb-1920-971566.jpg"));
            img1.Source = i;
            img2.Source = i;
            img3.Source = i;
            img4.Source = i;
            img5.Source = i;
            img6.Source = i;
            img7.Source = i;
            img8.Source = i;
            img9.Source = i;
            img10.Source = i;
            img11.Source = i;
            img12.Source = i;
        }
    }
}
```

