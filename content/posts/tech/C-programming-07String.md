---
title: "【嵌入式C语言编程】第七章 字符串处理函数"
date: 2023-10-01T00:17:58+08:00
lastmod: 2023-10-01T00:17:58+08:00
author: ["Eddy"]
keywords: 
- C programming
- Embedded Development
- String Manipulation functions
- C语言
- C语言编程
- 嵌入式编程
- 字符串处理函数
- C语言字符串处理函数
categories: 
- 
tags: 
- C语言
- C语言 字符串处理函数
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

## 第七章 字符串处理函数

## INIT

<div align = "center">
<img src = "https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/Blog-Common-Images/INIT.jpg" alt = "INIT.jpg" width = "70%" height = "auto">
</div>

<br/>

>**INIT：本节内容正式开始。action!**



### 一、获取字符串长度函数

```C
#include <string.h>
size_t strlen(const char *s);
功能：计算一个字符串的长度
参数：
  s：指定的字符串
返回值：
  当前字符串的长度
注意：strlen获取的字符串长度遇到第一个\0结束且\0不算做字符串长度之中
```

```C
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
  //使用strlen函数获取字符串的长度
  //strlen获取的字符串的长度遇到第一个\0结束
  char s1[100] = "hel\0lo";

  printf("s1_len = %d\n", strlen(s1));
  printf("s1_size = %d\n", sizeof(s1));

  char *s2 = "hello";

  printf("s2_len = %d\n", strlen(s2));
  printf("s2_size = %d\n", sizeof(s2));

  return 0;
}
```

执行结果

```C
s1_len = 3
s1_size = 100
s2_len = 5
s2_size = 4
```



### 二、字符串拷贝函数

```C
#include <string.h>
char *strcpy(char *dest, const char *src);
功能：将src复制给dest
参数：
  dest：目的字符串
  src：源字符串
返回值：
  保存dest字符串的首地址
注意：
  使用strcpy函数复制字符串时必须保证dest足够大，否则会内存溢出
  strcpy是将src字符串中第一个\0之前包括\0复制给dest

char *strncpy(char *dest, const char *src, size_t n);
函数的说明：
  将src指向的字符串前n个字节，拷贝到dest指向的内存中
返回值:
  目的内存的首地址
注意：
  1、strncpy不拷贝 ‘\0’
  2、如果n大于src指向的字符串中的字符个数，则在dest后面填充n‐strlen(src)个’\0’
```

```C
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
  //使用strcpy函数拷贝字符串
  char s1[32] = "hello world";
  //使用strcpy函数时，必须保证第一个参数的内存足够大
  //char s1[5] = "abcd";
  char s2[32] = "abcdefg";

  strcpy(s1, s2);

  printf("s1 = %s\n", s1);

  int i;
  for(i = 0; i < 32; i++)
  {
    printf("[%c] ‐ %d\n", s1[i], s1[i]);
  }

  return 0;
}
```

执行结果

```C
s1 = abcdefg
[a] - 97
[b] - 98
[c] - 99
[d] - 100
[e] - 101
[f] - 102
[g] - 103
[] - 0
[r] - 114
[l] - 108
[d] - 100
[] - 0
[] - 0
```



### 三、字符串追加函数

```C
#include <string.h>
char *strcat(char *dest, const char *src);
功能：将src追加到dest的后面
参数：
  dest：目的字符串
  src：源字符串
返回值：
  保存dest字符串的首地址

char *strncat(char *dest, const char *src, size_t n);
追加src指向的字符串的前n个字符，到dest指向的字符串的后面。
注意如果n 大于src的字符个数，则只将src字符串追加到dest指向的字符串的后面
追加的时候会追加’\0’
```

```C
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
  //使用strcat函数追加字符串
  char s1[32] = "hello world";
  char s2[32] = "abcdef";

  //strcat是从s1的\0的位置开始追加，直到s2的第一个\0复制完毕后结束
  strcat(s1, s2);

  printf("s1 = %s\n", s1);

  return 0;
}
```

执行结果

```C
s1 = hello worldabcdef
```



### 四、字符串比较函数

```C
#include <string.h>
int strcmp(const char *s1, const char *s2);
int strncmp(const char *s1, const char *s2, size_t n);
功能：strcmp是比较两个字符串的内容，strncmp是比较两个字符串的前n个字节是否一样
参数：
  s1、s2：要比较的两个字符串
  n：strncmp中的参数n表示要比较的字节数
返回值：
   0 s1 = s2
  >0 s1 > s2
  <0 s1 < s2
```

