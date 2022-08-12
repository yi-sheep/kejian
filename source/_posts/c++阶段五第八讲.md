---
title: c++阶段五第八讲
date: 2022-04-15 13:39:53
tags: [教材,阶段五]
categories: c++
---

# 第八讲

在page页面中获取当前窗口

`MainWindow window = (MainWindow)Window.GetWindow(this);`

### 命名空间

一个**WPF**项目就是存在于一个命名空间里，在这个命名空间里所有内容都能相互访问到，就算不是同一个文件，也能够访问到这个命名空间下的内容。

### 类

`权限修饰词 class 类名{}`

例子：

```c#
public class SFZ
{
    // 创建属性并同步生成get和set函数
    private string name { get; set; }
    private string sex { get; set; }
    private string id { get; set; }
    private string address { get; set; }
    // 构造函数
    public SFZ(string n, string s, string i, string a)
    {
        name = n;
        sex = s;
        id = i;
        address = a;
    }
    // 将属性按照一定格式转换为字符串
    public string toString()
    {
        return "\t\t" + name + "\t\t" + sex + "\t\t" + id + "\t\t" + address;
    }
}
```

### 列表

`List<类型> 名字 = new List<类型>();`

```c#
List<int> i = new List<int>();
i.add = 1;
i.add = 2;
i.add = 3;
foreach(var item in i){
    // 每一次循环item就是i中的值
}
```

本节课代码

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace WpfApp2
{
    public class SFZ
    {
        private string name { get; set; }
        private string sex { get; set; }
        private string id { get; set; }
        private string address { get; set; }
        public SFZ(string n, string s, string i, string a)
        {
            name = n;
            sex = s;
            id = i;
            address = a;
        }
        public string toString()
        {
            return "\t\t" + name + "\t\t" + sex + "\t\t" + id + "\t\t" + address;
        }
    }
}
```

```xaml
<Page x:Class="WpfApp2.tianjia"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" 
      xmlns:d="http://schemas.microsoft.com/expression/blend/2008" 
      xmlns:local="clr-namespace:WpfApp2"
      mc:Ignorable="d" 
      d:DesignHeight="450" d:DesignWidth="800"
      Title="tianjia">

    <Grid>
        <StackPanel HorizontalAlignment="Center" VerticalAlignment="Center">
            <StackPanel Orientation="Horizontal" Margin="0,10,0,10">
                <TextBlock Text="姓名" Width="60" />
                <TextBox x:Name="sName" Text="" TextWrapping="Wrap" Width="120"/>
            </StackPanel>
            <StackPanel Orientation="Horizontal" Margin="0,10,0,10">
                <TextBlock Text="性别" Width="60" />
                <TextBox x:Name="sSex" Text="" TextWrapping="Wrap" Width="120"/>
            </StackPanel>
            <StackPanel Orientation="Horizontal" Margin="0,10,0,10">
                <TextBlock Text="身份证号" Width="60" />
                <TextBox x:Name="sId" Text="" TextWrapping="Wrap" Width="120"/>
            </StackPanel>
            <StackPanel Orientation="Horizontal" Margin="0,10,0,10">
                <TextBlock Text="户口所在地" Width="61" />
                <TextBox x:Name="sAddress" Text="" TextWrapping="Wrap" Width="120"/>
            </StackPanel>
            <Grid HorizontalAlignment="Stretch">
                <Button Content="添加" HorizontalAlignment="Left" VerticalAlignment="Bottom" Margin="36,0,0,0" Click="Button_Click" />
                <Button Content="返回" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="116,0,0,0" Click="Button_Click_1" />
            </Grid>
        </StackPanel>
    </Grid>
</Page>

```

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
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace WpfApp2
{
    /// <summary>
    /// tianjia.xaml 的交互逻辑
    /// </summary>
    public partial class tianjia : Page
    {
        List<SFZ> sList = new List<SFZ>();
        public tianjia(List<SFZ> sList)
        {
            InitializeComponent();
            this.sList = sList;
        }
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            // 添加
            SFZ sfz = new SFZ(sName.Text, sSex.Text, sId.Text, sAddress.Text);
            sList.Add(sfz);
            MessageBox.Show("添加成功");
        }
        private void Button_Click_1(object sender, RoutedEventArgs e)
        {
            // 返回
            MainWindow window = (MainWindow)Window.GetWindow(this);
            window.Content = new guanliyuan(sList);
            window.Show();
        }
    }
}
```

