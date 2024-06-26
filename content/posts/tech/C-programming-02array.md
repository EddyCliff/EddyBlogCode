---
title: "【嵌入式C语言编程】第二章 数组"
date: 2023-09-16T00:17:58+08:00
lastmod: 2023-09-16T00:17:58+08:00
author: ["Eddy"]
keywords: 
- C programming
- Embedded Development
- array
- C语言
- C语言编程
- 嵌入式编程
- 数组
- C语言数组
categories: 
- 
tags: 
- C语言
- C语言 数组
description: 
weight:
slug: ""
draft: false # 是否为草稿
comments: false
reward: false # 打赏
mermaid: true #是否开启mermaid
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true #顶部显示路径
cover:
    image: "https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/BlogCover/c2.jpg" #图片路径例如：posts/tech/123/123.png
    caption: "" #图片底部描述
    alt: ""
    relative: false
---

## 第二章 数组

## INIT

<div align = "center">
<img src = "https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/Blog-Common-Images/INIT.jpg" alt = "INIT.jpg" width = "70%" height = "auto">
</div>

<br/>

>**INIT：本节内容正式开始。action!**




### 一、数组的概念

数组是若干个相同类型的变量在内存中有序存储的集合。

概念理解：

数组用于存储一组数据

数组里面存储的数据类型必须是相同的

数组在内存中会开辟一块连续的空间

`int a[10];`

//定义了一个整型的数组a，a是数组的名字，数组中有10个元素，每个元素的类型都是int类型，而且在内存中连续存储。

这十个元素分别是`a[0] a[1] …. a[9]`。

`a[0]~a[9]`在内存中连续的顺序存储。



### 二、数组的分类

#### 2.1 按元素的类型分类

1）字符数组

即若干个字符变量的集合，数组中的每个元素都是字符型的变量

`char s[10]; s[0],s[1]....s[9];`

2）短整型的数组

`short int a[10]; a[0] ,a[9]; a[0]=4;a[9]=8;`

3）整型的数组

`int a[10]; a[0] a[9]; a[0]=3;a[0]=6;`

4） 长整型的数组

`lont int a[5];`

5）浮点型的数组（单、双）

`float a[6]; a[4]=3.14f;`

`double a[8]; a[7]=3.115926;`

6）指针数组

`char *a[10];`

`int *a[10];`

7）结构体数组

`struct stu boy[10];`



#### 2.2 按维数分类

一维数组

`int a[30];`

类似于一排平房

二维数组

`int a[2][30];`

可以看成一栋楼房 有多层，每层有多个房间，也类似于数学中的矩阵

二维数组可以看成由多个一维数组构成的。

有行，有列，

多维数组

`int a[4][2][10];`

三维数组是由多个相同的二维数组构成的

`int a[5][4][2][10];`



### 三、数组的定义

#### 3.1 一维数组的定义

格式：

数据类型 数组名[数组元素个数];

例如：

`int a[10];`

 //定义了一个名为a的数组，数组中每一个元素都是int类型，一共有10个元素

//每一个元素都保存在一个变量中，每一个变量都是有数组名和数组下标组成的

//并且是从0开始的，分别是`a[0] a[1] a[2]... a[9]`

注意：数组元素的个数在定义的时候也可以不写，但是如果不写，必须初始化（定义的时候赋值）

```C
#include <stdio.h>

int main(int argc, char *argv[])
{
    //定义一个一维数组
    int a[10];
    //通过sizeof关键字可以获取数组的大小
    printf("sizeof(a) = %d %d\n", sizeof(a), 10 * sizeof(int));

    //如果定义数组的同时赋值（初始化），可以不指定数组元素的个数，系统会根据初始化元素的个数自动指定数组元素的个数
    int b[] = {10, 20, 30};
    printf("sizeof(b) = %d\n", sizeof(b));
  
    return 0;
}
```

执行结果

```C
sizeof(a) = 40 40
sizeof(b) = 12
```



#### 3.2 二维数组的定义

