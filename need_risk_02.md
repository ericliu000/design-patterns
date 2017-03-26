##0x1 原文再续，书接上回
上回说到，C哥凭借自己多年的编码经验，欲传授王小二绝世武功。
让我们书接上回。
##0x2 来源于生活中的实例
看着王小二求知若渴的眼神，C哥开始对小二循循善诱。

“小二啊，我们假设一个场景：假设你是一名讲师，对于上完你课程的人，你要确保接下来，每个人都知道他们下一节课去哪上。你如何去做呢？”

“嗯...我会在教室门口贴一张课表。课表上标明所有的课程以及课程对应的教室。让学生们自己根据课表去找就行了。”
![image_1bbqd04m5131126t114n1bnm1n4r9.png-349.6kB][2]

“不错！小二很聪明嘛。但是如果把这个场景转换为程序实现，你起初可能就不会这样设计了”。

“为什么？”小二睁大眼睛问道。

“因为面对需求，你首先想到的是过程化的解决办法。比如在你设计发送消息的需求的时候，就是典型的过程化的思维模式。上面那个讲师的场景，你转换成程序可能会这么做：

 1. 获得课堂上每个人的名单;
 2. 对于名单上的每个人：
    a.查找他的下一节课程;
    b.查找他的下一节课程的地点;
    c.告诉他去哪里上下一节课。

为了实现上面的过程，你可能需要：
 1. 获得课堂上每个人名单的方法;
 2. 获得每个人课表的方法;
 3. 获得每个课程对应的教室的方法;
 4. 告诉学生去相应教室上课的方法;
 5. 一个控制程序为每个人做需要的步骤。”
 
王小二沉思了一会，若有所思的点点头：“嗯，确实会这么做”。

##0x3 趁热打铁·责任的转移
![image_1bbqe1c61bmj36k1jj791n1kjam.png-251.5kB][3]

“小二啊，上面我们说了两种解决办法。你觉得这两种解决办法哪种更好些呢？”C哥问道。

“当然是第一种了，现实生活中我可不会傻到自己挨个去查学生的课表，地点，然后挨个告诉学生，那多累啊。”

“是啊，肯定是第一种解决办法好。其实，你仔细想想，这两种解决方式，最大的不同点是哪里？”

“嗯...想不出来。”

“最大的不同点，是**责任的转移**。你看第一种解决办法，你只需要把课表张贴出来，学生自己去查询课程、教室就行了。完成这件事情，既有老师的责任，也有学生的责任。而第二种方法，从头到尾都需要老师去做，责任都在老师身上。”

“每个人的责任边界划分的很清楚，每个人都对自己的事情负责，各司其职。这也就是我们常讲的低耦合。这样的代码很好维护、扩展，当需求有所改变时，我们就能很好的去应对。你好好想想是不是...”
##0x4 发送消息的重新设计
C哥提到，一种方式是面向过程，一种方式是面向对象。
两种方式最大的不同就是责任的转移。

王小二若有所悟，决定重新设计下发送消息的那个需求。

按照小二的想法，发送消息需要如下类(或实体)，才能实现责任的界定、转移。从而将程序解耦。

小二先把类图设计了出来。
![image_1bbqkel7sksu8sb1998dr5166l34.png-18.9kB][4]

设计完毕，顿时觉得思路清晰了好多。

用面向对象的方式去实现这个需求，如何实现呢？

 1. 开始控制程序;
 2. 对相应的vip用户做初始化;
 3. 告诉相应的vip用户，发送信息;
 4. 每个vip用户:
    a.确定自己要发送什么类型的消息(短信、微信、email...)
    b.发送消息

如此，就实现了解耦。真是能量满满。

##0x5 再也不怕需求变了
根据上面的设计，小二又用相应的代码进行了实现。
“需求爱咋变咋变，这次不怕了，哈哈”，小二窃喜道。

比如，现在需求变化了。

产品经理说:"需要给年Vip用户发送短信、邮件。其他Vip用户不变"。

王小二想到：“哈哈哈哈哈，需求随便改，我终于不再需要改那一大坨代码了，我只需要改年Vip用户的类就可以了。”

如图，需要改一个地方，其他地方不会有任何影响。
![image_1bbqkh45435d1rjs1apiv8nvr83h.png-23.5kB][5]

看，解耦之后，就是这么的灵活、有魅力。

**更多精彩，请关注公众号“聊聊代码”，让我们一起聊聊“左手代码右手诗”的事儿。**
![这里写图片描述](http://img.blog.csdn.net/20170326120133974?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMTUwOTc4MQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


  [1]: https://segmentfault.com/a/1190000008711877
  [2]: http://static.zybuluo.com/ericliu001/4rrnuftrqlgvk3zer0tk631f/image_1bbqd04m5131126t114n1bnm1n4r9.png
  [3]: http://static.zybuluo.com/ericliu001/7repmbqn25txi2p0xgue3pby/image_1bbqe1c61bmj36k1jj791n1kjam.png
  [4]: http://static.zybuluo.com/ericliu001/2llo3nyy3rso358g2bh47lwl/image_1bbqkel7sksu8sb1998dr5166l34.png
  [5]: http://static.zybuluo.com/ericliu001/3f47frj8hc3n8ff8wclg416y/image_1bbqkh45435d1rjs1apiv8nvr83h.png
  [6]: /img/bVK3YX