---
title: "【浅谈LLC谐振变换器】-章节3:LLC特性分析"
date: 2023-11-05T00:17:58+08:00
lastmod: 2023-11-05T00:17:58+08:00
author: ["Eddy"]
keywords: 
- LLC resonant converter
- switching mode power supply
- Power technology
categories: 
- 
tags: 
- LLC resonant converter
- switching mode power supply
- Power technology
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
    image: "https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/BlogCover/pcb2.jpg" #图片路径例如：posts/tech/123/123.png
    caption: "" #图片底部描述
    alt: ""
    relative: false
---
> **启程-第4站**
> 
尊敬的乘客，您好。

我是Eddy，将在这趟知识的列车旅程中担任您的列车长。欢迎您登上“探险号”，在这里，每次启程都承载着新的发现与学习的机会。

本次列车的目的地——LLC谐振变换器，一个在现代电子设备中不可或缺的神秘组件。它利用巧妙的物理原理有效减少能量损失，保证了我们设备的高效运行。

在接下来的行程中，无论您是刚接触电子的新手，还是希望巩固基础知识的老手，我都希望这次旅程能为您带来新的灵感和知识。请您准备好您的工具包，我们即将启程，深入探索LLC谐振变换器的奇妙世界。期待在旅途中与您共同探讨、学习，并享受这一探索之旅。

那么，请扣好安全带，我们这就出发吧！  

本次行车路线：LLC的定义及优势 - LLC入门 - LLC工作原理 - LLC特性分析  
🚄前方到站是：LLC特性分析  
## LLC谐振变换器特性分析

### LLC谐振变换器FHA等效模型推导

用基波等效法推出它的等效电阻Req，用等效模型从而推出电压增益。

![03image.png](https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/LLC_Resonant_Converters/03image.png)

由等效图可知，

$电压增益=\frac{\text{R}eq}{\text{}整个电路的阻抗}$

Req就是整流网络加上变压去等效到原边的阻抗Req。

而由图可知，

$Req =\frac{\text{V}p}{\text{I}p}$

这里我们用到基波等效分析法求Vp和Ip。

先介绍一下傅里叶级数的基本概念。

> **傅里叶级数基本概念**

周期为2π的函数f(x)傅里叶级数展开后的表达式为：

$f(x) = {{{a_0}} \over 2} + \sum\limits_{n = 1}^\infty {({a_n}\cos {nx} + {b_n}\sin {nx})}$

其中：

$\begin{aligned}
&a_{n} =\frac{1}{\pi}\int_{-\pi}^{\pi}f\bigl(x\bigr)\cos nxdx  \\
&b_{n} =\frac{1}{\pi}\int_{-\pi}^{\pi}f\bigl(x\bigr)\sin nxdx  \\
&a_{0} =\frac1\pi\int_{-\pi}^{\pi}f(x)dx 
\end{aligned}$

> **1）Vd方波的傅里叶级数展开**

半波Vd傅里叶级数展开后的表达式为：

$\nu_{d}\left(t\right)=\frac{V_{bus}}{2}+\frac{2V_{bus}}{\pi}\sum_{n=1,3,5,...}^{\infty}\frac{1}{n}\sin(n\omega_{s}t)$

基波分量表达式为：

$\nu_{d}\left(t\right)=\frac{2V_{bus}}{\pi}\sin(\omega_{s}t)$

![03image1.png](https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/LLC_Resonant_Converters/03image1.png)



> **2）变压器原边电压Vp傅里叶级数展开**

Vp傅里叶级数展开的表达式为：

$\nu_{p}\left(t\right)=\frac{4NV_{o}}{\pi}\sum_{n=1,3,5,..}^{\infty}\frac{1}{n}\sin(n\omega_{s}t-\varphi)$

基波分量与方波电压是同相的，因此，取n=1可得其基波分量表达式为：

