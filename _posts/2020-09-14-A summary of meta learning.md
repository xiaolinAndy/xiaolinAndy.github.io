---
layout:     post
title:      "A summary of meta learning"
subtitle:   "介绍一下NLP中很火的元学习"
date:       2020-09-14
author:     "Andy"
header-img: "img/post_bg.jpg"
catalog: true
mathjax: true
tags:
    - meta learning
    - NLP
---


<p id = "build"></p>

# Meta Learning

Q：为什么要去做元学习？

A：目的是想更快更好地学习新的任务。

## 定义：

训练集是一些任务(tasks)，在训练过程中，每个样本（任务）的loss是当前模型在该任务测试集上的错误率。随着训练过程的继续，模型在训练集中的任务的loss越来越低，表现越来越好，期望在测试集中的任务上也能有好的表现。

## 概念解析：

### Meta-learning vs Transfer Learning:

- 理论上
  - 迁移学习指具体的学习方法，例如如何利用任务A来帮助任务B
  - 元学习是一种**学习思想**，可以用于提高迁移学习的效率
- 任务上
  - 迁移学习可以在不同任务上做迁移
  - 元学习假定不同任务（训练任务和测试任务）满足同种分布，经常是**不同领域的同一任务**

### Meta-learning vs Multi-task Learning:

- 元学习是一种多任务学习
- 多任务学习侧重于在目标任务上的效果，元学习侧重于在目标任务上的**学习效率**
- 多任务学习对于数据多的任务效果更好，元学习一般对不同任务使用等量的数据
- 多任务学习的任务量不能过多，元学习的任务量越多越好

## 训练方法：

### Learn to Embed：学习样本的表示，使得相同类别的样本具有更加接近的表示

- Siamese Network: 比较两个样本是否属于同一个类别
- Matching Network：根据带标签的数据确定表示函数
- Prototypical Network：利用标签类别信息来表示样本
- Relation Network：利用神经网络学习两个样本的相似性

### **Learn to Fine-tune：学习如何更好地优化模型，使得其在所有任务上都有不错的效果**

- MAML：
  - 对于任务$T_i$，训练更新参数$\theta$，在验证集上得到$loss_i$![formula_1](https://raw.githubusercontent.com/xiaolinAndy/xiaolinAndy.github.io/master/_posts/post_image/2020-09-14-formula_1.png)
  - 对于所有任务，根据$loss_i$优化参数$\theta$![formula_2](https://raw.githubusercontent.com/xiaolinAndy/xiaolinAndy.github.io/master/_posts/post_image/2020-09-14-formula_2.png)
- First-Order MAML:
  - 忽略$\hat{\theta}$到$\theta$的梯度![formula_3](https://raw.githubusercontent.com/xiaolinAndy/xiaolinAndy.github.io/master/_posts/post_image/2020-09-14-formula_3.png)
- Reptile：
  - 在每个任务上训练n次，然后对于更新的参数变化求平均![formula_4](https://raw.githubusercontent.com/xiaolinAndy/xiaolinAndy.github.io/master/_posts/post_image/2020-09-14-formula_4.png)

## 在NLP中的应用：

### 同一个任务

- 一个类别是一个任务
- 一个领域是一个任务

### 多种类型的任务：

- 不同语言的机器翻译
- NLI，文本分类，情感分类等