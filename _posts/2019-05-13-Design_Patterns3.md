---
layout: post
title: 设计模式(三) 抽象工厂模式
tags:
- Abstract Factory Pattern
categories:
- Design_Patterns
description: 我运用了工厂方法模式 建设了我的火锅帝国 但是仔细想一想 火锅工厂方法模式还是有点脱离实际 我们从始至终都把火锅当成一个不可分割的整体 但是仔细想想火锅是一个整体吗? 各种配料 各种这些配料的供应商 为了做大做强 我们需要自己的子公司 自己的配料公司 由他们给我提供优质的配料 例如 花椒 辣椒 地沟…不..优质菜油 酱料........
---



# 设计模式(三) 抽象工厂模式

## 1. 绕不开的火锅

我运用了工厂方法模式 建设了我的火锅帝国 但是仔细想一想 火锅工厂方法模式还是有点脱离实际

我们从始至终都把火锅当成一个不可分割的整体 但是仔细想想火锅是一个整体吗? 各种配料 各种这些配料的供应商 为了做大做强 我们需要自己的子公司 自己的配料公司 由他们给我提供优质的配料 例如 花椒 辣椒 地沟…不..优质菜油 酱料........而且还要分地域性的 各地有各地的口味.....有的菜需要用嫩辣椒 有的要用老辣椒 有的用辣椒壳 有的用辣椒籽.........你怎么半? ? ?是不是觉得头大😂

如果放大这个细节 会发现 我们以前的模式貌似都不适用了 因为火锅对应着一个产品族:

<div class="mermaid">
graph BT;
shop[火锅类<br/>1.花椒类<br/>2辣椒类<br/>3菜油类]
	id[1花椒类]-->shop;
	id2[2辣椒类]-->shop;
	id3[3菜油类]-->shop;
	id5[.....]-->shop;
</div>

火锅是由多个产品组成的一个产品 ! ! ! !

所以我们前面的火锅都得忘记掉 ! 完全不适用 !

一个小小的火锅其实一点都不小 ! 他后面有一家花椒工厂 地点在成都 从哪里加工花椒 有江西婺源的采集的油菜花 加工成优质菜油 还有 湖南的辣椒 在长沙保存 运输.........一碗小小的火锅聚集了祖国各地的美味啊 都是大自然的馈赠啊  所以我的火锅店运营理念就是 : 我们不生产火锅 , 我们只做大自然的搬运工 ! ! !

好了好了 回过来😂 下面介绍抽象工厂模式
## 2. 抽象工厂模式
照旧先来个官方点的定义 : 提供一个借口,用于创建相关或依赖对象的家族,而不需要明确指定具体类
他是围绕一个超级工厂创建其他工厂。该超级工厂又称为其他工厂的工厂 😂 有点绕 这个源自菜鸟教程

我们的做法就是既然火锅是多个产品组成的 那么我们就抽象出火锅工厂这个接口 用于定义一组相关的产品的获取方法 用不同的具体工厂类实现这个接口

而且生意做大了 店面已经不需要生产火锅了 全部交给工厂就好了 所以店面就是地址不同 进货工厂不同而已

如图:

<div class="mermaid">
graph RL;
shop[MyStore<br/>private HuoguoAbstractFactory<br/>1.优秀的管理方法];
AbstractFactory{HuoguoAbstractFactory<br/>get花椒 get辣椒 get菜油 get其他};
id[JiangxiFactory<br/>get花椒 get辣椒 get菜油 get其他]-.实现.->AbstractFactory;
id1[HuNanFactory<br/>get花椒 get辣椒 get菜油 get其他]-.实现.->AbstractFactory;
id2[GuangDongFactory<br/>get花椒 get辣椒 get菜油 get其他]-.实现.->AbstractFactory;
id3[.....Factory<br/>get花椒 get辣椒 get菜油 get其他]-.实现.->AbstractFactory;
AbstractFactory-->shop;

</div>

材料图:材料还有很多..........

<div class="mermaid">
graph BT;
AbstractFactory{花椒};
id[花椒末]-.实现.->AbstractFactory;
id1[花椒籽]-.实现.->AbstractFactory;
id2[花椒壳]-.实现.->AbstractFactory;
id3[.....]-.实现.->AbstractFactory;

AbstractFactory1{辣椒};
id11[辣椒末]-.实现.->AbstractFactory1;
id22[辣椒籽]-.实现.->AbstractFactory1;
id33[辣椒壳]-.实现.->AbstractFactory1;
id44[.....]-.实现.->AbstractFactory1;
</div>

组合一下图吧 很复杂 但是思路清晰  大概就这样的结构 铺不开

通过这些具体的工厂获取各种材料

<div class="mermaid">
graph BT;
shop[MyStore<br/>private HuoguoAbstractFactory<br/>1.优秀的管理方法];
AbstractFactory{HuoguoAbstractFactory<br/>get花椒 get辣椒 get菜油 get其他};
id[JiangxiFactory<br/>get花椒 get辣椒 get菜油 get其他]-.实现.->AbstractFactory;
id1[HuNanFactory<br/>get花椒 get辣椒 get菜油 get其他]-.实现.->AbstractFactory;
id3[其他实现类]-.实现.->AbstractFactory;
AbstractFactory-->shop;

dm{花椒};
d1[花椒末]-.实现.->dm;
d2[花椒籽]-.实现.->dm;
d3[花椒壳]-.实现.->dm;
d4[.....]-.实现.->dm;

ddm{辣椒};
ddm1[辣椒末]-.实现.->ddm;
ddm2[辣椒籽]-.实现.->ddm;
ddm3[辣椒壳]-.实现.->ddm;
ddm4[.....]-.实现.->ddm;

other{其他原料};


dm-->id;
ddm-->id;
other-->id
</div>

这就是抽象工厂模式 它主要是生产一个系列的产品  工厂方法模式 只能生产一个产品

他能对产品族进行很好的解耦合 想想看 如果我开一家武汉店的火锅 然后调查他们的口味 接下来就是积木了 当然如果要扩展接口的话 虽然没人喜欢这么做 因为这是很严重的问题 必须重写全部下面的实现 出现这样的情况 请让你的设计或者产品经理请你来我店里吃火锅吧 

## 3. 总结

抽象工厂方法是针对一个产品族的设计模式 他能很方便的交换一个产品族 实现了很大程度上的分离 和解耦合

但是如果扩展接口的话 会非常麻烦 所以一个良好的设计非常重要

而且抽象工厂模式内部通常会使用工厂模式 或者使用简单工厂模式 或者使用更多的方案 毕竟他是个更大的接口 怎么实现这个模式还得看具体的场景



到这里我的工厂模式就结束了