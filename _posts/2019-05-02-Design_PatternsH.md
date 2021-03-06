---
layout: post
title: 设计模式(引子) 我为什么学习设计模式
tags:
- Design_Patterns
categories:
- Design_Patterns
description: 首先我想谈谈我对编程的理解 在我读大学之前,对于编程我是没概念的,我知道他是一堆计算机指令 ,一堆正常人都看不懂懂得天书 ,也对他们表示钦佩 .现在 这么久了,我对编程,对计算机世界有了自己的一点点理解
---



# 设计模式(引子) 我为什么学习设计模式


### 我对编程的理解

happy Birthday!   happy Birthday!  🎂 继续努力 继续努力 嘻嘻☺️ 

首先我想谈谈我对编程的理解 在我读大学之前,对于编程我是没概念的,我知道他是一堆计算机指令 ,一堆正常人都看不懂懂得天书 ,也对他们表示钦佩 .现在 这么久了,我对编程,对计算机世界有了自己的一点点理解!

#### 1. 计算机世界

渐渐的学习了一些基础知识 数据结构哦 算法 javase……我渐渐的发现 他们都来源于我们的生活——我们人类的世界 我感觉计算机世界 ==就是我们现实生活的映射==	生活处处有编程    所有计算机的问题 我觉得都可以在现实生活中找到最合理最自然的解决方法 这是人类几万年积累的知识库 

#### 2. 我的第一个有意思的程序

- 上了大学 第一个半学期学习了javase的基础知识, 好奇心下 我决定自己写个toy code (玩具代码),我想自己实现一个txt文本的**加密**功能-----也是那会我能想到,而且我能实现的功能 于是我开始思考🤔	文本加密 就是将明文弄成密文就可以实现了 用流一个一个读汉字然后一个一个操作........但是加密算法怎么实现?🤔	我知道java 的char类型和int类型可以互相转换,我只要将一个一个汉字转换成int类型 然后数值加一 然后在转换成char 这样就实现了加密 解密的时候只要减一就可以了

- 代码码完之后 功能可以实现了 ,但是我也发现了他的问题 就是我加密后 任何人都可以解密 我只能加密多次 但是我加密3次 他只需要解密三次就可以了 这是个问题 需要解决 于是我又想方法  都加一肯定是不行的 那我让让他随机加减数字 记录这些数字 然后生成一个密钥文件 解密的时候 用这个密钥文件解密就可以了

- 虽然我觉得这个很完美 但是还是有些很严重的问题,如果有个家伙恶意的破坏我的文件 他把加密文件多次加密 删除密钥 或者修改密文...........这样想的话问题很多了 需求总是在不断变化 改代码将成为日常.........

#### 3. 代码帮我挣更多钱

- 大二暑假开始兼职 找到一个很机械的工作 帮人扫描pdf 就是帮房产局扫描各种资料到电脑,每天的话可以挣到100多块呢 但是我 作为一个学过编程基础的人 我觉得这一系列鼠标操作让人厌烦

- 首先 我需要对这些不同类型的资料创建对应的文件夹 然后修改文件夹的名字 然后把扫描的文件放进文件夹...........我觉得可以通过io简化这个操作 于是我开始挑灯夜战 第一天晚上就弄完了一个java程序 他就长这样:

  ![image-20190428132430447]({{site.url}}/mkpicture/image-20190428132430447.png)

排版有些问题 因为以前是win8 现在是OS X

这样我只需要创建一个文件夹用来放扫描文件 然后创建客户文件夹 选择pdf的类别 点击移动 他就会自己创建对应的文件夹 并且移动pdf文件 显示操作信息(后来我知道有个东西叫日志)

就这样我的效率提高了很多因为最费时间的创建文件夹的工作被简化了! 主管也知道了 决定"收购"我的"产品" 而且给我加工资 ! 我第一次体会到知识就是力量 知识就是金钱 …..

但是好景不长 工作并不是一成不变的.....今天多了个出让说明的分类 过几天又多了个身份证明 下周有多了一个规划通知......每次我都要更改我的代码 通篇看一遍我写了什么鬼东西,东西一多 整个程序变得臃肿 就像一坨意大利面一样胡乱不堪.....

#### 4. 总结

- 从那一天开始 我体会到了 程序并不是只是为了实现功能 后期的需求变更 代码修改 维护  反而比开发花更多时间 所以好的程序设计非常重要 不然维护将是噩梦
- 就我上面的程序来说 我觉得他就像一台mac笔记本 出了一点问题 我需要全面了解mac的构造 什么地方干什么的 什么地方能拆 整个产品集成度很高 而且下次维修记忆力不好的话 这些步骤又需要来一次!
- 反而 如果我的程序想一台小轿车! 车胎爆了车子不能走了 都不用动脑子 换个轮胎就可以了! 我不需要了解整个汽车各个系统的功能 我只需要关心他的一部分——车胎那一部分! 后来我知道一个词来描述联系的紧密程度——**耦合**



#### 5. 体会

程序必须要可维护 而且各个系统应该要解耦合 这个在敲代码之前就要设计好 不然出现问题需要重头再来 我们必须要为 **低耦合,高内聚** 而努力.

所以我接触到了设计模式 这个大家都知道的设计 程序开发和程序设计者通用的知识   知道了"四人帮"    拥有了一本很优秀的书——<head frist 设计模式> 希望在以后的开发学习中——设计模式 这些前任程序员遭遇过的问题 以及他们的总结的解决方法和设计思想 能让我少走些弯路 更好的理解设计思想 也不用大费周章的和同事解释我的设计, 直接简单的一句话——我的这个模块使用了工厂模式 !