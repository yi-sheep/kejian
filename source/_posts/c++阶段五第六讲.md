---
title: c++阶段五第六讲
date: 2022-03-25 11:23:08
tags: [教材,阶段五]
categories: c++
---

# 第六讲

上节课的程序

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
        border-radius: 0 5px 5px 0;
        border: 1px solid rgb(71, 82, 236);
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

完成效果

[百度一下 ](http://gaoxianglong.gitee.io/web/百度一下2.html)

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
        border-radius: 0 5px 5px 0;
        border: 1px solid rgb(71, 82, 236);
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
    #nav{
        padding: 100px 140px;
    }
    .l{
        float: left;
    }
    .r{
        float:right;
    }
    a{
        width: 100px;
        color: rgb(0, 195, 255);
        text-decoration: none;  
        text-align: left;
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
    <div id="nav">
        <a href="http://www.lscykjf.top/index.server#ziyuan" class="l">创意科技坊</a>
        <a href="http://www.baidu.com/s?wd=c++" class="r">c++</a>
        <br>
        <br>
        <a href="http://www.baidu.com/s?wd=html" class="l">html</a>
        <a href="http://www.baidu.com/s?wd=css" class="r">css</a>
        <br>
        <br>
        <a href="http://www.baidu.com/s?wd=JavaScript" class="l">JavaScript</a>
        <a href="http://www.baidu.com/s?wd=c#" class="r">c#</a>
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

