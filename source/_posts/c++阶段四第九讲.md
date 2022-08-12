---
title: c++阶段四第九讲
date: 2022-04-22 09:08:00
tags: [教材,阶段四]
categories: c++
---

# 第九讲

## MySQL

### 删除数据

`DELETE FROM 表名;`

`DELETE FROM 表名 WHERE 条件;`

![image-20220422095835845](https://s2.loli.net/2022/04/22/7wYOX8BED1Sc39k.png)

### 排序

在查询数据时，由于数据过多，我们可以使用`ORDER BY 字段名 规则`来指定以某一个字段做参考，进行升序或降序的显示方式。

`SELECT * FROM 表名ORDER BY 字段名 规则;`

![image-20220422100932319](https://s2.loli.net/2022/04/22/uL3DUg2mJa68pWb.png)

`ASC`升序

![image-20220422101048580](https://s2.loli.net/2022/04/22/wDdrOJZaeBgpt6H.png)

`DESC`降序

![image-20220422101158289](https://s2.loli.net/2022/04/22/4N3fclnAOhyoqTG.png)

### 正则表达式

查找数据表中`name`字段以'小'为开头的所有数据

`SELECT * FROM u WHERE name REGEXP '^小';`

![image-20220422101507062](https://s2.loli.net/2022/04/22/wuTq3sjJbl5dhNY.png)

查找数据表中`name`字段以'三'为结尾的所有数据

`SELECT * FROM u WHERE name REGEXP '三$';`

![image-20220422101702882](https://s2.loli.net/2022/04/22/Y2wFzOVAyxSTi6t.png)

查找数据表中`name`字段包含'小'的所有数据

`SELECT * FROM u WHERE name REGEXP '小';`

![image-20220422101823818](https://s2.loli.net/2022/04/22/TBP2xENMtG9Zhgj.png)

### 图形化操作

### 练习



