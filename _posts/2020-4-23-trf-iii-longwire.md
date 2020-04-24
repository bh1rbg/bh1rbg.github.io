---
layout: post
title: "TRF III 长线调谐收音机"
excerpt_separator: <!--more-->
---

最近做完一个成功的矿石机, 一个天线调谐器和一个主调谐器, 算是半拉双调谐. 两者是紧耦合的. 紧接着, 自然就是要接上音频放大器听听TRF的效果. 好事多磨, 每次都有新问题.

<img src="{{site.baseurl}}/images/crystal-dt-receiver.jpg" class="center" width="600" /> 

<!--more-->

## 框图

仅简单的加入一个 LM386 音频放大器, 就能有不错的效果. 

双调谐已经能很不错的隔离短波的冲击, 选择性也可以. 如果没有天调组, 仅有主调谐线圈, 短波的影响将在所难免, 无论哪一种拓扑, 不可避免的多少都会变成短波机, 而不是中波.

<img src="{{site.baseurl}}/images/TRF-longwire-block.png" class="center" />


## LM386

这个LM386模块可以多重用途, 实际上是给积木万用板设计的模块, 用作收音机接收音频放大器也是非常合适. LM386 做接收机的爱好者最爱的芯片, 几乎没有之一.尽管都抱怨它嘶嘶声太重, 吐槽完, 依旧还是用LM386.

这个模块用料是很奢华的, LM386不过2毛钱, 可能都不如一个电阻值钱. 这样很好, 有'价值'的东西, 你不会想在做完后扔掉它.

|<img src="{{site.baseurl}}/images/lm386-photo1.jpg" />|<img src="{{site.baseurl}}/images/lm386-photo2.jpg" />|

LM386手册建议了很多种方法减少接收机噪音, 比如输入RC滤波, 低频提升, bypass电容一定要接等. 这样才是一个完整, 可靠的LM386电路, 大多数爱好者并不在意音质, 仅看重LM386用起来还算简单. 不是最简单的功放, 但是价格, 最高工作电压, 功耗, 都比较合适. 

|<img src="{{site.baseurl}}/images/lm386-sch.png" class="center" />|<img src="{{site.baseurl}}/images/lm386-pcb.png" class="center" />|


## 啄木鸟干扰

传说有一种冷战时期的雷达, 超视距雷达, Duga radar. 其中有一台就建在切尔诺贝利附近. 宏伟壮观, 叹为观止.

<img src="{{site.baseurl}}/images/duga-radar.png" class="center" width="600" />

<img src="{{site.baseurl}}/images/duga-radar-arm.png" class="center" width="600" />

这种雷达开启的时候, 整个短波波段都会听到一种脑仁痛的 哒哒声, 不服可以听听这个效果. 鉴于这个声效, ham亲切的称之为 啄木鸟.

<div align="center">
<iframe src="//player.bilibili.com/player.html?aid=412773729&bvid=BV1SV411o7C5&cid=181288612&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe> </div>

算是幸运, 昨天他就开了一整天. 前苏联的雷达已经关闭, 但传闻2017年又重新启用. 他是无差别, 不分敌我的干扰. 传闻, 莫斯科自己的电台也难以幸免.


## 环境干扰?

当野外来临, 信号变强, 能明显听到电台背景种掺杂着一个高频的 嘶嘶 声音, 和人们抱怨的 LM386 症状非常一致. 因此我怀疑这是 LM386 的噪音. 虽然白天就没有这个高频 嘶嘶声, 说不通.

还是换了一个分立器件的功放测试, 问题依旧. 这是什么鬼. 从此展开对这个问题一周的砍伐.

既然不太像是音频放大器的故障, 是不是检波后滤波不干净? 只有一个电容是不是不够, 那就加一个电感来试试.

<img src="{{site.baseurl}}/images/TRF-longwire-block2.png" class="center" />

依旧是失败的. 列举下为了查明这个原因, 都做了什么, 看到了什么:

* 夜晚有嘶嘶声
* 可能只有部分台有嘶嘶声
* 白天无嘶嘶声, 声音和晚上一样响亮.
* 插入滤除短波的滤波器, 无效, 证明不是夜晚的短波导致的问题.
* 改变LM386 输入RC滤波, 只有在高音明显被衰减的情况下, 才能滤除这个嘶嘶声. 证明它在音频通带内.无法滤除.
* 更换50米长的天线, 结果与15米天线相同.
* 3DQ 检波器更容易嘶嘶响. 越灵敏越容易出这个响声.

这些都不行. 到矿石机群里打听, 很多人遇到相同的问题, 有可能是夜晚干扰. 不过干扰这么精确是很少见的. 一开始就怀疑是 IMD (互调干扰), 但又觉得, 无源检波本就动态大, 又是矿石机, 怎么可能呢. 

既然无法蒙对, 就只能上仪器试试了.  对比了50米天线上白天和夜晚的信号强度区别.

|<img src="{{site.baseurl}}/images/50m-ant-SA-day.jpg" width="400" />|<img src="{{site.baseurl}}/images/50m-ant-SA-night.jpg" width="400"/>|
| 左边是白天 | 右边是夜晚 |


可以看到夜晚的信号, 总体强度没有提高, 但是更加稠密, 一些弱台的信号得到增强.

顺便, 下面是15米天线上的信号. 可以看到, 15米天线的信号要比50米弱了不少, 并且15米天线对短波更加友好, 短波信号强于中波, 而50米天线上是中波强于短波的.

<img src="{{site.baseurl}}/images/15m-ant-SA-day.jpg" class="center" width="400"/>


## 证据

夜深人静的时候, 是开频谱的时候. 这段视频是在三个台中间来回切换的时候, 调谐线圈上的信号频谱. RBW 是 1khz, 输入衰减 0 dB. 

<div align="center"><iframe src="//player.bilibili.com/player.html?aid=967925197&bvid=BV1Sp4y1X7TM&cid=182307023&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" > </iframe></div>

其中 最高的信号当前接收的台, 附近有很多竖线, 是当前台的AM边带信号. 明显可以看到, 几个台的边带信号几乎完全混在一起. 双调谐的选择性也不大于15db. 这明显会引起 IMD 干扰. 某些电台的边带信号竟然有 80khz, 严重怀疑发射设备有故障了吧. 理想的边带是 5khz, 就是放松要求也不能到 80khz 吧. 



所以, 抓了白天和夜晚的电台直接的边带信号强度. 白天, 边带信号根本不会超出 20khz, 夜晚在80khz处都有很强信号, 80kh这么远, 都到另一个电台的中心频率了, IMD 没商量.

|<img src="{{site.baseurl}}/images/daytime-station-space.jpg" width="400"/>|<img src="{{site.baseurl}}/images/night-station-space.png" width="400"/>|
| 左边是白天 | 右边是夜晚 |

白天, 用信号发生器, 注入一个距离载波 80 khz, -50dbm 的纯音信号, 可以得到完全一样的啸叫声.  至于如何消除, 衰减信号, 改变双调谐耦合度, 用不灵敏的二极管, 都可以让 IMD 干扰不至于影响收听.

## 解释

因为是IMD, 所以一切都说得通了.

* 只有夜晚有嘶嘶声: 因为夜晚传播好, 边带信号才能到达.
* 可能只有部分台有嘶嘶声: 周围没有另一个电台, 就不会有IMD.
* 白天无嘶嘶声, 声音和晚上一样响亮: 夜晚只是弱态信号变强, 而强台没有进一步增加. 边带信号也得到加强.
* 更换50米长的天线, 结果与15米天线相同: 和天线无关.
* 3DQ 检波器更容易嘶嘶响: 灵敏的器件容易过载, IMD 产物更高. 
  

二极管混频动态范围很高, 不代表AM检波动态好. AM检波二极管工作在平方律区间, 而混频工作在开关区. 