```C
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
  //使用strcmp比较两个字符串的内容是否一致
  //strcmp函数一个字符一个字符比较，只要出现不一样的，就会立即返回
  char s1[] = "hello";
  char s2[] = "w";

  int ret = strcmp(s1, s2);

  if(ret == 0)
  {
    printf("s1 = s2\n");
  }
  else if(ret > 0)
  {
    printf("s1 > s2\n");
  }
  else
  {
    printf("s1 < s2\n");
  }

  return 0;
}
```

执行结果

```C
s1 < s2
```



### 五、字符查找函数

```C
#include <string.h>
char *strchr(const char *s, int c);
功能：在字符指针s指向的字符串中，找ascii 码为c的字符
参数：
  s：指定的字符串
  c：要查找的字符
返回值：
  成功：找到的字符的地址
  失败：NULL
注意：s指向的字符串中有多个ASCII为c的字符，则找的是第1个字符

char *strrchr(const char *s, int c);
功能：在s指向的字符串中，找最后一次出现的ASCII为c的字符，
```

```C
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
  //使用strchr函数在一个字符串中查找字符
  char s[] = "hel6lo wor6ld";
  //找第一个匹配的字符
  char *ret = strchr(s, '6');
  //找最后一个匹配的字符
  //char *ret = strrchr(s, '6');

  if(ret == NULL)
  {
    printf("没有找到\n");
  }
  else
  {
    printf("找到了，在数组的第%d个位置\n", ret ‐ s);
  }

  return 0;
}
```

执行结果

```C
找到了，在数组的第3个位置
```



### 六、字符串匹配函数

```C
#include <string.h>
char *strstr(const char *haystack, const char *needle);
函数说明：
  在haystack指向的字符串中查找needle指向的字符串，也是首次匹配
返回值：
  找到了：找到的字符串的首地址
  没找到：返回NULL
```

```C
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
  //使用strstr函数在一个字符串中查找另一个字符串
  char s[] = "1234:4567:666:789:666:7777";

  //strstr查找的时候，查找的是第二个参数的第一个\0之前的内容
  char *ret = strstr(s, "666");

  if(ret == NULL)
  {
    printf("没找到\n");
  }
  else
  {
    printf("找到了，在当前字符串的第%d个位置\n", ret ‐ s);
  }
  return 0;
}
```

执行结果

```C
找到了，在当前字符串的第10个位置
```



### 七、字符串转换数值

```C
#include <stdlib.h>
int atoi(const char *nptr);
功能：将一个数字型字符串转化为整形数据
参数：
  nptr：指定的字符串
返回值：
  获取到的整形数据
```

```C
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[])
{
  //使用atoi将数字型字符串转化为整形数据
  char s1[] = "7856";
  int ret1 = atoi(s1);

  printf("ret1 = %d\n", ret1);
  
  //使用atof将浮点型的字符串转化为浮点型数据
  char s2[] = "3.1415926";
  double ret2 = atof(s2);

  printf("ret2 = %lf\n", ret2);

  return 0;
}
```

执行结果

```C
ret1 = 7856
ret2 = 3.141593
```



### 八、字符串切割函数

```C
#include <string.h>
char *strtok(char *str, const char *delim);
功能：对字符串进行切割
参数：
  str：要切割的字符串
  第一次切割，就传入指定的字符串，后面所有次的切割传NULL
  delim：标识符，要根据指定的delim进行切割，切割的结果不包含delim
返回值：
  返回切割下来的字符串的首地址，如果都切割完毕，则返回NULL
```

```C
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[])
{
  //使用strtok函数切割字符串
  char s[] = "111:22222:33:4444444444:5555555555555";
  char *ret;

  //第一次切割
  ret = strtok(s, ":");
  printf("ret = %s\n", ret);

  //后面所有切割时都要将strtok的第一个参数传NULL
  while((ret = strtok(NULL, ":")) != NULL)
  {
    printf("ret = %s\n", ret);
  }

  return 0;
}
```

执行结果

```C
ret = 111
ret = 22222
ret = 33
ret = 4444444444
ret = 5555555555555
```

### 九、格式化字符串操作函数

```C
#include <stdio.h>
int sprintf(char *str, const char *format, ...);
功能：将按照格式保存的字符串复制给str
参数：
  str：保存字符串
  format：同printf
返回值：
  保存的字符串的字节数


#include <stdio.h>
int sscanf(const char *str, const char *format, ...);
功能：scanf是从终端读取数据并赋值给对应变量，而sscanf是从第一个参数中读取数据
参数：
  str：指定要获取内容的字符串
  format：按照格式获取数据保存在变量中
返回值：
  成功获取的个数
```

