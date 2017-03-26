##面向对象的三大特征
我们知道，面向对象有三大特征，分别是：

 - 封装
 - 继承
 - 多态
##封装与继承
###封装
因为对象都对自己负责，所以，对象的很多东西都不需要或不可以暴露给其他对象。

比如：

 - 小明不需要将所有的信息告诉别人；
 - 手机不能不封装而把CPU、内存卡等等都暴露给用户，这太危险了(如下图)。

![image_1bbtpe96d1it014n31bfs68vt9g9.png-2669.5kB][1]

封装解决了数据的安全性，内在也体现了**‘每个对象都对自己负责’**。

###继承
继承，没什么好说的，主要是实现了代码的复用。

但说到这里，我们知道实现代码的复用，有两种方式，一种是组合、一种是继承。

先给大家抛出一个问题：“什么时候该用组合？什么时候该用继承呢？”

这个问题大家先想想，我们以后再讨论。

##重头戏·多态
###定义
对于多态，我们先下一个定义：

> 同一个操作，作用于不同的对象，会产生不同的结果。

说白了，就是一个相同的指令发出，不同的对象会对这个指令有不同的反应，所以称为多态。

###举个栗子
比如，我们有2个对象，分别是 word、excel。
我们使用相同的操作 ```Ctrl+N```。

相同的操作:
对于word是新建word文档;
对于excel是新建excel表格。

###多态有什么好处
多态最大的好处可以用2个词语来概括：**“灵活”、“解耦”**。

耦合度的意思是模块与模块之间、代码与代码之间的关联度。
紧耦合也就是他们之间的关联度大，这样的代码是很难维护的，很容易出bug的。出现一个bug，其他bug很可能像滚雪球一样增长。

我们经常说：“**要面向接口编程，而不是面向实现编程**”。

多态性，也就要求我们面向接口编程。
不同的对象，相同的接口，但因为多态，有了不同的实现。

这样面向接口编程，就降低了耦合度，很灵活。

###PHP中的多态
talk is cheap,show me your code
```
<?php
abstract class Animal{
    //说话的方法
    abstract public function say();
    //吃的方法
    public function eat(){
        echo "eating food...";
    }
}

//Dog子类继承Animal抽象类
class Dog extends Animal {
    public function say(){
        echo "Dog say wangwang\n";
    }
}

//Cat子类继承Animal抽象类
class Cat extends Animal {
    public function say(){
        echo "Cat say miaomiao\n";
    }
}

//test function
function work(Animal $obj){
    if($obj instanceof Animal){
        $obj->say();
    }else{
        echo "sorry.It's wrong";
    }
}

work(new Cat()); //Cat say miaomiao
work(new Dog()); //Dog say wangwang
```

**更多精彩，请关注公众号“聊聊代码”，让我们一起聊聊“左手代码右手诗”的事儿。**

![这里写图片描述](http://img.blog.csdn.net/20170326120350289?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMTUwOTc4MQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


  [1]: http://static.zybuluo.com/ericliu001/17j2y8lf76ounmuzmrpjk6qq/image_1bbtpe96d1it014n31bfs68vt9g9.png