$\begin{aligned}V_{p1}\left(t\right)&=\frac{4NV_{o}}{\pi}\sin(\omega_{s}t-\varphi)=\sqrt{2}V_{p1rms}\sin(\omega_{s}t-\varphi)\\&\quad V_{p1rms}=\frac{4NV_{o}}{\pi}/\sqrt{2}=\frac{2\sqrt{2}NV_{o}}{\pi}\end{aligned}$

![03image2.png](https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/LLC_Resonant_Converters/03image2.png)

> **3）变压器原边电压ip傅里叶级数展开**

ip可以近似认为是一正弦基波分量，其表达式为:

$i_{_p}\left(t\right)=\sqrt{2}I_{_{prms}}\sin(\omega_st-\varphi)$

上式最关键的是计算Iprms：

$I_o=\frac1{2\pi}\int_0^{2\pi}i_o\left(t\right)dt=\frac1{2\pi}\int_0^{2\pi}N\left|i_p\left(t\right)\right|dt=\frac{2\sqrt{2}N}\pi I_{prms}$

$I_{prms}=\frac{I_{o}\pi}{2\sqrt{2}N}$

![03image3.png](https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/LLC_Resonant_Converters/03image3.png)

> **4）等效电阻Req**

$R_{eq}=\frac{\nu_{_{p1}}}{i_p}=\frac{\frac{4NV_o}\pi\sin(\omega_st-\varphi)}{\frac{I_o\pi}{2N}\sin(\omega_st-\varphi)}=\frac{8N^2}{\pi^2}R_L$

#### LLC谐振变换器电压增益

根据上图可以得到LLC谐振变换器的交流电压增益为：

$H(j\omega)=\frac{V_{p1}(j\omega)}{V_{d1}(j\omega)}=\frac{R_{eq}\parallel j\omega L_m}{j\omega L_r+\frac1{j\omega C_r}+R_{eq}\parallel j\omega L_m}$

定义励磁电感与谐振电感之比为：

$\gamma=\frac{L_m}{L_r}$

品质因数Q：

$Q=\frac{Z_r}{R_{eq}}=\frac{\sqrt{\frac{L_r}{C_r}}}{R_{eq}}$

归一化频率：

$f_n=\frac{f_s}{f_r}$



可以得到LLC谐振变换器的电压增益函数为：

$M(f_n)=\frac1{\sqrt{\left[1+\frac1\gamma(1-\frac1{f_n}^2)\right]^2+\left[Q(f_n-\frac1{f_n})\right]^2}}$





### LLC谐振变换器电压增益曲线分析 - Q值和γ值的选取

> **课程回顾**

![03image4.png](https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/LLC_Resonant_Converters/03image4.png)

> **Q值对增益的影响**

![03image5.png](https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/LLC_Resonant_Converters/03image5.png)

> **γ值对增益的影响**

![03image6.png](https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/LLC_Resonant_Converters/03image6.png)

> **Q与γ的选取思路**

1. 由输入电压变换引起的最大输出电压变换范围

2. 由空载到满载引起的输出电压变换

3. 确保整个工作区ZVS，从而降低损耗

$V_O=M\times\frac1N\times\frac{V\mathrm{in}}2$

![03image7.png](https://testingcf.jsdelivr.net/gh/EddyCliff/ChartBed/LLC_Resonant_Converters/03image7.png)



## 参考/感谢

[1]ST. Simplified Analysis and Design of Series resonant LLC Half-bridge Converters.

[2][https://www.bilibili.com/video/BV1tG411j7Vx/?p=5&spm_id_from=pageDriver&vd_source=c57cc7d724946a8cfa6381f148e147d5](https://www.bilibili.com/video/BV1tG411j7Vx/?p=5&spm_id_from=pageDriver&vd_source=c57cc7d724946a8cfa6381f148e147d5)

🚉尊敬的旅客朋友们，已到站，本站是：LLC特性分析，请需要下车的乘客带好随身物品有序下车。

⏩下一站是：LLC参数设计
