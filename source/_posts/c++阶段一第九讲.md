---
title: c++阶段一第九讲
date: 2021-11-11 14:48:15
tags: [教材,阶段一] 
categories: c++
---

# 第九讲

输出1-100？

## while循环

公式：

```c++
while(布尔表达式){
    
}
```

作用：

先判断小括号内的条件是否成立，如果成立则执行大括号内的代码，然后再回到小括号做判断，如此循环，直到小括号内的条件不成立才停止循环。

输出1-10？

```c++
int i = 0;
while(i<10){
    cout<<i;
    i++;
}
```

**有限循环的三要素：**

+ 控制循环次数的变量
+ 控制循环次数的条件
+ 改变变量的值

输出100-1？

```c++
int i = 100;
while(i>0){
    cout<<i;
    i--;
}
```

## do-while循环

公式：

```c++
do{
    
}while(布尔表达式);
```

作用：

不管条件是否成立，先执行一次do后面的大括号里的所有代码，然后判断条件是否成立，成立则再次执行do后面的大括号里的所有代码，如此循环，直到条件不成立。

例子：

```c++
int i = 0;
while(i<0){
    cout<<i;
    i++;
}
cout<<endl;
int j = 0;
do{
  cout<<j;
  j++;  
}while(j<0);
```

使用循环计算1累加到10的和？

```c++
int i = 1;
int sum = 0;
while(i<=10){
    sum = sum+i;
    i++;
}
cout<<sum;
```

