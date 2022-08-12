---
title: c++阶段四第二讲
date: 2022-02-23 09:45:21
tags: [教材,阶段四]
categories: c++
---

# 第二讲

## 文件流  

`ofstream ofile;`声明一个输出流

`ifstream ifile;`声明一个输入流

`fstream iofile;`声明一个输入\输出流

**常用函数：**

| 函数      | 作用                                                         |
| --------- | ------------------------------------------------------------ |
| fail()    | 判断一个流是否坏掉了                                         |
| open()    | 打开一个文件                                                 |
| close()   | 关闭文件流                                                   |
| eof()     | 函数来判断文件是否为空或者是否读到文件结尾了(是不是最后一行) |
| tellg()   | 获取当前流的位置，失败返回（-1）                             |
| getline() | 获取文件中的一行数据，并且保存到字符数组中                   |

**文件写入:**

```c++
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
	fstream file("test.txt", ios::out);
	if (!file.fail()) // fail()用来判断一个流是否“坏”掉了
	{
		cout << "开始写入" << endl;
		file << "name" << "\n";
		file << "sex" << "\n";
		file << "age" << "\n";
		cout << "写入完成" << endl;
	}
	else {
		cout << "can not open" << endl;
	}
	file.close();
	return 0;
}
```

**文件读取：**

```c++
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
	fstream file("test.txt", ios::in);
	if (!file.fail())
	{
		while (!file.eof())
		{
			char buf[128];
			file.getline(buf, 128);
			if (file.tellg() > 0) // 判断当前流的指针是不是还停留在最前面
			{
				cout << buf << endl;
			}
		}
	}
	else {
		cout << "can not open" << endl;
	}
	file.close();
	return 0;
}
```

练习：

试着写一个程序，该程序接受用户输入的用户名和密码，并把用户名和密码保存在`user.txt`文件中

![image-20220225093617372](https://gitee.com/gaoxianglong/picgo/raw/master/img/image-20220225093617372.png)

```c++
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
	fstream file("user.txt", ios::out);
	if (!file.fail())
	{
		char buf[128] = { 0 };
		cout << "请输入用户名:" << endl;
		cin >> buf;
		file << buf << "\n";
		cout << "请输入密  码:" << endl;
		cin >> buf;
		file << buf << "\n";
	}
	else {
		cout << "can not open" << endl;
	}
	file.close();
	return 0;
}
```

尝试着将`user.txt`文件中的用户名密码读取出来并输出。

![image-20220225094236151](https://gitee.com/gaoxianglong/picgo/raw/master/img/image-20220225094236151.png)

```c++
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
	fstream file("user.txt", ios::in);
	int i = 1;
	if (!file.fail())
	{
		while (!file.eof())
		{
			char buf[128];
			file.getline(buf, 128);
			if (file.tellg() > 0)
			{
				if (i % 2 != 0) {
					cout << "账号:";
				}
				else {
					cout << "密码:";
				}
				cout << buf;
				cout << endl;
				i++;
			}
		}
	}
	else {
		cout << "can not open" << endl;
	}
	file.close();
	return 0;
}
```

**复制文件：**

```c++
#include <iostream>
#include <fstream>
#include <cstring>
using namespace std;
int main()
{
    ifstream infile;
    ofstream outfile;
    char name[100];
    char bufName[100];
    char c;
    cout << "请输入文件：" << "\n";
    cin >> name; // 输入文件名
    infile.open(name); // 打开文件
    if (!infile) {
        cout << "文件打开失败！";
        exit(1);
    }
    strcat_s(name, "副本"); // 重命名文件
    cout << "开始复制" << endl;
    outfile.open(name); // 创建文件并打开
    if (!outfile)
    {
        cout << "无法复制";
        exit(1);
    }
    while (infile.get(c))
    {
        outfile << c;
    }
    cout << "完成" << endl;
    infile.close();
    outfile.close();
    return 0;
}
```

**get()**

| 函数 | 作用                                                         |
| ---- | ------------------------------------------------------------ |
| get  | 获取文件中的字符，流指针会依次往后移动，直到后面没有后就返回`-1` |

```c++
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
	ifstream ifile("user.txt");
	if (!ifile)
	{
		cerr << "open fail" << endl;
	}
	char ch;
	while (ifile.get(ch))
	{
		cout << ch;
	}
	cout << endl;
	ifile.close();
	return 0;
}
```

**删除文件：**

| 函数   | 作用                                |
| ------ | ----------------------------------- |
| remove | 删除文件，成功返回`0`,失败返回`-1`. |

```c++
#include <iostream>
using namespace std;
int main()
{
    char file[50];
    cout << "Input file name:" << "\n";
    cin >> file;
    if (!remove(file))
    {
        cout << "The file:" << file << "已删除" << "\n";
    }
    else {
        cout << "删除失败" << file;
    }
    return 0;
}
```

