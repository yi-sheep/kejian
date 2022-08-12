---
title: c++阶段四第六讲
date: 2022-03-25 08:54:59
tags: [教材,阶段四]
categories: c++
---

# 第六讲

**网页组成**

`html`、`css`、`JavaScript`

## CSS

在网页中`html`是编写网页的结构或者框架，而`css`就是在这个结构上进行美化。

在标签中写上`style`就可以修改当前这个标签是长什么样的

比如现在要控制`div`的背景颜色为`red`

```html
<div style="background-color: red;">111</div>
```

再设置宽度为`100px`

```html
<div style="background-color: red;width: 100px;">111</div>
```

再设置高度为`100px`

```html
<div style="background-color: red;width: 100px;height: 100px;">111</div>
```

但是如果一个标签的样式比较复杂，那么这样写就会有特别多的代码已经及其不好看，如果有两个标签的样式差不多相同，除了`ctrl+c/v`别无它法。

所以css也在进化。

## 选择器

在`body`标签的上边加上`style`的双标签，在这个标签中就可以编写`css`的代码。

```html
<style>
    
</style>
```

### 标签选择器

如果我们想让这个网页上所有的`div`都使用一个样式，就可以使用标签选择器

公式：

```css
div {
    
}
```

案例

```html
<style>
    div {
        width: 100px;
        height: 100px;
        background-color: rgb(0, 173, 253);
        /* 字体颜色 */
        color:#fff;
    }
</style>

<body>
    <div>111</div>
</body>
```

### 类选择器

有的时候并不想控制页面上所有的标签，只需要控制一个或多个，这种情况就可以给要控制的标签加上一个`类`

`<div class="test">111</div>`

在`style`标签中就可以针对这个类编写样式

```css
.test {
    
}
```

案例

```html
<style>
    div {
        width: 100px;
        height: 100px;
        background-color: rgb(0, 173, 253);
        /* 字体颜色 */
        color:#fff;
    }
    .test {
        width: 100px;
        height: 100px;
        background-color: rgb(60, 255, 0);
        color: #fff;
        /* 标签圆角 */
        border-radius: 10px;
        /* 内容左右居中 */
        text-align: center;
        /* 内容上下居中 */
        line-height: 100px;
    }
</style>

<body>
    <div class="test">111</div>
    <br/>
    <div class="test">222</div>
    <br/>
    <div>333</div>
</body>
```

### ID选择器

在网页中我们可以给每一个标签设置一个**唯一标识符`ID`**通过这个`ID`只能找到这个标签

`<div id="div1">111</div>`

在`style`标签中就可以针对这个`ID`编写样式

```css
#div1 {
        
}
```

案例

```html
<style>
    div {
        width: 100px;
        height: 100px;
        color: #fff;
    }
    #div1 {
        background-color: rgb(0, 174, 255);
        /* 字体大小 */
        font-size: 24px;
        /* 外边距 */
        margin: 10px;
    }
    #div2{
        background-color: rgb(0, 255, 0);
        /* 内边距 */
        padding: 10px;
    }
</style>

<body>
    <div id="div1">111</div>
    <br/>
    <div id="div2">222</div>
</body>
```

### 伪类选择器

伪类选择器比较特殊它无法单独存在，要依托于以上任意一个选择器上

```css
/* 鼠标移动到元素上触发这个样式 */
div:hover {
    
}
```

案例

```html
<style>
    div {
        width: 100px;
        height: 100px;
        color: #fff;
        background-color: rgb(187, 255, 0);
    }
    div:hover {
        width: 100px;
        height: 100px;
        color: #fff;
        background-color: rgb(116, 158, 0);
    }
</style>

<body>
    <div id="div1">111</div>
    <br/>
    <div id="div2">222</div>
</body>
```

## 扩展

设置`a`标签的下划线样式为空

```css
a {
  text-decoration: none;
}
```

```css
img {
   /* 设置占屏幕多少百分比 */
   width: 70%;
   /* 设置当前yuanyuan是浮动到右边 */
   float:right;
}
```

## 练习

[案例网站](http://gaoxianglong.gitee.io/web/新闻2.html)

```html
<!DOCTYPE html>
<html lang="zh-cn">

<head>
    <meta charset="utf-8">
    <title>新闻demo</title>
</head>
<style>
    body {
        width: 720px;
        margin: 0 auto;
    }

    .text-c {
        text-align: center;
    }

    .text-s {
        font-size: 14px;
        color: rgb(73, 73, 73);
    }

    a {
        text-decoration: none;
    }

    a:link {
        color: rgb(0, 162, 255);
    }

    a:hover {
        color: rgb(255, 0, 0);
    }
    img {
        /* 设置占屏幕多少百分比 */
        width: 70%;
        /* 设置当前yuanyuan是浮动到右边 */
        float:right;
    }
    #x{
        width: 30%;
        font-size: 14px;
    }
</style>

<body>
    <div class="text-c">
        <h2>光波导：主流AR眼镜的核心显示技术</h2>
    </div>
    <div class="text-c text-s">
        <p>
            2021-3-10 08:43
        </p>
    </div>
    <div>
        <p>
            <strong>
                <a href="https://baike.baidu.com/item/光波导">
                    光波导
                </a>
                ，因其轻薄和外界光线的高穿透特性而被认为是消费级
                <a href="https://baike.baidu.com/item/AR眼镜">AR眼镜</a>
                的必选光学方案，又因其价格高和技术门槛高让人望而却步。
            </strong>
        </p>
        <p>
            <strong>
                随着主流AR设备微软HoloLens2、Magic Leap
                One等对光波导技术的采用和设备量产，以及AR光学模组厂商DigiLens、耐德佳、灵犀微光等近期融资消息的频繁披露，导致光波导的讨论热度也持续增加了不少。
            </strong>
        </p>
        <img src="https://gitee.com/gaoxianglong/picgo/raw/master/img/816.jpg">
        <div id="x">
            <p>
                <strong>
                    那么，光波导的工作原理是怎样的？
                </strong>
            </p>
            <p>
                <strong>
                    市面上林林总总的阵列光波导、几何光波导、衍射光波导、全息光波导、多层光波导又有什么不同？
                </strong>
            </p>
            <p>
                <strong>
                    它又是如何一步步改变AR眼镜市场格局的？
                </strong>
            </p>
            <p>
                <strong>
                    我们更看好哪一种光波导技术，为什么？
                </strong>
            </p>
        </div>

    </div>
</body>

</html>
```

