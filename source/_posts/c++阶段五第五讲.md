---
title: c++阶段五第五讲
date: 2022-03-17 17:54:03
tags: [教材,阶段五]
categories: c++
---

# 第五讲

## html

`div`、`img`、`input`、`a`、`p`、`h`、`br`.

## css

标签样式:

类样式

id样式

伪样式

`:hover`

| 名称             | 作用                                   |
| ---------------- | -------------------------------------- |
| width            | 宽度                                   |
| height           | 高度                                   |
| margin           | 外边距，可以单独设置，比如`margin-top` |
| border           | 边框，比如`border: 0px solid #ccc;`    |
| border-radius    | 边框圆角                               |
| float            | 浮动位置                               |
| background-color | 背景颜色                               |
| color            | 字体颜色                               |
| font-size        | 字体大小                               |
| text-align       | 字体排列                               |
| line-height      | 竖直位置                               |

## JavaScript

变量

`var i = 0;`

`let j = 0;`

函数

```javascript
function funName() {
}
// 箭头函数
() => {
    
}
```

页面跳转

```javascript
window.location.href = "要跳转到的地址";
```

获取元素

```javascript
// 通过id获取
document.getElementById("in");
// 通过class获取
document.getElementsByClassName("");
```

提示框

```javascript
alert("提示语");
```

## 练习

[作品网址](http://gaoxianglong.gitee.io/web/百度一下.html)

```html
<!-- 百度一下 -->
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>百度一下</title>
</head>
<style>
    body {
        width: 720px;
        margin: 0 auto;
    }
    input{
        width: 80%;
        height: 30px;
        border: 0px solid #ccc;
        border-radius: 5px;
        float: left;
    }

    #input {
        width: 100%;
        border: 1px solid #ccc;
        border-radius: 5px;
        float: left;
    }

    #button {
        width: 14%;
        height: 30px;
        border-radius: 5px;
        border: 1px solid #ccc;
        background-color: rgb(71, 82, 236);
        color: rgb(248, 244, 244);
        font-size: 16px;
        float: right;
        text-align: center;
        line-height: 28px;
    }
    #button:hover{
        background-color: rgb(39, 48, 173);
        color: rgb(231, 216, 216);
    }

    #form {
        text-align: center;
        /* padding: 0 100px; */
    }
    #ss{
        width: 20px;
        /* float: right; */
        margin-top: 6px;
    }
</style>

<body>
    <div id="form">
        <img src="http://www.baidu.com/img/PCtm_d9c8750bed0b3c7d089fa7d55720d6cf.png" alt="">
        <div id="input">
            <input id="in" type="text" placeholder="请输入搜索内容">
            <img id="ss" src="https://gitee.com/gaoxianglong/picgo/raw/master/img/%E6%8B%8D%E7%85%A7.png" alt="">
            <div id="button" onclick="buttonClick();">
                百度一下
            </div>
            
        </div>
    </div>
</body>
<script>
    let input = document.getElementById("in");
    function buttonClick() {
        window.location.href = "http://www.baidu.com/s?wd=" + input.value;
    }
    let ss = document.getElementById("ss");
    ss.onclick = () => {
        alert("暂不支持搜索图片");
    }

</script>

</html>
```

<iframe src="http://gaoxianglong.gitee.io/web/百度一下.html" width="100%" height="100%">


