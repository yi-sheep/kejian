---
title: c++阶段五第十三讲
date: 2022-06-08 10:25:04
tags: [教材,阶段五]
categories: c++
---

# 第十三讲

实现点击图片加载大图

- 给图片加点击事件
- 点击后获取到图片控件加载的图片地址
- 新建窗口，接收一个图片地址
- 动态更新窗口大小
- 加载图片

## 图片点击

图片并没有`Click`看上去好像没办法加上点击事件

`MouseDown`在使用方法上和`Click`类似，它可以让非按钮控件设置点击事件。

```xaml
<Image MouseDown="img_MouseDown"/>
```

```cs
private void img_MouseDown(object sender, MouseButtonEventArgs e)
{
    
}
```

## 获取控件

在点击事件中第一个参数`object sender`就是我们点击的控件。

```cs
private void img_MouseDown(object sender, MouseButtonEventArgs e)
{
    MessageBox.Show(sender.ToString());
    MessageBox.Show(((Image)sender).Source.ToString());
}
```

## 新窗口

在新的窗口中需要接收一个字符串，就是图片的地址。

```cs
using System;
using System.Collections.Generic;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Shapes;

namespace 图库
{
    /// <summary>
    /// ShowImage.xaml 的交互逻辑
    /// </summary>
    public partial class ShowImage : Window
    {
        public ShowImage(string url)
        {
            InitializeComponent();
        }
    }
}
```

跳转到新窗口

```c++
private void img_MouseDown(object sender, MouseButtonEventArgs e)
{
    ShowImage si = new ShowImage(((Image)sender).Source.ToString());
    si.Show();
}
```

## 动态窗口大小

通过`BitmapImage`对象可以得到图片的宽度和高度，再通过`this`指代当前窗口，可以设置高和宽。

```cs
public ShowImage(string url)
{
    InitializeComponent();
    BitmapImage i = new BitmapImage(new Uri(url));
    this.Width = i.Width;
    this.Height = i.Height;
}
```

## 加载图片

在新窗口页面中加入一个`image`控件，可以给控件设置图片`Stretch`伸缩方式为`None`不伸缩

```xaml
<Image x:Name="img" Stretch="None"/>
```

后端程序中加载图片

```cs
public ShowImage(string url)
{
    InitializeComponent();
    BitmapImage i = new BitmapImage(new Uri(url));
    this.Width = i.Width;
    this.Height = i.Height;
    img.Source = i;
}
```

