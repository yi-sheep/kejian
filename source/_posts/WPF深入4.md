---
title: WPF深入4
date: 2022-06-23 11:51:00
tags: [教材,阶段一]
categories: c++
---

# WPF深入

### 画正方体

### 画三角体

### 画六棱柱

### 画圆锥

```xaml
<Path Stroke="Pink" StrokeThickness="2">
    <Path.Data>
        <PathGeometry Figures="M95,100 L50,200 M95,100 A6,6,0,0,1,105,100 M150,200 L105,100 M50,200 A50,10,0,0,0,150,200 A50,10,0,0,0,50,200  Z"/>
    </Path.Data>
</Path>
```

![image-20220622203244998](https://s2.loli.net/2022/06/22/ZG5HdSRey1cv9li.png)

### 画圆柱

```xaml
<Path Stroke="Pink" StrokeThickness="2">
    <Path.Data>
        <PathGeometry Figures="M100,100 L100,200 A50,60,0,0,0,150,200 L150,100 A50,60,0,0,0,100,100 A50,60,0,0,0,150,100 M100,200 A50,60,0,0,1,150,200"/>
    </Path.Data>
</Path>
```

![image-20220623114110291](https://s2.loli.net/2022/06/23/5fK1uAR8aJkNdGv.png)

