---
title: c++阶段四第十二讲
date: 2022-05-26 09:45:12
tags: [教材,阶段四]
categories: c++
---

# 第十二讲

## 控件移动

每一个控件都会有一个`Margin`属性，通过这个属性就可以设置控件距离上下左右的距离是多少

大小与外边距的冲突

如果设置了大小那么外边距就需要让出对于的空间

如果不设置大小那么控件的大小就是根据外边距而自动设置的

```cs
but.Margin = new Thickness(l, --t, r, ++b);
```

## 键盘检测

通过给window设置`KeyDown="触发函数"`监听按键的按键

```cs
if (e.KeyStates == Keyboard.GetKeyStates(Key.W))
{
    but.Margin = new Thickness(l, --t, r, ++b);
}
else if (e.KeyStates == Keyboard.GetKeyStates(Key.S))
{
    but.Margin = new Thickness(l, ++t, r, --b);
}
else if (e.KeyStates == Keyboard.GetKeyStates(Key.A))
{
    but.Margin = new Thickness(--l, t, ++r, b);
}
else if (e.KeyStates == Keyboard.GetKeyStates(Key.D))
{
    but.Margin = new Thickness(++l, t,--r, b);
}
```

