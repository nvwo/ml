---
layout: post
title: 感知器 - Perceptron
date: 2020-04-15 23:12:24.000000000 +09:00
---
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/katex.min.css" integrity="sha384-yFRtMMDnQtDRO8rLpMIKrtPCD5jdktao2TV19YiZYWMDkUR5GQZR/NOVTdquEx1j" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/katex.min.js" integrity="sha384-9Nhn55MVVN0/4OFx7EE5kpFBPsEMZxKTCnA+4fqDmg12eCTqGi6+BB2LjY8brQxJ" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body,   {delimiters: [{left: '$$', right: '$$', display: true},{left: '$', right: '$', display: false}]});"></script>
[wikipedia原文](https://zh.wikipedia.org/wiki/%E6%84%9F%E7%9F%A5%E5%99%A8)
## 概述  
为了模拟神经细胞行为，与之对应的感知机基础概念被提出，如权量（突触）、偏置（阈值）及激活函数（细胞体） 
它可以被视为一种最简单形式的前馈神经网络，是一种二元线性分类器
感知机学习算法，常用的有感知机学习、最小二乘法和梯度下降法。
感知机主要的本质缺陷是它不能处理线性不可分问题。
## 历史  
* 1943年，心理学家沃伦·麦卡洛克和数理逻辑学家沃尔特·皮茨--M-P模型
* 1949年，心理学家唐纳德·赫布--神经元学习法则——赫布型学习
* 1957年，感知器是弗兰克·罗森布拉特（Frank Rosenblatt）就职于康奈尔航空实验室（Cornell Aeronautical Laboratory）时所发明的一种人工神经网络。  

## 定义  
感知器使用特征向量来表示的前馈神经网络，它是一种二元分类器，把矩阵上的输入x（实数值向量）映射到输出值f(x)上（一个二元的值）。
{% raw %}
$$ f(x)={\begin{cases}1&{\text{if }}w\cdot x+b>0\\0&{\text{else}}\end{cases}} $$
{% endraw %}
## 结构  
![Ncell.png](https://upload.wikimedia.org/wikipedia/commons/thumb/9/97/Ncell.png/300px-Ncell.png)
设有n维输入的单个感知机（如右图示），$a_1$至$a_n$为n维输入向量的各个分量，$w_1$至$w_n$为各个输入分量连接到感知机的权量（或称权值），
b为偏置，f(.)为激活函数（又曰激励函数或传递函数），t为标量输出。输出t的数学描述为：
{% raw %}
$$ t=f(\sum _{i=1}^{n}{{w}_{i}{x}_{i}+b})=f(\mathbf {w} ^{T}\mathbf {x} ) $$
{% endraw %}
## 学习算法
学习算法对于所有的神经元都是一样的，因此下面所有东西都要独立的应用于每个神经元。我们首先定义一些变量：
* x(j)表示n维输入向量中的第j项
* w(j)表示权重向量的第j项
* f(x)表示神经元接受输入x产生的输出
* $ \alpha $是一个常数，符合$ 0<\alpha \leq 1 $（接受率）

更进一步，为了简便我们假定偏置量${\displaystyle b}$等于0。因为一个额外的维${\displaystyle n+1}$维，可以用${\displaystyle x(n+1)=1}$的形式加到输入向量，这样我们就可以用${\displaystyle w(n+1)}$代替偏置量。

感知器的学习通过对所有训练实例进行多次的迭代进行更新的方式来建模。令${\displaystyle D_{m}=\{(x_{1},y_{1}),\dots ,(x_{m},y_{m})\}}$表示一个有${\displaystyle m}$个训练实例的训练集。

每次迭代权重向量以如下方式更新：

对于每个${\displaystyle D_{m}=\{(x_{1},y_{1}),\dots ,(x_{m},y_{m})\}}$中的每个${\displaystyle (x,y)}$对，

${\displaystyle w(j):=w(j)+{\alpha (y-f(x))}{x(j)}\quad (j=1,\ldots ,n)}$
注意这意味着，仅当针对给定训练实例${\displaystyle (x,y)}$产生的输出值${\displaystyle f(x)}$与预期的输出值${\displaystyle y}$不同时，权重向量才会发生改变。

如果存在一个正的常数${\displaystyle \gamma }$ 和权重向量${\displaystyle w}$，对所有的${\displaystyle i}$满足${\displaystyle y_{i}\cdot \left(\langle w,x_{i}\rangle +b\right)>\gamma }$ ，
训练集${\displaystyle D_{m}}$就被叫被做线性分隔的。Novikoff（1962）证明如果训练集是线性分隔的，那么感知器算法可以在有限次迭代后收敛，
错误的数量由${\displaystyle \left({\frac {2R}{\gamma }}\right)^{2}}$限定，其中${\displaystyle R}$为输入向量的最大平均值。

然而，如果训练集不是线性分隔的，那么这个算法则不能确保会收敛。