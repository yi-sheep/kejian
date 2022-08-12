---
title: c++阶段五第九讲
date: 2022-05-05 09:32:33
tags:  [教材,阶段五]
categories: c++
---

# 第九讲

相互传递数据

```c++
class A{
    int number;
    A(int a){
       number = a; 
    }
}
```

```c++
class B{
    int number;
    B(int a){
       number = a;
    }
}
```

```c++
int n = 2;
B(n);
```

遍历列表

```c#
List<SFZ> sList = new List<SFZ>();
foreach(var item in sList)
{
    // item就是每一个对象
}
```

添加界面

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
            MessageBox.Show(sList[0].toString());
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

显示界面

```xaml
<Page x:Class="WpfApp2.showSFZ"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" 
      xmlns:d="http://schemas.microsoft.com/expression/blend/2008" 
      xmlns:local="clr-namespace:WpfApp2"
      mc:Ignorable="d" 
      d:DesignHeight="450" d:DesignWidth="800"
      Title="showSFZ">

    <Grid>
        <TextBlock x:Name="data" HorizontalAlignment="Stretch" VerticalAlignment="Stretch" />
        <Button Content="返回" Width="50" Height="23" HorizontalAlignment="Left" VerticalAlignment="Bottom" Margin="10,0,0,10" Click="Button_Click"/>
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
    /// showSFZ.xaml 的交互逻辑
    /// </summary>
    public partial class showSFZ : Page
    {
        List<SFZ> sList = new List<SFZ>();
        public showSFZ(List<SFZ> sList)
        {
            InitializeComponent();
            this.sList = sList;
            string d = "\t\t姓名\t\t性别\t\t身份证号\t\t\t户口地\n";
            foreach(var item in sList)
            {
                d += item.toString() + "\n";
            }
            data.Text = d;
        }
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            // 返回
            MainWindow window = (MainWindow)Window.GetWindow(this);
            window.Content = new guanliyuan(sList);
            window.Show();
        }
    }
}
```

数据类

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

