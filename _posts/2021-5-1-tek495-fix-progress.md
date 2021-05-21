---
layout: post
title: "Tektronix 495P 维修校准 (三)进展"
excerpt_separator: <!--more-->
---

花了无数时间逆向PCB的布局, 最痛苦的莫过于, 在将近完成的时候, 找到了准确的布局图.

<img src="{{site.baseurl}}/images/tek495-fix-31.png" class="center" height='600'>

无数次尝试校准对数放大器, 因为我盲目认为, 校准结果有问题, 肯定是哪里出了问题.

<!--more-->

## 简易校准流程

标准的校准流程需要用外部的信号源, 向对数放大器注入10Mhz的中频信号, 用于校准对数放大器的响应. 基本的设置就是信号源经过步进衰减器,送入对数放大器的输入. 当然, 采用HP8640B信号源的话, 并不需要外部的步进衰减器. 校准流程需要1db 步进.

<img src="{{site.baseurl}}/images/tek495-fix-32.png" class="center" >

这套流程比较复杂, 不外接信号发生器,也可以初步校准信号响应, 就是利用机器自带的校准信号源. 基本的流程如下:


* 断开校准信号源, 打开窄视频滤波器, 参考功率 在-70 dBm, 和 -20dBm之间来回切换. 这一步骤,要调整面板的 "LOG CAL", 使得 -20dbm 到 -70dbm 切换时, 信号基准线变化正好 5 格.

<img src="{{site.baseurl}}/images/tek495-fix-36.jpg" class="center" >


* 切换 2 dB/div 模式和 10 dB/div 模式, 调整 "INPUT Ref Level", 使得10db 和 2 dB 模式下, 幅度一样高. 

这是对数放大器的电位器布局:

<img src="{{site.baseurl}}/images/tek495-fix-37.jpg" class="center" >


* 接入校准信号源, 参考功率 -20 dbm, 调整 "OUTPUT Ref Level", 让信号达到最顶端. 切入50db 衰减器(或者30db), 调整"LOG Gain", 使得响应幅度变化正好 5 格(3格). 

* 重复 以上三步, 让每个结果都尽可能准确. 


## 对数放大器评估结果

最初的校准结果是这样的(外部注入的 0 dBm 信号, RBW: 1Mhz ):

|<img src="{{site.baseurl}}/images/tek495-fix-38.jpg" class="center" width="350"> | <img src="{{site.baseurl}}/images/tek495-fix-39.jpg" class="center" width="330"> |
|Tek495|HP8566|

这里最让我迷惑的是这个幅度响应到噪音的动态, 只有40dB, 无论怎么设置(我还是忽略了很多,后述), 这个动态范围就只有这么多. 右边是HP8566的响应. 这差的又点多. 即便是手头的 Anritsu MS610B, 这个范围也是很大的, 60dB.

由于一些原因(需要剁手), 还有一个备份的对数放大器, 是比较老的机器, TEK492上的对数放大器. Tek 49x 系列频谱分析仪的板卡, 几乎都可以互换. 这个对数放大器, 就可以很好的在495上工作.

<img src="{{site.baseurl}}/images/tek495-fix-35.jpg" class="center" width="550">
<div align="center">  直插元件的对数放大器 </div>

之后, 对这两块板子分别进行简易校准之后, 进行了对比测试:

|<img src="{{site.baseurl}}/images/tek495-fix-33.jpg" width="350" class="center" >|<img src="{{site.baseurl}}/images/tek495-fix-34.jpg" class="center" width="350">|
|492 的对数放大器|495的对数放大器|

492的对数放大器, 明显的比495放大器的动态范围要宽, 大约10 dB. 这一部分的测试, 几乎实在黑暗中摸索. 后续的经验说明这里有很多的问题没有搞对.

* 校准是不准确的, 作为对比, 倒是可以参考.
* 噪音和 RBW 有极大的关系, HP8566的 RBW 是300khz, 495启动默认是 1Mhz RBW. 一般这个噪音是-60dBm 到 -70 dBm.这里495只有 -40dBm, 有非常显著的差距. 
* 495 有个设置, 叫做 'MIN Noise', 没有开启之前, 会损失掉. 即便是开启, 仍然距离 -60dbm 的噪音水平差了大约 10db.












