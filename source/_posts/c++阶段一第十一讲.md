---
title: c阶段一第十一讲
date: 2021-11-24 10:01:32
tags: [教材,阶段一]
categories: c++
---

# 第十一讲

## 嵌套

while循环的嵌套

例子：

```c++
while(true){
    while(true){
        
    }
}
```

for循环的嵌套

例子：

```c++
for(int i = 0;i<5;i++){
    for(int j = 0;j<5;j++){
        
    }
}
```

练习：

使用循环的嵌套打印一个5*5的正方形

```c++
for(int i = 0;i<5;i++){
    for(int j = 0;j<5;j++){
        cout<<"*";
    }
    cout<<endl;
}
```

使用循环的嵌套打印一个5*5的直角三角形

```c++
for(int i = 0;i<5;i++){
    for(int j = 0;j<i;j++){
        cout<<"*";
    }
    cout<<endl;
}
```

让用户来决定输出多少几*几的三角形

```c++
 #include <iostream>
using namespace std;
int main() {
	int a, b;
	cout << "请输入矩形的长：";
	cin >> a;
	cout << "\n请输入矩形的宽：";
	cin >> b;
	for (int i = 0; i < a; i++)
	{
		for (int j = 0; j < b; j++)
		{
			cout << "* ";
		}
		cout << "\n";
	}
}
```

选择一个循环语句，输出乘法表

```c++
for(int i = 1;i<10;i++){
    for(int j = 1;j<=i;j++){
        cout<<i<<"x"<<j<<"="<<i*j<<" ";
    }
    cout<<endl;
}
```



