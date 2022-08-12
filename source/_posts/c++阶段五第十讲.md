---
title: c++阶段五第十讲
date: 2022-05-13 11:44:45
tags: [教材,阶段五]
categories: c++
---

# 第十讲

更换界面

登录之后之间进入数据相关的页面

![image-20220513114944488](https://s2.loli.net/2022/05/13/Mor9JeS6OhH3ZVv.png)

添加成功后数据显示在右边

```cs
string s = "";
for (int i = 0; i < sList.Count; i++)
{
    s += sList[i].toString();
}
info.Text = "姓名\t\t性别\t\t身份证\t\t地址\n" + s;
```

点击按钮切换状态

```cs
int zt = 0;
private void Button_Click_2(object sender, RoutedEventArgs e)
{
    // 添加
    zhuangtai.Text = "添加";
    zt = 0;
}

private void Button_Click_3(object sender, RoutedEventArgs e)
{
    // 修改
    zhuangtai.Text = "修改\n根据身份证号做修改";
    zt = 1;
}

private void Button_Click_4(object sender, RoutedEventArgs e)
{
    // 删除
    zhuangtai.Text = "删除\n根据身份证号做修改";
    zt = 2;
}
```

修改

```cs
// 添加
if (zt == 0)
{
    SFZ sfz = new SFZ(sName.Text, sSex.Text, sId.Text, sAddress.Text);
    sList.Add(sfz);
}
else if (zt == 1)
{
    // 修改
    for (int i = 0; i < sList.Count; i++)
    {
        if (sList[i].id == sId.Text)
        {
            sList[i].name = sName.Text;
            sList[i].sex = sSex.Text;
            sList[i].address = sAddress.Text;
        }
    }
}
```

删除

```cs
else if (zt == 2)
{
    // 删除
    for (int i = 0; i < sList.Count; i++)
    {
        if (sList[i].id == sId.Text)
        {
            sList.RemoveAt(i);
        }
    }
}
```

前端

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
        <StackPanel HorizontalAlignment="Left" VerticalAlignment="Top" Margin="64,196,0,0">
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
                <Button Content="确定" HorizontalAlignment="Left" VerticalAlignment="Bottom" Margin="36,0,0,0" Click="Button_Click" />
            </Grid>
        </StackPanel>
        <TextBlock 
            x:Name="info"
            HorizontalAlignment="Left"
            Margin="320,0,0,0" 
            Text="TextBlock"
            VerticalAlignment="Center" Height="390" Width="480"/>
        <TextBlock x:Name="zhuangtai" HorizontalAlignment="Left" Margin="126,155,0,0" Text="添加" TextWrapping="Wrap" VerticalAlignment="Top"/>
        <Button Content="添加" HorizontalAlignment="Left" Margin="64,85,0,0" VerticalAlignment="Top" Click="Button_Click_2" RenderTransformOrigin="0.929,0.78"/>
        <Button Content="修改" HorizontalAlignment="Left" Margin="140,85,0,0" VerticalAlignment="Top" Click="Button_Click_3"/>
        <Button Content="删除" HorizontalAlignment="Left" Margin="207,85,0,0" VerticalAlignment="Top" Click="Button_Click_4"/>
    </Grid>
</Page>
```

后端

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
        int zt = 0;
        public tianjia(List<SFZ> sList)
        {
            InitializeComponent();
            this.sList = sList;
            info.Text = "姓名\t\t性别\t\t身份证\t\t地址\n";
        }
        private void Button_Click(object sender, RoutedEventArgs e)
        {
            // 添加
            if (zt == 0)
            {
                SFZ sfz = new SFZ(sName.Text, sSex.Text, sId.Text, sAddress.Text);
                sList.Add(sfz);
            }
            else if (zt == 1)
            {
                // 修改
                for (int i = 0; i < sList.Count; i++)
                {
                    if (sList[i].id == sId.Text)
                    {
                        sList[i].name = sName.Text;
                        sList[i].sex = sSex.Text;
                        sList[i].address = sAddress.Text;
                    }
                }
            }
            else if (zt == 2)
            {
                // 删除
                for (int i = 0; i < sList.Count; i++)
                {
                    if (sList[i].id == sId.Text)
                    {
                        sList.RemoveAt(i);
                    }
                }
            }
            string s = "";
            for (int i = 0; i < sList.Count; i++)
            {
                s += sList[i].toString();
            }
            info.Text = "姓名\t\t性别\t\t身份证\t\t地址\n" + s;
        }

        private void Button_Click_2(object sender, RoutedEventArgs e)
        {
            // 添加
            zhuangtai.Text = "添加";
            zt = 0;
        }

        private void Button_Click_3(object sender, RoutedEventArgs e)
        {
            // 修改
            zhuangtai.Text = "修改\n根据身份证号做修改";
            zt = 1;
        }

        private void Button_Click_4(object sender, RoutedEventArgs e)
        {
            // 删除
            zhuangtai.Text = "删除\n根据身份证号做修改";
            zt = 2;
        }
    }
}
```