格式:

数据类型 数组名[行的个数][列的个数];

例如：

`int a[2][4];`

解释：

定义一个名为a的二维数组，每一个元素都是int类型

这个二维数组中包含两行四列的元素，一共有8个元素

二维数组也是连续开辟空间，访问元素是行和列都是从0开始，分别是`a[0][0] a[0][1] a[0][2] a[0][3] a[1][0] a[1][1] a[1][2] a[1][3]`

注意：二维数组的下标也是可以省略的，但是有条件，在初始化时行数可以省略，但是列数不能省略

```C
//定义一个二维数组
    int c[2][4];
    printf("sizeof(c) = %d %d\n", sizeof(c), 2 * 4 * sizeof(int));

    //二维数组的行数可以省略，但是列数不能省略，在初始化时可以这样操作
    //系统会根据列数自动指定行数，最终得到的函数所得到得元素个数移动是列的整数倍
    int d[][4] = {1, 2, 3, 4, 5};
    printf("sizeof(d) = %d\n", sizeof(d));
```

执行结果

```C
sizeof(c) = 32 32
sizeof(d) = 32
```



- 为什么sizeof(d) = 32？

    假设 `sizeof(int)` 在您的系统上是4字节，通常情况下，`int` 类型需要按4字节对齐。因此，编译器会在数组 `d` 的每一行之后添加填充以确保每一行都满足对齐要求。

    所以，虽然数组中的实际数据只占用20字节（5个 `int` 值 * 4字节），但由于填充字节，`sizeof(d)` 返回32字节。

    这种情况下的内存布局可能如下所示：

    ```C
    [1][2][3][4][5][0][0][0]
    ```

    这些额外的0值字节是为了满足内存对齐要求而添加的，因此导致 `sizeof(d)` 返回32字节。不同的编译器和系统可能会有不同的对齐规则，因此结果可能会有所不同。



### 四、定义并初始化

#### 4.1 一维数组的初始化

```C
#include<stdio.h>

int main(int argc, char *argv[])
{
    //以一维数组的初始化
    //如果不初始化，直接使用会是随机值
    //int a[4];

    //初始化方式1：全部初始化
    //int a[4] = {123, 78, 666, 476};
    //如果是全部 初始化，可以不指定数组元素的个数，系统会自动分配
    //int a[] = {10, 20, 30, 40};

    //初始化方式2：局部初始化
    //未初始化的位置的元素自动赋值为0
    int a[4] = {10, 20};

    printf("%d\n",a[0]);
    printf("%d\n",a[1]);
    printf("%d\n",a[2]);
    printf("%d\n",a[3]);

    return 0;
}
```



#### 4.2 二维数组的初始化

**按行初始化：**

a、全部初始化

`int a[2][2]={{1,2},{4,5}};`

`a[0][0] =1; a[0][1] = 2; a[1][0] = 4,a[1][1]=5;`

b、部分初始化

`int a[3][3]={{1,2},{1}};`

`a[0][0] = 1;a[0][2] =0;`

**逐个初始化：**

全部初始化：

`int a [2][3]={2,5,4,2,3,4};`

部分初始化：

`int a[2][3]={3,5,6,8};`

```C
#include <stdio.h>

int main(int argc, char *argv[])
{
    //二维数组的初始化
    //int a[2][3];

    //初始化方式1：按行初始化
    //全部初始化
    //int a[2][3] = {{10, 20, 30}, {666, 777, 888}};
    //局部初始化
    //没有赋值的位置的元素自动为0
    //int a[2][3] = {{10, 20}, {666}};

    //初始化方式2：逐个初始化
    //全部初始化
    //int a[2][3] = {1, 2, 3, 4, 5, 6};
    //局部初始化
    //没有赋值的位置的元素自动为0
    int a[2][3] = {1, 2, 3};

    printf("%d\n", a[0][0]);
    printf("%d\n", a[0][1]);
    printf("%d\n", a[0][2]);
    printf("%d\n", a[1][0]);
    printf("%d\n", a[1][1]);
    printf("%d\n", a[1][2]);

    return 0;
}
```



