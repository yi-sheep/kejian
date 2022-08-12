---
title: c++阶段二第九讲
date: 2021-11-11 15:15:57
tags: [教材,阶段二]
categories: c++
---

# 第九讲

![image-20211111153025496](https://gitee.com/gaoxianglong/picgo/raw/master/img/image-20211111153025496.png)

## 井字棋-地图绘制

地图分析：

+ 拆分

  + 第一行

    ` | 1 | 2 | 3 |`

  - 第二、四、六、八行

    `-|---|---|---|`

  - 第三行

    `1|   |   |   |`

  - 第五行

    `2|   |   |   |`

  - 第七行

    `3|   |   |   |`

地图打印：

```c++
for(int i = 0;i<8;i++){
    if(i==0){
        cout<<" | 1 | 2 | 3 |"<<endl;
    }else if(i==1||i==3||i==5||i==7){
        cout<<"-|---|---|---|"<<endl;
    }else if(i==2){
        cout<<"1|   |   |   |"<<endl;
    }else if(i==4){
        cout<<"2|   |   |   |"<<endl;
    }else if(i==6){
        cout<<"3|   |   |   |"<<endl;
    }
}
```

棋位抽取

```c++
for(int i = 0;i<8;i++){
    if(i==0){
        cout<<" | 1 | 2 | 3 |"<<endl;
    }else if(i==1||i==3||i==5||i==7){
        cout<<"-|---|---|---|"<<endl;
    }else if(i==2){
        cout << "1| " << qipan[0][0] << " | " << qipan[0][1] << " | " << qipan[0][2] << " |"<<endl;
    }else if(i==4){
        cout << "2| " << qipan[1][0] << " | " << qipan[1][1] << " | " << qipan[1][2] << " |"<<endl;
    }else if(i==6){
        cout << "3| " << qipan[2][0] << " | " << qipan[2][1] << " | " << qipan[2][2] << " |"<<endl;
    }
}
```

