---
layout: post
title: 设计模式(二) 工厂方法模式
tags:
- factory method mode
categories:
- Design_Patterns
description: 使用了简单工厂方法的火锅店运行稳定 但是也是存在问题的 因为客人越来越挑剔 需要更多的口味 每次在火锅工厂机器上新添加一个种类的火锅 我都需要请到小王 让他来拆开机器 添加新的材料 如 刀头 什么的 因为切竹鼠用的刀和切螃蟹的刀是不一样的 然后还得编程序 总之很麻烦 而且每次弄完之后 我还得请小王吃个饭喝个酒什么的.....
---


# 设计模式(二) 工厂方法模式

## 1. 股东加入

使用了简单工厂方法的火锅店运行稳定 但是也是存在问题的 因为客人越来越挑剔 需要更多的口味 每次在火锅工厂机器上新添加一个种类的火锅 我都需要请到小王 让他来拆开机器 添加新的材料 如 刀头 什么的 因为切竹鼠用的刀和切螃蟹的刀是不一样的 然后还得编程序 总之很麻烦 而且每次弄完之后 我还得请小王吃个饭喝个酒什么的.....

虽然麻烦点 但是就最近的状况来看 我的火锅工厂明显不能胜任了

由于火锅店生意很好 也得到了几个股东的投资 并且决定开设分店 四川的分店 江西的分店 广东的分店.....开设分店的计划推上日程 我这边的火锅工厂必须做出改变 我已经受够了 每次拆开机器 添加工具...........受够了这些繁琐的操作 而且让客人在牛肉火锅中吃出海鲜的味道 确实也不妥

### 简单工厂的缺点

很明显简单工厂是存在不足的 而且开分店需要迎合当地消费者的口味推出不同地方口味的火锅 也就是添加了新逻辑  比如四川爱吃麻辣 江西爱吃纯辣 广东不爱辣....... 大公司都是这么做的 比如肯德基 美国人饮食不健康爱吃肉 中国人饮食健康爱吃蔬菜而且不暴饮暴食 所以以同样的价格 我们能买到更健康的汉堡   再比如联想 为了发展中国品牌打入美国市场 采取降价策略..........

如果我的火锅工厂不作出改变的话 他将会是这样:
```java
public class HuoguoFactory{
	private String factoryName;
  public Huoguo createHuoguo(String name){	//拿到火锅的方法
    Huoguo huoguo = null;
    if(factoryName.equals("sichuan")){
    	if(name.equals("sichuanBeffHuoguo")){
      	 huoguo = new BeffHuoguo();
    	}else if(name.equals("sichuanLambHuoguo")){
     	  huoguo = new LambHuoguo();
    	}else if(name.equals("sichuanBambooRatHuoguo")){
      	 huoguo = new BambooRatHuoguo();
    	}
    }
    
    if(factoryName.equals("jiangxi")){
    	if(name.equals("jiangxiBeffHuoguo")){
      	 huoguo = new BeffHuoguo();
    	}else if(name.equals("jiangxiLambHuoguo")){
     	  huoguo = new LambHuoguo();
    	}else if(name.equals("jiangxiBambooRatHuoguo")){
      	 huoguo = new BambooRatHuoguo();
    	}
    }
    ......
    return huoguo;
  }
  HuoguoFactory(String factoryName){
  	this.factoryName=factoryName;
  }
}
```
如果火锅的种类很多,所有的判断都在工厂对象中 业务代码会很多很多 难以管理 耦合高 而且每次增加 删除 修改等操作都需要打开工厂  违反了设计准则五:**类应该对扩展开放,对修改关闭**

所以我们必须引入新方法
## 2. 工厂方法模式
### 标准的官方解释:
​		**定义了一个创建对象的接口,但由子类决定实例化的类是哪一个类,工厂方法让类把实例推移到了子类**

说这么多简单点解释就是 以前的火锅工厂太耦合了 事情太多了 为了对它进行解耦合 将他抽离出来

流程图如下:	按道理我们的需要将MyStore抽离出来的 但是由于他们只是地点不一样 其他的都是一样的 所以我们用同一个类     菱形为接口

<div class="mermaid">
graph RL;
shop[MyStore<br/>1.优秀的管理方法];
Factory{Factory};
Factory-->shop;
id[BeefHuoguoFactory]-.实现.->Factory;
id1[LambHuoguoFactory]-.实现.->Factory;
id2[BambooRatHuoguoFactory]-.实现.->Factory;
id3[.....Factory]-.实现.->Factory;

abstract((Huoguo<br/>1.加油方法<br/>2.加调料方法<br/>3.加热方法))
abstract-.继承.-idq[BeefHuoguo];
abstract-.继承.-idq1[LambHuoguo];
abstract-.继承.-idq2[BambooRatHuoguo];
abstract-.继承.-idq3[.....];
	
	idq--创建-->id;
	idq1--创建-->id1;
	idq2--创建-->id2;
	idq3--创建-->id3;
</div>

这就是工厂方法模式了 为了实现火锅工厂的解耦合 我就为每一个火锅类创建一个火锅工厂 现在毕竟有大股东的加入财大气粗 有变化 就变化对应的工厂类或火锅类就可以了 逻辑就被分离出去了 分离到哪里去了呢? 分离到使用者了 你需要那种产品就选择那种工厂就好了

### 不同的观点 平行的类层级:

怎么平行了? 这样看不就平行了吗

<div class="mermaid">
graph RL;
Factory{Factory};
id[BeefHuoguoFactory]-.实现.->Factory;
id1[LambHuoguoFactory]-.实现.->Factory;
id2[BambooRatHuoguoFactory]-.实现.->Factory;
id3[.....Factory]-.实现.->Factory;

abstract((Huoguo<br/>1.加油方法<br/>2.加调料方法<br/>3.加热方法))
idq[BeefHuoguo]-.继承.-abstract;
idq1[LambHuoguo]-.继承.-abstract;
idq2[BambooRatHuoguo]-.继承.-abstract;
idq3[.....]-.继承.-abstract;
</div>


是不是两个平行的类层级?

产品类对应创建者工厂类;

## 3. 回到我的火锅帝国

思想有了 现在怎么运用思想到实际中来? 我们需要分析变化

将所有的火锅产品都运用一个工厂类 明显是不实际的 因为不光涉及菜品种类 还涉及口味

分析一下 菜品种类需要变动吗? 经过我们股东的讨论认为 不需要太多变动了 毕竟火锅店已经运营了有一会了 而且连竹鼠火锅都推出了 还会有比这个还刁钻的吗?

所以我们主要的变化还是在不同地域的口味上 四川爱吃麻 江西喜欢纯辣 广东以清汤涮为主......这是变化

而且我们需要把工厂放进店面(店面成为工厂实体类或者内部维护一个对应的工厂实体类)

至于逻辑部分 也就是客人选择那种地域口味的火锅 这层逻辑 我们完全的交给客人了 我们可不提供配送服务 比如长沙的小伙想带小姑凉吃到正宗的江西火锅 不好意思 请来到我们南昌总店来品尝

现在的逻辑图如下:

<div class="mermaid">
graph RL;
shop[MyStore<br/>1.优秀的管理方法];
	id[JiangxiStore<br/>HuoGuo<br/>1.纯辣的操作方法]-->shop;
	id2[HuNanStore<br/>HuoGuo<br/>1.麻辣的操作方法]-->shop;
	id3[GuangDongStore<br/>HuoGuo<br/>1.清汤的操作方法]-->shop;
	
	abstract((Huoguo<br/>1.加油方法<br/>2.加调料方法<br/>3.加热方法))
idq[BeefHuoguo]-.继承.-abstract;
idq1[LambHuoguo]-.继承.-abstract;
idq2[BambooRatHuoguo]-.继承.-abstract;
idq3[.....]-.继承.-abstract;

abstract1((Huoguo<br/>1.加油方法<br/>2.加调料方法<br/>3.加热方法))
idqq[BeefHuoguo]-.继承.-abstract1;
idqq1[LambHuoguo]-.继承.-abstract1;
idqq2[BambooRatHuoguo]-.继承.-abstract1;
idqq3[.....]-.继承.-abstract1;

abstract2((Huoguo<br/>1.加油方法<br/>2.加调料方法<br/>3.加热方法))
idqqq[BeefHuoguo]-.继承.-abstract2;
idqqq1[LambHuoguo]-.继承.-abstract2;
idqqq2[BambooRatHuoguo]-.继承.-abstract2;
idqqq3[.....]-.继承.-abstract2;

abstract-->id;
abstract1-->id2;
abstract2-->id3;
</div>

这就是我的火锅帝国继承体系

## 4. 总结

由于分离了工厂,当有不同的产品时需要建不同的工厂,将一部分逻辑移到客户端,体现了创建和选择的分离 如果有变化只需要修改工厂实体类,或者修改客户端,解决了简单工厂的开闭问题;



## 5. 多谈一下 依赖倒置原则

**要依赖抽象,不要依赖具体类 就是 程序要依赖于抽象接口，不要依赖于具体实现**

如果依赖具体实现 上层调用下层，上层依赖于下层 一旦改变一部分 对应的其他层必须要改变 那我分层干哈 ? ?

如果我的火锅店都直接依赖所有的火锅类 那我的火锅店中将有很多new火锅方法 如果有一天 火锅被实锤了 有害健康(其实已经被锤烂了) 我转手不干火锅生意了 改去做泡泡鱼

如果直接依赖火锅类 那我就需要改店面代码 如果庞大的话还不如重新开发

如果直接依赖抽象的话 改下传入的抽象类型就可以了 改下方法就可以了 (方法是肯定要改的 毕竟泡泡鱼和火锅做法不同)

### 倒置

至于倒置怎么个倒置? 说说我的理解吧

照我例子  从高层组件开始思考也就是火锅店 我怎么构建我的体系🤔 我首先需要想 火锅店的管理 再到 火锅的制作 需要容器 需要加油 加作料 需要加热 搅拌 还得为不同的地方设计不同的口味 四川火锅这样new 江西火锅要多加辣 ...…..从高层组件(火锅店类)想到底层组件(火锅类) 思路顺置了吧

倒置下思路 不从火锅店开始 先从火锅开始 从火锅的抽象开始  火锅相同的地方设计成一个抽象类 没有就设计成一个接口.....然后他的子类.....好了 火锅的设计过程我心里大致有数了	抽象出了火锅	我现在开始设计我的火锅店了  怎么管理......而且无论用那种工厂 都是在运用火锅的抽象 不用再去理会火锅类了 思想从底层到高层了吧 而且依赖的是抽象 不是具体类 


