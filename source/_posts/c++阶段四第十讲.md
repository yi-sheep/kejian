---
title: c++阶段四第十讲
date: 2022-05-12 20:53:54
tags: [教材,阶段四]
categories: c++
---

# 第十讲

## Windows桌面程序

Windows Presentation Foundation 是创建桌面客户端应用程序的 UI 框架。 **WPF** 开发平台支持广泛的应用开发功能，包括应用模型、资源、控件、图形、布局、数据绑定、文档和安全性。

### 创建第一个wpf应用程序

![20220512210405.png](https://s2.loli.net/2022/05/12/ETHrD1MWwPG5d4O.png)

```xaml
<Window x:Class="HelloWPF.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:HelloWPF"
        mc:Ignorable="d"
        Title="MainWindow" 
        Height="450" Width="800">
    
    <Grid>
        
    </Grid>
</Window>
```

| 名称   | 描述                                                       |
| :----- | ---------------------------------------------------------- |
| Window | 窗口标签，在这个标签的开始标签里可以设置很多窗口相关的属性 |
| Title  | 设置窗口的标题                                             |
| Height | 设置窗口的高度                                             |
| Width  | 设置窗口的宽度                                             |
| Grid   | 网格布局,将页面上需要显示的控件，按照一定格式排列显示      |

在`Grid`标签中显示`Hello,world!`

```xaml
<Window x:Class="HelloWPF.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:HelloWPF"
        mc:Ignorable="d"
        Title="MainWindow" 
        Height="450" Width="800">
    
    <Grid>
        <Label
            Content="Hello,world!"/>
    </Grid>
</Window>
```

| 名称                | 描述                                                         |
| ------------------- | ------------------------------------------------------------ |
| Label               | 标记标签，用于在页面上显示内容                               |
| Content             | 设置标记标签的显示内容                                       |
| Height              | 设置控件的高度                                               |
| Width               | 设置控件的宽度                                               |
| HorizontalAlignment | 设置控件内容横向的排列规则，Center(居中)、Left(左)、Right(右)、Stretch(伸展,默认的) |
| VerticalAlignment   | 设置控件内容竖向的排列规则，Botton(底部)、Center(居中)、Stretch(伸展,默认的)、Top(顶部) |
| Margin              | 设置控件和父控件的边距，顺序是左、上、右、下                 |
| FontSize            | 设置控件字体大小                                             |
| Foreground          | 设置控件内容颜色                                             |
| Background          | 设置控件背景颜色                                             |

`TextBlock`标签是针对用于显示文字的，使用方法和`Label`，但是它多出了很多实用的功能

| 名称         | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| TextWrapping | 设置文本信息的显示规则，NoWrap(不包裹)、Wrap(包裹)、WrapWithOverflow(溢出) |

### 输入框

`TextBox`可以输入文字内容，使用属性和`TextBlock`类似

### 按钮

`Button`可以点击的控件，使用属性和`Label`类似

| 名称  | 描述                                   |
| ----- | -------------------------------------- |
| Click | 给控件设置点击之后需要完成的事件(函数) |

```cs
private void Button_Click(object sender, RoutedEventArgs e)
{

}
```

点击后更换输入框中的内容

| 名称 | 描述                                   |
| ---- | -------------------------------------- |
| Name | 给控件设置点击之后需要完成的事件(函数) |

前端

```xaml
<Window x:Class="HelloWPF.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:HelloWPF"
        mc:Ignorable="d"
        Title="MainWindow" 
        Height="450" Width="800">

    <Grid>
        <TextBox 
            x:Name="input"
            HorizontalAlignment="Center"
            Margin="0,160,0,0" 
            Text="TextBox" 
            TextWrapping="Wrap" VerticalAlignment="Top" Width="120"/>
        <Button
            Content="按钮"
            Width="100"
            Height="50"
            Click="Button_Click" />
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
        public MainWindow()
        {
            InitializeComponent();
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            input.Text = "xxxx";
        }
    }
}
```

获取输入框里的内容

```cs
private void Button_Click(object sender, RoutedEventArgs e)
{
    MessageBox.Show("你输入的是"+input.Text);
}
```

### 练习

让用户输入`账号`、`密码`判断账号是不是`cykjf`以及密码是不是`123456`,如果账号密码正确，就弹出对话框显示内容`成功`，否则弹出对话框内容`错误`

前端

```xaml
<Window x:Class="HelloWPF.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:HelloWPF"
        mc:Ignorable="d"
        Title="MainWindow" 
        Height="450" Width="800">

    <Grid>
        <TextBlock 
            HorizontalAlignment="Left" 
            Margin="305,162,0,0" 
            Text="账号" 
            TextWrapping="Wrap"
            VerticalAlignment="Top"/>
        <TextBox 
            x:Name="user"
            HorizontalAlignment="Center"
            Margin="0,160,0,0" 
            TextWrapping="Wrap" VerticalAlignment="Top" Width="120"/>
        <TextBlock 
            HorizontalAlignment="Left" 
            Margin="305,200,0,0" 
            Text="密码" 
            TextWrapping="Wrap"
            VerticalAlignment="Top"/>
        <TextBox 
            x:Name="password"
            HorizontalAlignment="Center"
            Margin="0,200,0,0" 
            TextWrapping="Wrap" VerticalAlignment="Top" Width="120"/>
        <Button
            Content="按钮"
            Width="100"
            Height="50"
            Click="Button_Click" 
            VerticalAlignment="Bottom" />
        
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
        public MainWindow()
        {
            InitializeComponent();
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            if (user.Text == "cykjf" && password.Text == "123456")
            {
                MessageBox.Show("成功");
            }
            else
            {
                MessageBox.Show("错误");
            }
        }
    }
}
```

