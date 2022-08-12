---
title: c++阶段四第七讲
date: 2022-03-31 18:21:27
tags: [教材,阶段四]
categories: c++
---

# 第七讲

**网页组成**

`html`、`css`、`JavaScript`

## JavaScript

在网页中`html`是编写网页的结构或者框架，`css`就是在这个结构上进行美化，而`JavaScript`是处理页面数据的。

在标签中写上`script`就可以设置页面的数据了。

在这之前还需要来学习一下`JavaScript`的语法

### 变量

`var a = 0;`

```html
<script>
    var a = 1;
	console.log(a);
</script>
```

> 没有创建变量就会有错误信息

```html
<script>
	console.log(a);
	var a = 1;
</script>
```

> 变量被提升了

`let a = 1;`这种方式是非常推荐的为了避免不必要的错误。

### 循环

```html
<script>
	for (let i = 0; i < 10; i++) {
		console.log(i);
	}
    while (1) {
		
	}
</script>
```

### 函数

```html
<script>
	function name(params) {
		console.log(1);
	};
    // 箭头函数
	let fun = ()=>{

	}
</script>
```

### 对象

在`JavaScript`中对象是很常见的，对象只需要包裹在`{}`中就行具备一定的格式

```javascript
let data = {
    a:1,
    b:"y"
}
// 访问对象中的值
data.a;
```

### 获取元素

通过`class`获取

```html
<body>
	<div class="d"></div>
	<div class="d"></div>
	<div class="d"></div>
</body>
<script>
	let div = document.getElementsByClassName("d");
	console.log(div);
</script>
```

通过`id`获取

```html
<body>
	<div id="d">111</div>
	<div id="d">222</div>
</body>
<script>
	let div = document.getElementById("d");
	console.log(div);
</script>
```

### 获取双标签元素中的内容

```html
<body>
	<div id="d">
		<h1>111</h1>
	</div>
</body>
<script>
	let div = document.getElementById("d");
	// 内容以文字显示出来,会有一定的标签特点
	console.log(div.textContent);
	// 内容以文字显示出来
	console.log(div.innerText);
	// 内容以标签显示出来
	console.log(div.innerHTML);
</script>
```

### 获取输入框的内容

```html
<body>
	<input id="in" type="text">
</body>
<script>
	let input = document.getElementById("in");
	console.log(input.value);
</script>
```

### 表格

表格由 `<table> `标签来定义。每个表格均有若干行（由 `<tr> `标签定义），每行被分割为若干单元格（由` <td> `标签定义）。字母 td 指表格数据（table data），即数据单元格的内容。表格的表头使用 `<th> `标签进行定义。

```html
<table border="1">
    <tr>
        <th>标题 1</th>
        <th>标题 2</th>
    </tr>
    <tr>
        <td>行 1, 列 1</td>
        <td>行 1, 列 2</td>
    </tr>
    <tr>
        <td>行 2, 列 1</td>
        <td>行 2, 列 2</td>
    </tr>
</table>
```

### 列表

HTML 支持有序、无序和定义列表

#### 无序列表：

序列表使用 `<ul>` 标签

```html
<ul>
<li>张三</li>
<li>李四</li>
</ul>
```

#### 有序列表：

每个列表项始于` <li> `标签。列表项使用数字来标记。

```html
<ol>
<li>张三</li>
<li>李四</li>
</ol>
```

JavaScript添加表格数据:

```html
<!DOCTYPE html>
<html lang="zh-cn">
<head>
	<meta charset="utf-8">
	<title>表格</title>
</head>
<style>
	table{
		text-align: center;
	}
	th{
		width: 50px;
	}
</style>

<body>
	<table id="table" border="1">
		<tr>
			<th>id</th>
			<th>姓名</th>
			<th>年龄</th>
		</tr>
		<tr>
			<td>行 1, 列 1</td>
			<td>行 1, 列 2</td>
		</tr>
		<tr>
			<td>行 2, 列 1</td>
			<td>行 2, 列 2</td>
		</tr>
	</table>
</body>
<script>
	let data = [
		{
			id: "01",
			name: "张三",
			age: 18
		},
		{
			id: "02",
			name: "李四",
			age: 18
		},
		{
			id: "03",
			name: "小明",
			age: 18
		}
	];
	let table = document.getElementById("table");
	let html = `
	<tr>
		<th>id</th>
		<th>姓名</th>
		<th>年龄</th>
	</tr>
	`;

	data.forEach((d) => {
		html += `
		<tr>
			<td>${d.id}</td>
			<td>${d.name}</td>
			<td>${d.age}</td>
		</tr>`;
	});
	table.innerHTML = html;
</script>

</html>
```

### 