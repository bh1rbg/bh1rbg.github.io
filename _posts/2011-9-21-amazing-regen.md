---
layout: post
title: "Amazing Regen"
excerpt_separator: <!--more-->
---

再生接收机由来已久, 再生接收机的专利诞生迄今已经100多年了.    美国发明家, 电子工程师, Edwin Howard Armstrong 是一个传奇人物, 他申请再生接收机的时候, 还是一个大三的学生.(1914年)

##  再生接收机框图
<img src="{{site.baseurl}}/../images/regen-block.png"  class="center"  width="400"/>
<div align="center"> 再生接收机框图  </div>


<!--more-->

振荡器无处不在, 他是放大器的敌人,  是接收计的核心. 再生接收机是一个可控的振荡器, 总是接近震荡, 而又还未震荡.  任何一个振荡器, 都可能是一个再生接收机.  


## 第一次制作再生接收计

2011/9/21

如果没有记错, 最早接触再生接收机, 肯定是在 <中学科技> <无线电> 这类杂志.  一个中波收音机总是试图控制好再生, 免得他发出刺耳的啸叫. 

但是  ARRL (美国业余无线电联盟) 铺天盖地的资料中, 再生收音机即便是变成一个振荡器, 也是有无穷乐趣,  不仅能接收中波, 在短波, 再生接收机更是能接收 AM, SSB, CW 各类信号. 

其中ARRL 着重介绍的一个再生机, 是 N1TEV 同志 设计的 "初学者再生机".

<img src="{{site.baseurl}}/images/regen-arrl-n1tev.jpg" class="center"  width="600"/>
<div align="center">  N1TEV 系列高性能接收机  初学者篇  </div> 

这个给初学者的再生接收计看起来一点都不简单. 不过, 这么做是有道理的, 至少供电稳定, 退耦合有效. 复杂的东西不一定就困难.  所以, 话不多说, 做好再论.

| <img src="{{site.baseurl}}/images/regen-arrl-proto.jpg" class="center" /> | <img src="{{site.baseurl}}/images/regen-proto-ant.jpg" class="center" /> |
|  原型验证机  | 天线  |

最大的旋扭是调台的, 覆盖短波 3-10 Mhz. 做完就知道了, 没有大减速比的空气电容, 这样调台是极度困难的, 太不容易正好调整到一个广播台了.

天线是给接收 CW (电报) 信号用的, 拉杆天线长度大约 2 米, 电路地回路还有另一根 3-5米长的导线从窗户垂下去.   当然要接收到 电报信号,  再生控制要开大, 开到正好发生震荡 -- 此时扬声器会有一声响声.  如响起来不停了,  那就是发生音频震荡了, 就得治一治了.


## 再次制作再生机

2012/7/24

时光匆匆, 一年就过去了.  做一次再生机, 自然玩不明白.  这次再来. 看能不能做到一个壳子里.  同时也换一个电路试试. 

 这次我看中了 NA5N 的 "pipsqueak" 再生机. 这名字起得非常低调, 意为 "微不足道" 的再生机. 可以看到这个再生机是 ARRL 初学者 的延伸机型. 增加了一个音频放大级, 看起来很强大的样子. 

<img src="{{site.baseurl}}/images/regen-na5n-pipsqueak.gif" class="center" />

自然不能照抄, 在给定点路上动点手脚, 改一改, 修修, 最能锻炼技术, 磨练意志了.  主要是把LM386换成了更弱的双管音频放大器.   事后诸葛一下: 当时做这个音频放大器,  并非已经知道了它的全部特性, 只是新鲜而已.

<img src="{{site.baseurl}}/images/regen-my-pipsqueak.jpg" class="center" />


## 困难的装壳

<img src="{{site.baseurl}}/images/regen-2012-internal.jpg" class="center" />

给接收计制作外壳中, 犯了许多错误. 

* 壳子是先开好孔, 再制作电路的, 除非做过多次, 否则这样就托大了. 一定要先做电路.
* 可调电容的接线自作聪明的用了屏蔽线, 以为可以抗干扰. 问题是这段线有60 皮法 的电容,  赶紧拆了, 下不为例.
* 布局纯粹是瞎搞的. 一条线的布局是最好的, 每一级的输入输出朝向都一致, 一字排开才是上策. 
* 同时, 为了良好布局, 不要一开始追求把机器做的很小, 相反, 要尽量大才对 -- 方便调试, 布局合理比小型化重要的多.


<img src="{{site.baseurl}}/images/regen-2012-final.jpg" class="center" width="450" />
<div align="center">  这个 "芯"乱如麻的机器   </div>


## 最后的奋斗

 最终, 通过修改电路, 还是做到了抑制啸叫,  基本可用的程度.  新的电路如下, 主要是添加了许多电容, 进行退耦.

问题是通过示波器发现的, 在音频级, 有许多射频信号存在, 导致无法避免的大回路震荡. 所有的修改几乎都是为了去掉音频中的射频信号.

<img src="{{site.baseurl}}/../images/regen-my-pips-sch.png"  class="center" width="800" />

*   C16,C9, C15 提供 检波器 RF信号 退耦合 
*   增加 C8 到 三极管 T4 , 抑制RF 增益. 
*   C3 增加到 47pF , 这样只覆盖  8.7Mhz  到 11Mhz, 否则调台困难. 
*   采用了变容二极管  BB910 , 这样可以把调台旋扭任意放置, 不受空气电容旋扭的限制.
*    C17 滤除 可变电阻噪音 .
*    R7 改为  4.7k , 增益足够. 

<img src="{{site.baseurl}}/images/regen-2012.jpg" class="center" width="400" />
<div align="center">   最后的样子    </div>
