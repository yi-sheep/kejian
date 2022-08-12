---
title: c++阶段四第十一讲
date: 2022-05-19 18:09:39
tags: [教材,阶段四]
categories: c++
---

# 第十一讲

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

练习

点击按钮切换图片

前端

```xaml
<Window x:Class="HelloWPF.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:HelloWPF"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Grid>
        <Image x:Name="image" Source="https://img.zcool.cn/community/0169ec5ca46bb8a8012141685daea4.jpg@1280w_1l_2o_100sh.jpg"/>
        <Button Content="下一张" Width="100" Height="30" Click="Button_Click" VerticalAlignment="Bottom" HorizontalAlignment="Right"/>
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

namespace HelloWPF
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        string[] imgUri = {
        "https://images6.alphacoders.com/122/thumb-1920-1224268.jpg",
        "https://images8.alphacoders.com/121/thumb-1920-1214264.jpg",
        "https://images5.alphacoders.com/120/thumb-1920-1205663.jpg",
        "https://images2.alphacoders.com/122/thumb-1920-1224918.jpg",
        "https://images4.alphacoders.com/121/thumb-1920-1217455.jpg"
        };
        int p = 0;
        public MainWindow()
        {
            InitializeComponent();
            BitmapImage i = new BitmapImage(new Uri(imgUri[p], UriKind.RelativeOrAbsolute));
            image.Source = i;
            p++;
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            
            BitmapImage i = new BitmapImage(new Uri(imgUri[p], UriKind.RelativeOrAbsolute));
            image.Source = i;
            p++;
            if (p == imgUri.Length)
            {
                p = 0;
            }
           
        }
    }
}
```

