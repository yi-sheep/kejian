---
title: c++阶段四第一讲
date: 2022-02-16 09:15:35
tags: [教材,阶段四]
categories: c++
---

# 第一讲

## 文件操作

创建一个文件`test.txt`

### 打开文件

创建文件公式：

1. `文件流类 文件流对象名(文件名，打开方式);`

   比如：打开文件`test.txt`

   `ofstream outfile("test.txt",ios::out);`创建一个写入文件的对象，将`test.txt`文件以`out（写入）`的形式打开，如果当前项目下没有这个文件就创建文件。

   `outfile << "111";`将`111`写入到文件中。

2. `文件流对象名.open(文件名,打开方式);`

   比如：打开文件`test.txt`

   `ifstream infile;`创建一个读取文件的对象。

   `infile.open("test.txt",ios::in);`将`test.txt`文件以`in（读取）`的形式打开，如果当前项目下没有这个文件不会创建。

   读取并显示内容到控制台上

   ```c++
   #include <iostream>
   #include <fstream>
   using namespace std;
   int main()
   {
   	ifstream infile;
   	infile.open("test.txt", ios::in);
   	string a; // 创建一个变量用于存储文件中的数据
   	infile >>a; // 将文件中的数据通过提取符提取到变量中
   	cout << a; // 输出变量的值
   }
   ```

3. `fstream`可读可写

   写入：

   ```c++
   #include <iostream>
   #include <fstream>
   using namespace std;
   int main()
   {
   	fstream file;
   	file.open("test.txt", ios::out);
   	file << "12";
   }
   ```

   读取：

   ```c++
   #include <iostream>
   #include <fstream>
   using namespace std;
   int main()
   {
   	fstream of;
   	of.open("test.txt", ios::in);
   	string a;
   	of >> a;
   	cout << a;
   }
   ```

| 数据类型 | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| ofstream | 该数据类型表示输出文件流，用于创建文件并向文件写入信息。     |
| ifstream | 该数据类型表示输入文件流，用于从文件读取信息。               |
| fstream  | 该数据类型通常表示文件流，且同时具有 ofstream 和 ifstream 两种功能，这意味着它可以创建文件，向文件写入信息，从文件读取信息。 |

| 模式标志   | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| ios::ate   | 文件打开后定位到文件末尾。                                   |
| ios::in    | 打开文件用于读取。                                           |
| ios::app   | 追加模式。所有写入都追加到文件末尾。                         |
| ios::out   | 打开文件用于写入。                                           |
| ios::trunc | 如果该文件已经存在，其内容将在打开文件之前被截断，即把文件长度设为 0。 |

练习：

在程序设计，经常需要长期保存一些数据，如自动登录时，需要保存账号，请写一个程序，该程序接受用户输入的账号，之后创建一个以账号为文件名的文件。

```c++
/*
* 在程序设计，经常需要长期保存一些数据，
* 如自动登录时，需要保存账号，请写一个
* 程序，该程序接受用户输入的账号和密码，
* 之后创建一个以账号为文件名的文件，文件
* 中保存用户的密码。
*/
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
	char username[1000];
	cout << "请输入账号:";
	cin >> username;
	ofstream ofile;
	// 打开文件名为用户输入的账号的文件
	ofile.open(username);
	char password[1000];
	cout << "请输入密码:";
	cin >> password;
	ofile << password;
}
```

写一个程序，该程序连续创建 10 个文件，文件名为 1.txt,2.txt ... 10.txt。

```c++
#include <iostream>
#include <fstream>
using namespace std;
int main()
{
	ofstream ofile;
	char name[100];
	for (int i = 1; i <= 10; i++)
	{
		sprintf_s(name, "%d.txt", i);
		ofile.open(name);
		ofile.close();
	}
}
```

