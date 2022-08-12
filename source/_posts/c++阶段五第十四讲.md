---
title: 阶段五第十四讲
date: 2022-06-08 11:03:07
tags: [教材,阶段五]
categories: c++
---

# 第十四讲

## 图片切换

- 显示图片窗口接收图片地址列表以及当前位置
- 点击按钮修改图片位置
- 加载图片

```cs
using Microsoft.Win32;
using System;
using System.Collections.Generic;
using System.IO;
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
        List<string> url;
        int p;
        public ShowImage(List<string> url,int p)
        {
            InitializeComponent();
            this.url = url;
            this.p = p;
            jz();
        }
        private void jz()
        {
            BitmapImage i = new BitmapImage(new Uri(url[p]));
            this.Width = i.Width;
            this.Height = i.Height;
            img.Source = i;
        }
        private void Buttont_Click(object sender, RoutedEventArgs e)
        {
            p--;
            if (p < 0)
            {
                p = 11;
            }
            jz();

        }
        private void Buttonb_Click(object sender, RoutedEventArgs e)
        {
            p++;
            if (p > 11)
            {
                p = 0;
            }
            jz();
        }
    }
}
```

传递当前图片位置

```cs
private void img_MouseDown(object sender, MouseButtonEventArgs e)
{
    /*BitmapImage i = new BitmapImage(new Uri(((Image)sender).Source.ToString()));
            MessageBox.Show(i.Width.ToString()+":"+i.Height.ToString());*/
    int p = 0;
    switch (((Image)sender).Name)
    {
        case "img1":
            p = 0;
            break;
        case "img2":
            p = 1;
            break;
        case "img3":
            p = 2;
            break;
        case "img4":
            p = 3;
            break;
        case "img5":
            p = 4;
            break;
        case "img6":
            p = 5;
            break;
        case "img7":
            p = 6;
            break;
        case "img8":
            p = 7;
            break;
        case "img9":
            p = 8;
            break;
        case "img10":
            p = 9;
            break;
        case "img11":
            p = 10;
            break;
        case "img12":
            p = 11;
            break;
    }
    ShowImage si = new ShowImage(list,p);
    si.Show();
}
```



## 文件下载

- 创建文件保存对话框
- 设置文件保存类型
- 是否记住上一次选择的路径
- 判断文件对话框是否显示
- 创建临时位图对象
- 将图片加载进位图对象
- 引入文件流，进行保存

```cs
SaveFileDialog sfd = new SaveFileDialog();
sfd.Filter = "Image Files (*.bmp, *.png, *.jpg)|*.bmp;*.png;*.jpg | All Files | *.*"; // 保存文件类型
sfd.RestoreDirectory = true;//保存对话框是否记忆上次打开的目录 
if (sfd.ShowDialog() == true)
{
    var encoder = new PngBitmapEncoder();
    encoder.Frames.Add(BitmapFrame.Create((BitmapSource)this.img.Source));
    using (FileStream stream = new FileStream(sfd.FileName, FileMode.Create)) encoder.Save(stream);
}
```