#### 9.1 sprintf和sscanf的基本用法

```C
//sprintf和sscanf的基本用法
void test1()
{
  char buf[20];
  int a, b, c;

  sprintf(buf,"%d:%d:%d",2013,10,1);
  printf("buf = %s\n",buf);

  sscanf("2013:10:1", "%d:%d:%d", &a, &b, &c);
  printf("a=%d,b=%d,c=%d\n",a,b,c);
}
```

执行结果

```C
buf = 2013:10:1
a=2013,b=10,c=1
```



#### 9.2 sscanf高级用法

```C
//sscanf高级用法
void test2()
{
  //1、跳过数据：%*s或%*d
  char buf1[20];
  sscanf("1234 5678","%*d %s",buf1);
  printf("%s\n",buf1);

  //2、读指定宽度的数据：%[width]s
  char buf2[20];
  sscanf("12345678","%4s ",buf2);
  printf("%s\n",buf2);

  //3、支持集合操作：只支持获取字符串
  // %[a‐z] 表示匹配a到z中任意字符(尽可能多的匹配)
  // %[aBc] 匹配a、B、c中一员，贪婪性
  // %[^aFc] 匹配非a、F、c的任意字符，贪婪性
  // %[^a‐z] 表示读取除a‐z以外的所有字符
  char buf3[20];
  sscanf("agcd32DajfDdFF","%[a‐z]",buf3);
  printf("%s\n",buf3);
}
```

执行结果

```C
5678
1234
agcd
```



### 十、const

```C
#include <stdio.h>

//const修饰全局变量
//此时全局变量只能使用但是不能修改，
//如果直接拿全局变量修改值，编译直接报错
//如果使用全局变量的地址修改值，运行时程序异常结束
const int a = 100;
void test1()
{
  printf("a = %d\n", a);

  //a = 666;
  //printf("a = %d\n", a);

  int *p = &a;
  *p = 888;
  printf("a = %d\n", a);
}

//const修饰普通局部变量
//可以读取变量的值
//不能直接通过变量进行修改值，编译报错
//可以通过变量的地址修改值
void test2()
{
  const int b = 100;
  printf("b = %d\n", b);

  //b = 666;
  //printf("b = %d\n", b);

  int *p = &b;
  *p = 888;
  printf("b = %d\n", b);
}

    //const修饰指针变量
    //如果const修饰指针变量的类型，无法通过指针变量修改地址里面的值
    //如果const修饰指针变量，无法修改指针变量保存的地址
    //如果const既修饰指针变量的类型，又修饰指针变量，则只能通过原本变量修改值
void test3()
{
  int c = 100;
  //const修饰指针变量的类型
  //const int * p = &c;
  //const修饰指针变量
  //int * const p = &c;
  //const既修饰指针变量的类型，又修饰指针变量
  const int * const p = &c;
  printf("*p = %d\n", *p);

  c = 666;
  printf("*p = %d\n", *p);

  *p = 777;
  printf("*p = %d\n", *p);

  int d = 888;
  p = &d;
  printf("*p = %d\n", *p);
}

int main(int argc, char *argv[])
{
  test3();

  return 0;
}
```

## END

>**END：本节内容到此结束。**

个人提升之余，别忘了和小伙伴积极交流，很多人觉得他们在思考，而实际上他们只是在重新整理自己的偏见。请珍惜和他人交流讨论的机会。

<br/>

<div align = "center">
<img src = "https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/Blog-Common-Images/END1.jpg" alt = "END1.jpg" width = "70%" height = "auto">
</div>

<br/>

希望你每一天都有所收获，进步up up up。今天的我们并不比昨天更聪明，但一定要比昨天更睿智。

<div align = "center">
<img src = "https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/Blog-Common-Images/END2.jpg" alt = "END2.jpg" width = "70%" height = "auto">
</div>

<br/>





**彩蛋**🎁

当你走在灿烂的阳光下，你会惊奇地发现，生命的一切及苦难，不过是在插满尖玻璃的墙头上行走。

- 塞斯·诺特博姆《狐狸在夜晚来临》

恭喜你🎉，完成了对第七章《字符串处理函数》部分的学习，下一章我们将学习结构体，共用体，枚举。

⏩第八章 《结构体，共用体，枚举》
