---
title: 阶段五第七讲
date: 2022-04-01 10:03:43
tags: [教材,阶段五]
categories: c++
---

# 第七讲

## WPF应用

### 文字

`TextBlock`:文字标签，可以在界面上显示文字，用户无法修改文字

`TextBox`:文字输入标签，可以在界面上显示一个文字输入框，用户可以输入对应的文字

对应属性：

| 名字       | 范围 | 作用                 |
| ---------- | ---- | -------------------- |
| Text       | 通用 | 设置标签里的文字内容 |
| FontSize   | 通用 | 设置标签里的文字大小 |
| FontWeight | 通用 | 设置标签里的文字样式 |

### 按钮

`Button`:按钮标签，可以在界面上显示一个按钮，用户可以点击这个按钮

> 除了按钮以外几乎所有的标签都可以设置点击事件，但是没有按钮的点击特效

| 名字    | 范围   | 作用                   |
| ------- | ------ | ---------------------- |
| Content | Button | 设置按钮的文字内容     |
| Click   | 通用   | 设置标签的点击事件函数 |

> 点击事件函数必须创建在对应的cs文件里，才能触发

本节课效果：

![image-20220401140755831](https://gitee.com/gaoxianglong/picgo/raw/master/img/image-20220401140755831.png)MainWindows.xaml

```xaml
<Window x:Class="WpfApp2.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WpfApp2"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Grid>
        <TextBlock HorizontalAlignment="Center" Margin="0,86,0,0" Text="身份证管理系统" TextWrapping="Wrap" VerticalAlignment="Top" FontSize="24" FontWeight="Bold"/>
        <StackPanel Margin="0,154,0,0" Height="123" HorizontalAlignment="Center" VerticalAlignment="Top">
            <StackPanel x:Name="userName" Width="180" Height="24" Orientation="Horizontal" VerticalAlignment="Stretch" Margin="0,10,0,10">
                <TextBlock Text="用户名：" TextWrapping="Wrap" VerticalAlignment="Center"/>
                <TextBox x:Name="userNameInput" Text="123456" TextWrapping="Wrap" Width="120" VerticalAlignment="Center"/>
            </StackPanel>
            <StackPanel x:Name="password" Width="180" Height="24" Orientation="Horizontal" VerticalAlignment="Stretch" Margin="0,10,0,10">
                <TextBlock Text="密码    ：" TextWrapping="Wrap" VerticalAlignment="Center"/>
                <TextBox x:Name="passwordIput" Text="123456" TextWrapping="Wrap" Width="120" VerticalAlignment="Center"/>
            </StackPanel>
            <Button VerticalAlignment="Stretch" HorizontalAlignment="Center" Content="登录" Click="Button_Click" />
        </StackPanel>

    </Grid>
</Window>
```

MainWindows.xaml.cs

```csharp
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

namespace WpfApp2
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
            WindowStartupLocation = System.Windows.WindowStartupLocation.CenterScreen;
        }
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            if (userNameInput.Text == "123456" && passwordIput.Text == "123456")
            {
                this.Content = new guanliyuan();
            }
            else
            {
                MessageBox.Show("没有这个用户","错误");
            }
        }
    }
}
```

