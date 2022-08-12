---
title: c++阶段四第十三讲
date: 2022-06-07 10:30:18
tags: [教材,阶段四]
categories: c++
---

# 验证码

随机数

```c++
Random random = new Random(); // 创建一个随机数对象
random.Next(0, 10); // 参数0到10的数
```

整数转字符串

`ToString()`

![image-20220607105507756](https://s2.loli.net/2022/06/07/YgfRX1MpoFhLH4n.png)

前端

```xaml
<Window x:Class="WpfApp5.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WpfApp5"
        mc:Ignorable="d"
        Title="MainWindow"
        Height="450" 
        Width="800">
    <Grid>
        <TextBox
            x:Name="input"
            Width="100"
            Height="30"
            Margin="300,180,380,203"/>
        <TextBlock
            x:Name="text"
            Width="100"
            Height="30"
            Text="1111"
            Margin="420,180,300,203"/>
        <Button
            Width="50"
            Height="30"
            Content="刷新"
            HorizontalAlignment="Right"
            Click="Button_Click"/>
        <Button
            Width="50"
            Height="30"
            Content="确定"
            VerticalAlignment="Bottom"
            Click="Button_Click_1"/>

    </Grid>
</Window>
```

后端

```c++
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

namespace WpfApp5
{

    public partial class MainWindow : Window
    {
        Random random = new Random();
        public MainWindow()
        {
            InitializeComponent();
            text.Text = random.Next(1000, 9999).ToString();
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            text.Text = random.Next(1000, 9999).ToString();
        }

        private void Button_Click_1(object sender, RoutedEventArgs e)
        {
            if(text.Text == input.Text)
            {
                MessageBox.Show("正确");
                text.Text = random.Next(1000, 9999).ToString();
            }
            else
            {
                MessageBox.Show("错误");
            }
            
        }
    }
}
```

