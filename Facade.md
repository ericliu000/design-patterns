
## 流行的MVC架构模式
如今的Web开发，各种框架风起云涌，势如破竹。

从国民第一的ThinkPhp到称霸全球的Laravel，这些框架有一个共同特征，都采用了MVC的架构模式。

![112.jpeg-20.9kB][1]

没有任何意外，王小二的公司用Thinkphp来开发公司的主打产品。

## Get新需求
一天，小二刚到公司，正打算坐下来喝杯茶。

老大走了过来：“小二啊，现在有个新的需求。咱们之前提交订单的模块，需要增加发送邮件的功能，你看看能不能实现？”

小二想了想说：“没问题，最多3天搞定！”

看王小二胸有成竹的样子，老大满意的点了点头。

## 臃肿的Controller
着手开干吧！小二打开熟悉的IDE，找到提交订单模块的Controller。

OMG!不看不知道，一看吓一跳，这个Controller的代码竟然接近2000行。

因为用户提交订单时，会与其他模块进行交互，需要的数据也比较复杂。
只见此Controller，从Model层各种拿数据，然后各种逻辑处理，怪不得代码到了将近2000行。

“哎，这2000行代码，看着就头疼，可让我怎么写啊”...小二叹气道。

“要不再去请教下C哥？”

## MVC的烦恼
小二找到C哥，详细的描述了他的问题。

C哥喝了口水，淡定的说：“这个嘛，我之前也遇到过。”

“您也遇到过，怎么解决的？”

“这个问题，哈哈，姑且就叫MVC的烦恼吧！MVC将View与Model进行了分离解耦，这固然很好，但很多人就将业务逻辑的处理写在了Controller里，导致Controller越来越臃肿，以致最后都无法维护。”

“对对对，您说的太对了，我就经常这样写。”

[图片：臃肿的代码]
![20160825085351234.jpg-88.4kB][2]

## 给Controller减肥
C哥继续说道：其实，Controller不应该处理过多的业务逻辑。给你举两个例子就明白了。

1. 控制器，就像遥控器一样。
你见过遥控器关心电视怎么播放视频吗？没有，遥控器只是发送播放视频的信号，具体的播放视频的细节，遥控器不会关心。

2. 控制器，就像将军一样。
你见过将军亲自为每位士兵配备武器吗？细节部分，将军不必过问，将军的职责是领兵打仗，这叫各司其职，否则就乱了。

说到这里，小二恍然大悟：“听C哥一席话，胜读十年书啊！”

“既然这样，就给Controller减减肥吧。”C哥说到
“是啊，但是怎么减肥呢？”

## 初识Facade外观模式
“我给你讲一种设计模式-外观模式，你就懂了”。
“好啊好啊，洗耳恭听”。

C哥又讲到：

外观模式，提供了统一的接口，用来访问子系统中的一群接口。外观模式定义了一个高层接口，使得子系统更加易用。

也就是说，干一件很复杂的事的时候，你想团队中每个人都花一年半载去学习如何做这件事吗？利用外观模式，我只需要指定一个人去学会这些复杂的步骤，然后我再告诉这个接口人去干就行了。


## Facade外观模式的应用
“如果让你实现上面那个需求，你可能会找到用户提交订单的Controller，然后在Controller里写下面一大堆代码。是不是？”

```
/****文件名：SubmitController.class.php(用户提交模块controller)****/
    
//..............接上...2000行代码..............//

    //获取用户邮箱
    public function get_user_email($uid){
        return new User()->get_user_email($uid);
    }
    //获取要发送给用户的内容
    public function get_email_content($uid){
        return new Email()->get_email_content($uid);
    }
    //发送邮件
    public function send_email($email,$content){
        return new Email()->send_email($email,$content);
    }
    
    //用户提交订单触发的方法
    public function submit(){
        $email=$this->get_user_email($uid);
        $content=$this->get_email_content($uid);
        $this->send_email($email,$content);
    }
```

“对对对，我会这么写”。

"其实你用的ThinkPhp，有一层叫Logic层，关于业务逻辑处理的部分，你可以写在Logic层里。这样，Controller层就变得很轻量了，好维护了。"

```
/****文件名：SendEmailFacadeLogic.class.php(发送邮件Logic)****/
    
    //获取用户邮箱
    private function get_user_email($uid){
        return new User()->get_user_email($uid);
    }
    //获取要发送给用户的内容
    private function get_email_content($uid){
        return new Email()->get_email_content($uid);
    }
    //发送邮件
    public function send_email($uid){
        $email=$this->get_user_email($uid);
        $content=$this->get_email_content($uid);
        return new Email()->send_email($email,$content);
    }
```

```
/****文件名：SubmitController.class.php(用户提交模块controller)****/
    
//..............接上...2000行代码..............//

    D('SendEmail','Logic')->send_email($uid);
```

“你看，加了Logic层，业务逻辑都放在Logic里面去处理，Controller是不是瘦了很多呢？Logic层为Controller提供了一个高层的接口用来发送邮件，也就是Facade模式的应用。”

## 加深理解
“小二，明白些了吧？”
“嗯嗯，明白了好多，犹如醍醐灌顶！”

“为了加深你的理解，我给你画个简单的实例图吧”。
“真的吗？太谢谢C哥了”。

![image_1bc4ti5671bba1v88nsj1267ied2s.png-82.3kB][3]

## 恍然大悟
看了C哥画的图，小二小彻小悟了。

“C哥，Facade模式真不错，你看，这样统一成简单的接口后：”

1、降低了系统的耦合度。提交订单的Controller，再也不用与UserController、EmailController等耦合了。现在只需要关心SendEmailFacadeLogic就可以了。
2、并且，用户使用了Facade模式后，有了统一的入口，就很容易监控客户对系统的使用了。就如Thinkphp的单一入口一样。

“嗯嗯。小二真聪明，确实是这样。”

更多精彩，请关注公众号“聊聊代码”，让我们一起聊聊“左手代码右手诗”的事儿。
![miaoshu][4]

  [1]: http://static.zybuluo.com/ericliu001/kvcme8excjrvk5ga481bfrxk/112.jpeg
  [2]: http://static.zybuluo.com/ericliu001/6o56dmj0m76dm2ic3r5js6ez/20160825085351234.jpg
  [3]: http://static.zybuluo.com/ericliu001/1wfb2lnfpb9xdtm4co59nsyk/image_1bc4ti5671bba1v88nsj1267ied2s.png
  [4]: https://sfault-image.b0.upaiyun.com/426/377/4263778125-58d283201b083_articlex