### 五、数组元素的引用方法

一维数组元素的引用方法

数组名[下标]；//下标代表数组元素在数组中的位置，注意从0开始

`int a[10];`

二维数组元素的引用方法

数组名[行下标][列下标];

`int a[3][4];`

```C
#include<stdio.h>

int main(int argc, char *argv[])
{
    //一维数组的引用以及一维数组的遍历
    int a[6] = {111, 222, 333, 444, 555, 666};

    a[3] = 10000;

    //一维数组的遍历
    int i;
    for(i = 0; i < sizeof(a) / sizeof(int); i++)
    {
        printf("a[%d] = %d\n", i, a[i]);
    }

    printf("**********************\n");

    //二维数组的引用以及二维数组的遍历
    int b[3][4] = {1, 2, 3, 4,
                  5, 6, 7, 8,
                  9, 10, 11, 12};

    b[2][0] = 666;

    //二维数组的遍历
    int m, n;
    //外层循环控制行数
    for(m = 0; m < 3; m++)
    {
        //内层循环控制列数
        for(n = 0; n < 4; n++)
        {
            printf("%-4d", b[m][n]);
        }
        printf("\n");
    }

    return 0;
}
```

执行结果

```C
a[0] = 111
a[1] = 222
a[2] = 333
a[3] = 10000
a[4] = 555
a[5] = 666
**********************
1   2   3   4
5   6   7   8
666 10  11  12
```



### 六、字符数组的定义和初始化问题

`char c1[] ={'c','p','r','o','g'};`

`char c2[] =  "c prog";`

`char a[][5] = {`

`{'B', 'A', 'S', 'I', 'C'},`

`{'d', 'B', 'A', 'S', 'E'}`

`};`

`char a[][6] = {"hello","world"};`

**字符数组的引用**

1.用字符串方式赋值比用字符逐个赋值要多占1个字节,用于存放字符串结束标志‘\0’;

2.上面的数组c2在内存中的实际存放情况为：

<br/>

<div align="center">
<img src="https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/Embedded_high-level_C_programming/02array_image.png" alt = "02array_image.png" width="70%" height="auto" />
</div>

<br/>

注：'\0'是由C编译系统自动加上的3.由于采用了'\0'标志，字符数组的输入输出将变得简单方便.

3.由于采用了'\0'标志，字符数组的输入输出将变得简单方便.

```C
#include <stdio.h>

int main(int argc, char *argv[])
{
    //定义一个字符数组，通过scanf函数输入字符串并输出结果
    //通过赋值""这样的方式可以清除字符数组中的垃圾字符，让每一个元素都是\0
    char ch[32] = "";

    //数组名就是当前数组的首地址，所以scanf的第二个参数直接传数组名即可
    scanf("%s", ch);

    printf("ch = %s\n", ch);

    return 0;
}
```

执行结果

```C
nihao
ch = nihao
```

## END

>**END：本节内容到此结束。**

个人提升之余，别忘了和小伙伴积极交流，很多人觉得他们在思考，而实际上他们只是在重新整理自己的偏见。请珍惜和他人交流讨论的机会。

<br/>

<div align = "center">
<img src = "https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/Blog-Common-Images/END1.jpg" alt = "END1.jpg" width = "70%" height = "auto">
</div>

希望你每一天都有所收获，进步up up up。今天的我们并不比昨天更聪明，但一定要比昨天更睿智。

<br/>

<div align = "center">
<img src = "https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/Blog-Common-Images/END2.jpg" alt = "END2.jpg" width = "70%" height = "auto">
</div>

<br/>

**彩蛋**🎁

秋日薄暮，用菊花煮竹叶青，人与海棠俱醉。 

- 林清玄《温一壶月光下酒》

恭喜你🎉，完成了对第二章《数组》部分的学习，下一章我们将学习函数。


⏩第三章 《函数》