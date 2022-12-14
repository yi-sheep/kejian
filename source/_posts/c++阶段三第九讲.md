---
title: c++阶段三第九讲
date: 2021-11-11 15:58:04
tags: [教材,阶段三]
categories: c++
---

# 第九讲

创建一个10个房间的数组，我们往里放值，可以放多少个？要是还想继续放怎么办？

## 容器

### 序列容器

#### 向量类容器

##### vector

创建公式：

`std::vector<数据类型> 名称;`

例如：

`std::vector<int> v;`

作用：从后面快速的插入与删除，直接访问任何元素

| 用法                 | 作用                               |
| -------------------- | ---------------------------------- |
| `v.begin(),v.end()`  | 返回vector的首、尾**迭代器**       |
| `v.front(),v.back()` | 返回vector的首、尾**元素**         |
| `v.push_back()`      | 从vector末尾加入一个元素           |
| `v.size()`           | 返回vector当前的长度（大小）       |
| `v.pop_back()`       | 从vector末尾删除一个元素           |
| `v.empty()`          | 返回vector是否为空，1为空、0不为空 |
| `v.clear()`          | 清空vector                         |

#### 双端队列容器

##### deque

创建公式：

`std::deque<数据类型> 名称;`

例如：

`std::deque<int> q;`

作用：从前面或后面快速的插入与删除，直接访问任何元素

| 用法                 | 作用                        |
| -------------------- | --------------------------- |
| `q.begin(),q.end()`  | 返回deque的首、尾**迭代器** |
| `q.front(),q.back()` | 返回deque的首、尾**元素**   |
| `q.push_back()`      | 从队后插入一个元素          |
| `q.push_front()`     | 从队前插入一个元素          |
| `q.pop_back()`       | 从队后删除一个元素          |
| `q.pop_front()`      | 从队前删除一个元素          |
| `q.clear()`          | 清空队列                    |

#### 链表容器

##### list

创建公式：

`std::list<数据类型> 名称;`

例如：
`std::list<int> l;`

作用：双链表，从任何地方快速插入与删除

| 用法                | 作用                             |
| ------------------- | -------------------------------- |
| `l.begin(),l.end()` | 返list的首、尾**迭代器**         |
| `l.push_back()`     | 从队尾入队一个元素               |
| `l.push_front()`    | 从队头入队一个元素               |
| `l.pop_back()`      | 从队尾出队一个元素               |
| `l.pop_front()`     | 从队头出队一个元素               |
| `l.size()`          | 返回当前容器实际包含的元素个数   |
| `l.empty()`         | 返回list是否为空，1为空、0不为空 |
| `l.clear()`         | 清空队列                         |

### 关联容器

### set容器

创建公式：

`std::set<数据类型> 名称;`

例如：

`std::set<int> s;`

作用：快速查找，不允许重复值

| 用法                | 作用                                                         |
| ------------------- | ------------------------------------------------------------ |
| `s.begin(),s.end()` | 返set的首、尾**迭代器**                                      |
| `s.insert()`        | 向 set 容器中插入元素                                        |
| `s.erase()`         | 删除 set 容器中存储的元素                                    |
| `s.find(val)`       | 在 set 容器中查找值为 val 的元素，如果成功找到，则返回指向该元素的双向迭代器；反之，则返回和 end() 方法一样的迭代器 |
| `s.size()`          | 返回当前容器实际包含的元素个数                               |
| `s.empty()`         | 返回set是否为空，1为空、0不为空                              |
| `s.clear()`         | 清空队列                                                     |

### multiset容器

multiset特性及用法和set完全相同，唯一的差别在于它允许键值重复。

创建公式：

`std::multiset<数据类型> 名称;`

例如：

`std::multiset<int> ms;`

### map容器

创建公式：

`map<键类型,数据类型> 名称;`

例如：

`std::map<int,int> intmap;`

作用：一对多映射，基于关键字快速查找，不允许重复键

| 用法                | 作用                                                         |
| ------------------- | ------------------------------------------------------------ |
| `m.begin(),m.end()` | 返map的首、尾**迭代器**                                      |
| `m.emplace()`       | 向 map容器中插入键和元素                                     |
| `m.erase()`         | 删除 map容器中存储的元素                                     |
| `m.find(val)`       | 在 map 容器中查找键为 val 的元素，如果成功找到，则返回指向该元素的双向迭代器；反之，则返回和 end() 方法一样的迭代器 |
| `m.size()`          | 返回当前容器实际包含的元素个数                               |
| `m.empty()`         | 返回map是否为空，1为空、0不为空                              |
| `m.clear()`         | 清空队列                                                     |

迭代器：

`(*i).first`键

`(*i).second`值

### multimap容器

multimap和map很相似，但是multiMap允许重复的键。

创建公式：

`std::multimap<键类型,数据类型> 名称;`

例如：

`std::multimap<int,int> intmap;`

