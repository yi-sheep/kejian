---
title: c++阶段四第五讲
date: 2022-03-17 09:19:28
tags: [教材,阶段四]
categories: c++
---

# 第五讲

**网页组成**

`html`、`css`、`JavaScript`

## HTML

HTML（英语：超文本标记语言，简称：HTML）也叫作超文本标记语言，是一种使用结构化Web网页及其内容的标记语言，您可以使用HTML来建立自己的WEB站点。

html代码其实就是一个个标签组成的，标签分为两类

**单标签：**

创建公式:`<标签名/>`

**双标签：**

创建公式：`<标签名>内容</标签名>`

## 标签

### 标题

`h`:表示标题的意思,它是一个双标签。有几个等级分布为h1一级标签、h2二级标签、h3三级标签、h4四级标题、h5五级标题、h6六级标题。

```html
<h1>这是一级标题</h1>
<h2>这是二级标题</h2>
<h3>这是三级标题</h3>
<h4>这是四级标题</h4>
<h5>这是五级标题</h5>
<h6>这是六级标题</h6>
```

> 写完后将后缀名改为.html，使用浏览器打开

### 段落

`p`:段落标签，它是一个双标签。会更具标签内的文字进行自动换行

```html
<p>
    这是一个段落。
    这是第二段。
    这是第三段。
</p>

```

### 换行

`br`:换行，它是一个单标签。

```html
<p>
    这是一个段落。
    <br/>
    这是第二段。
    <br/>
    这是第三段。
</p>
```

### 文字特效

![clip_image001](https://gitee.com/gaoxianglong/picgo/raw/master/img/clip_image001.png)

### 超链接

`a`:超链接标签。

`<a href="地址">描述</a>`

### html的标准格式

```html
<!DOCTYPE html>						<!-- 网页类型声明 -->
<html lang="zh-cn">				<!-- 表示HTML网页开始 -->
<head>						<!-- 包含网页源数据开始 -->
	<meta charset="uth-8">		<!-- 声明字符编码 -->
	<title>基本结构</title>		<!-- 设置网页标题 -->
</head>						<!-- 包含网页源数据结束 -->
<body>						<!-- 表示HTML网页内容 -->

</body>						<!-- 表示HTML网页内容结束 -->
</html>						<!-- 表示HTML网页结束 -->
```

### 图片

`img`:图片标签

`<img src="图片地址" alt="描述">`

### 盒子

`div`标签：盒子标签块级元素，用来整理网页格式

```html
<!DOCTYPE html>
<html lang="zh-cn">
<head>
	<meta charset="uth-8">
	<title>基本结构</title>
</head>
<body>
	<div>
		导航栏
	</div>
	<div>
		轮播栏
	</div>
	<div>
		内容区
	</div>
</body>
</html>
```

### 样式

在标签中写入`style`就可以给这个标签设置样式了

```html
<div style=""></div>
```

常见的样式：

`font-size: 14px` 设置字体大小为14，px是像素的意思

`width: 100px;`设置元素的宽度

`height: 1000px;` 设置元素的高度

`margin:0 0;` 设置元素的外边距第一个值为上下，第二个值为左右，如果写的是auto就表示自适应

如果要让页面内容居中就可以在body标签上设置样式

`width:720px;margin:0 auto;`

## 练习

完成以下网页

![](https://gitee.com/gaoxianglong/picgo/raw/master/img/20220317162302.png)

![img](https://gitee.com/gaoxianglong/picgo/raw/master/img/816.jpg)

图片地址：`https://gitee.com/gaoxianglong/picgo/raw/master/img/816.jpg`

文案地址：

`https://baike.baidu.com/item/光波导`

`https://baike.baidu.com/item/AR眼镜`

```html
<!DOCTYPE html>
<html lang="zh-cn">
<head>
	<meta charset="uth-8">
	<title>新闻demo</title>
</head>
<body style="width: 720px;margin:0 auto;">
	<div>
      <h2>光波导：主流AR眼镜的核心显示技术</h2>
	</div>
	<div style="font-size: 14px">
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
				随着主流AR设备微软HoloLens2、Magic Leap One等对光波导技术的采用和设备量产，以及AR光学模组厂商DigiLens、耐德佳、灵犀微光等近期融资消息的频繁披露，导致光波导的讨论热度也持续增加了不少。
			</strong>
		</p>
		<img src="https://imagepphcloud.thepaper.cn/pph/image/119/276/816.jpg" style="width: 720px;">
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
</body>
</html>
```

