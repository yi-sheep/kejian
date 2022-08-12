---
title: c++阶段四第八讲
date: 2022-04-15 10:14:40
tags: [教材,阶段四]
categories: c++
---

# 第八讲

## Mysql

### 安装

[phpstudy](https://www.xp.cn/download.html)

### 连接Mysql

`mysql -u用户名 -p密码`

![img](https://s2.loli.net/2022/04/15/w4CVXarS18NtmcH.jpg)

### 断开连接

`exit`

### 创建数据库

`CREATE DATABASE 数据库名;`

![img](https://s2.loli.net/2022/04/15/FXfI8HulGYxqcoW.gif)

### 删除数据库

`drop database 数据库名;`

![img](https://s2.loli.net/2022/04/15/9FM6Osj2JDKHx4c.gif)

### 连接数据库

`use 数据库名;`

![img](https://s2.loli.net/2022/04/15/MbI3yNWEqsdelO6.jpg)

Mysql中常见的数据类型：

数值类型：

![img](https://s2.loli.net/2022/04/15/NHKpWG2LBzDsoRC.jpg)

日期和时间类型：

![img](https://s2.loli.net/2022/04/15/Fmg2ruZfMXDxbNp.jpg)

字符串类型：

![img](https://s2.loli.net/2022/04/15/beT3xPlBARLKnou.jpg)

### 创建数据表

`CREATE TABLE 表名 (字段名 字段类型,...);`

![img](https://s2.loli.net/2022/04/15/qk2OVneX5wAuvgK.jpg)

> MySQL命令终止符为分号 `; `。

### 删除数据表

`DROP TABLE 表名;`

![img](https://s2.loli.net/2022/04/15/YNRciBytO3WUDFp.jpg)

### 插入数据

`INSERT INTO 表名 (字段1名, 字段2名,...字段n名)VALUES (值1, 值2,...值n);`

![img](https://s2.loli.net/2022/04/15/uQtDInmcdApi31Y.jpg)

### 查询数据

`SELECT * FROM 表名;`

![img](https://s2.loli.net/2022/04/15/Yfy5b1ZxgVKtLCh.jpg)

### 更新数据

`UPDATE 表名 SET 字段名=值;`

![img](https://s2.loli.net/2022/04/15/VItUTelo4JAGRqK.jpg)

## 练习：

创建一个数据库名为`user`,这个数据库中有两张表分别为`info`和`guanxi`,**info**表中有姓名，年龄，身高，体重。**guanxi**表中有姓名，职业，家庭成员。

插入数据，并且显示出来

```mysql
create database user;
use user
create table info(name varchar(20),age int,height int,weight int);
create table guanxi(name varchar(20),occupation varchar(30),family text);
insert into info(name,age,height,weight) values ("张三",10,150,100);
insert into info(name,age,height,weight) values ("小红",11,151,90);
insert into info(name,age,height,weight)values("李华",12,155,101);
SELECT * FROM info;
insert into guanxi(name,occupation,family) values ("张三","学生","王二，李四"),("小红","学生","小明，小强"),("李 华","学生","杰克，瑞希");
SELECT * FROM guanxi;
```

