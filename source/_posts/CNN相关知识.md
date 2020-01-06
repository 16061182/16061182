---
title: CNN相关知识 & 论文阅读笔记
categories:
- 笔记
tags:
- CNN
- 手势识别
- CVPR
---

> 这几天看了几篇CNN相关论文，看的过程中学到了一些新的算法和网络模型，也重温了一下CNN的基础知识。由于我知识水平十分有限，自己总结这些知识难免有疏漏；又看到网上的一些介绍这些知识的博客写得真的不错，因此干脆把这些博客总结在此，希望对各位的学习有所帮助。

# 一些算法和模型

[概率图模型(Probabilistic Graphical Model)链接1](https://blog.csdn.net/qq_17109251/article/details/82823279)    [链接2](https://mp.weixin.qq.com/s?src=3&timestamp=1578313401&ver=1&signature=gNkHjxyIfDfLuuR8Vmxxt4Q-Lqz0a2MHtWDTW807L*N15FhZK-Ka1BP49Hgd8RYz5IFh2*UTseaG8za6Ts2wjFB4IFfExc8qPz*xbUwAKq5cvUghUhlqDkhU0fZnAYaFTS3oNZ4ADtgRmBfx1iumi1DKyBHxpVYCLnEonur*foE=)

《Convolutional Pose Machines》这篇文章的方法的特色和优势之一就是没有使用图模型

[非极大值抑制(Non-Maximum Suppression)](https://www.jianshu.com/p/d452b5615850) 

《Realtime Multi-Person 2D Pose Estimation using Part Afﬁnity Fields》2.2最末：用于确定候选关节点的位置

[匈牙利算法(Hungarian algorithm)](https://blog.csdn.net/dark_scope/article/details/8880547)

《Realtime Multi-Person 2D Pose Estimation using Part Afﬁnity Fields》2.4式13、14下方：最优匹配

[上采样方法(upsampling)](https://blog.csdn.net/qq_27871973/article/details/82973048)

《3D Hand Shape and Pose Estimation from a Single RGB Image》1、4.1：相当于最大池化的逆

[堆叠沙漏网络(stacked hourglass network)](https://blog.csdn.net/wangzi371312/article/details/81174452)

《3D Hand Shape and Pose Estimation from a Single RGB Image》4.1：从初始图像生成2D热点图

[残差网络(Residual Networks, ResNets)](https://www.cnblogs.com/wuliytTaotao/archive/2018/09/15/9560205.html)

《3D Hand Shape and Pose Estimation from a Single RGB Image》4.1：根据2D热点和feature maps生成latent feature vector，作为Graph CNN的输入

[图神经网络(Graph Neural Network, GNN)链接1](https://www.jiqizhixin.com/articles/2019-01-07-8)    [链接2](https://blog.csdn.net/tmb8z9vdm66wh68vx1/article/details/85961396)

《3D Hand Shape and Pose Estimation from a Single RGB Image》

[骨骼蒙皮动画算法(Linear Blending Skinning)](https://www.cnblogs.com/shushen/p/5987280.html)

《3D Hand Shape and Pose from Images in the Wild》

# 基础知识

[神经网络中的各种优化方法](https://blog.csdn.net/autocyz/article/details/83114245)

[详解CNN感受野](https://www.jianshu.com/p/9305d31962d8)

[如何解决数据不平衡问题](https://www.cnblogs.com/charlotte77/p/10455900.html)

[目标函数、损失函数和代价函数](https://blog.csdn.net/qq_28448117/article/details/79199835)

> ”f(X)关于训练集的平均损失称作**经验风险**(empirical risk)······大白话说就是它的函数太复杂了，都有四次方了，这就引出了下面的概念，我们不仅要让经验风险最小化，还要让**结构风险**最小化。“

[正则化](https://blog.csdn.net/charles_thegod/article/details/83588212)

> ”我们从前面的图形可以看出，正是那些高次项导致了过拟合的产生，所以如果我们能让这些高次项的系数接近于0的话，我们就能很好的拟合了。“

[主成分分析PCA(principal component analysis)](https://segmentfault.com/a/1190000015332397)

# 论文下载(来自arXiv)

[《Convolutional Pose Machines》](http://xxx.itp.ac.cn/pdf/1602.00134.pdf)

[《Realtime Multi-Person 2D Pose Estimation using Part Afﬁnity Fields》](http://xxx.itp.ac.cn/pdf/1611.08050.pdf)

[《3D Hand Shape and Pose Estimation from a Single RGB Image》](http://xxx.itp.ac.cn/pdf/1903.00812.pdf)

[《3D Hand Shape and Pose from Images in the Wild》](http://xxx.itp.ac.cn/pdf/1902.03451.pdf)

从arXiv上下载论文太慢？可以按照[这篇文章](https://blog.csdn.net/seasermy/article/details/95176357)介绍的方法，使用中科院的arXiv镜像，具体方法是把域名里的**https://arxiv.org**替换成**http://xxx.itp.ac.cn**