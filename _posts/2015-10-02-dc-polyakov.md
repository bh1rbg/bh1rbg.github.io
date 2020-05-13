---
layout: post
title: "DC Polyakov 直变频接收机"
excerpt_separator: <!--more-->
---

直变频接收机, DC 接收机, 又叫 零中频接收机. 省掉了超外差的中频变压器, 采用超高增益的音频放大器来代替中频放大器或取灵敏度. 

简化的同时也带来许多挑战, 音频稳定性就是最大的问题. DC接收机多用于 CW, SSB 还算是比较严肃的接收机. 之前也没有做过接收SSB信号的接收机, 一切都很新鲜, 充满挑战.

<div align="center">
<iframe src="//player.bilibili.com/player.html?bvid=BV1oe411x7Be&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe> </div>
<div align="center"> DC 接收机 SSB信号效果 </div>

 
## ARRL Mciro R1 直变频接收机.

<!--more-->

ARRL  推荐给新手的 直变频接收机是 Micro R1. 属于入门机型.

<img src='{{site.baseurl}}/images\DC-micro-r1.png'  class='center' />
<div align='center'> ARRL Micro R1 DC接收机</div>

虽然ARRL极力推荐, 还是放弃直接制作 micro R1.  micro R1 采用了极为靠谱的 T50-2 磁芯, FT2401-43 宽带变压器, 晶体振荡器,  以及音频变压器.   太遗憾了, 这些器件并不好找,  40米波段专用晶体就很稀缺, 美式磁环更是难找. 

最好用中周做. 

## DC Polyakov

有一种比较新颖的混频器,   HAM RA3AAE,  Vladimir Polyakov 发表于 1977年苏联的 <Radio> 杂志. 采用两个 二极管头尾相连进行混频. 本振频率是接收频率的一半, 7.050的 SSB信号, 只需要 7.050/2 = 3.525 Mhz 即可. 

AA1TJ  是这个电路的粉丝, 下面这个电路就是AA1TJ制作的 Polyakov DC接收机. 

<img src='{{site.baseurl}}/images\DC-polyakov.png'  class='center' />

无论是ARRL Mciro R1, 还是 AA1TJ 的 Polyakov, 都是针对 CW信号的, 没有考虑SSB. 不过, AA1TJ的电路更容易适应SSB . Polyakov 采用VFO, 频率容易调整.  同时采用中周制作双调谐滤波器, 元件易得, 用FM的中周即可,  不必要是 4uH,  1uH 到 几十 uH 都可以, 调整C1, C3 让中周谐振于 7Mhz 基本就可以.  C2 可以用微调电容. 


## 原型

那就动手吧. 

<img src='{{site.baseurl}}/images\DC-block-digaram.png'  class='center' width="500" />
<div align='center'> DC接收机框图 </div>

 基本保留 AA1TJ的所有设计, 除了音频放大器, 要换用 LM386, 就可以支持SSB.  AA1TJ的音频放大器有一个谐振在600Hz左右的音频LC, 是专门给CW接收准备的. 

<img src='{{site.baseurl}}/images\DC-receiver-proto.jpg'  class='center' />

原型机风格非常狂野, 布局不好.  DC接收机的音频增益很高, ARRL以及各路神仙, 都强烈建议采用单点接地的方式焊接.但是我并没有听, 主要是 ARRL的布局是 R1的, 不是给 LM386准备的.  采用整张覆铜板作为地平面, 多少还是有点靠谱的. 

注意这个可变电容, 切记, 必须采用减速电容, 减速比 10:1 以上. 不然是不可能把本振频率调整到符合SSB要求的精度的. 


<img src='{{site.baseurl}}/images\DC-ant.jpg'  class='center' />

这个天线可能是最不靠谱的器件了. 长5米, 垂直架设, 是一个加感天线.   ( 事后诸葛下,  拉一根15米长线比这个好得多. )

找了一个黄道吉日, 开机收听.  但除了沙沙声, 什么都没有.  情急之下, 在LM386之前又增加了一级音频放大, 依旧无声, 不过当夜幕降临,  终于, 等到了强大的短波SSB信号.

第一课就是: 得等HAM们吃完饭, 才有人通过 SSB 呼叫. 这不像广播电台,  不会整天都有人在, 有时候传播不好, 也是没有信号的.


## 音频增益和稳定性 

DC接收机最大的挑战就是音频. 整个接收机的增益全靠音频提供. 最初, 仅配备一个 LM386 放大器, 增益为 40 dB 最高增益. 完全dead bug(死虫) 法制作.

|<img src='{{site.baseurl}}/images\DC-LM386-deadbug.jpg' width="400"  class='center' />|<img src='{{site.baseurl}}/images\DC-LM386.jpg' width="400"  class='center' />|

这个增益是完全不够的. 一个DC接收机的建议增益是100 dB. 需要一个音频预放. W7ZOI 是美国大学教授, 他曾经推出过一个接收机叫做 "ugly weekender" 的直变频接收机, 其中的音频预放大器是良好的选择. 也曾经尝试过增加一个单管的音频放大器, 但是增益不足, 而且容易自激. 不得已, 转而寻求设计良好的放大器. 


<img src='{{site.baseurl}}/images\DC-gain-boost.png' width="600" class='center' />

这个放大器增益很高, Q11 是一个"电容放大器", 又叫做有源退耦电路. 能给预防提供良好的退耦性能, 是电路能够稳定的先决条件, 同时也大大减轻高增益音频电路容易出现的哼哼声(220V感应干扰). 

 "ugly weekender" 直变频接收机的音频后级, 也采用LM386.  我将电路重新画了下, 未作任何改动, 只是风格上比较老式. 这种风格的电路非常突出信号路径, 容易阅读.

<img src='{{site.baseurl}}/images\DC-my-gain.jpg'  class='center' />


这种强要搭棚的风格, 做出来是比较丑的. 不重要, 能工作最重要.  不过不幸的是, 音频自激依旧非常严重, 良好的设计也架不住乱七八糟的制作. (ugly weekender 文章建议地平面必须接220V 电源的地线.)

最后为了稳定, 不得已, 牺牲一些增益, 把R34 换成了 4.7k, 而把R35接成了1k. 参考我重新手绘的电路. 这样不要增益, 最终才使得音频放大器稳定下来.

预放大器出来通过了一个音量调节旋钮. 这段线很长, 对稳定性造成不利影响. 如果发生音频自激, 无论如何安排LM386和预放的位置, 都是不能解决问题的. 

我并没有完全照搬 "ugly weekender" 放大器, 而是省略了 Q10. Q10 给增益级提供了buffer, 输出阻抗低, 这是一个非常良好的设计, 我本不应该省略这个三极管. 保持信号在低阻抗线路上传输, 是良好的抗自激手段.

<img src='{{site.baseurl}}/images\DC-my-gain-proto.jpg'  class='center' />

这个焊接效果, 就不要深究了. 

## 其他音频解决方案

另外一个音频与放大器的电路也很有潜力.  同样采用了有源退耦电路, 输入输出都是低阻抗设计. 

<img src='{{site.baseurl}}/images\DC-gain-boost-intrest.png'  class='center' />

如果, 不想采用预放, 能不能解决增益问题? 还针是有条路, 不过LM386名声并不好, 据说噪音很大, 如果再配置成 70 dB 的超高增益, 不知道是个什么壮观景象. 

这个70dB 增益的 LM386 电路是 日本 HAM JF10ZL 介绍的. 可惜的是, 最近他的主页不再能访问.

<img src='{{site.baseurl}}/images\DC-LM386-70db.gif'  class='center' />

电路中 Rf控制增益, 取 3.3 欧姆时, 增益可达 74 dB. 

| Rf (ohm) | gain db |
|3.3 | 74|
|10	 | 70 |
|33	 | 54 |
|105 |	44|
|820 |	34|


## LO 稳定性

音频稳定下来, 就可以守听 SSB/CW 通讯了. 不过, 很快, 就能发现另一个问题: 本振的稳定性不够. 听一会儿声音就变调, 甚至完全不能辨识. 

<img src='{{site.baseurl}}/images\DC-LO-v1.jpg'  class='center' />

本振电路电路是常见的电容三点式振荡器, 采用中周作为谐振线圈.  折腾这个振荡器很久, 也没有完全满意. 不过收获是很多的. 长话短说. 

* 首先就是选材, 电容式重中之重, 请不要使用低于1毛钱的任何电容. 可以用老云母电容, NP0, C0G 瓷片电容.
* 如果振荡器的频率, 不能稳定在 HZ 级别 几十秒, 或者根本就是每秒跳几百, 几千Hz, 那绝对是电容用错了.
* 必须屏蔽, 装入金属壳子内部. 这可以极大的提高温度稳定性. 短期稳定性也大大提高. 

<img src='{{site.baseurl}}/images\DC-LO-mica.jpg'  class='center' />
<div align="center"> 左边云母和右边的聚苯乙烯都很好, 中间的电容请不要用在震荡器中 </div>

|<img src='{{site.baseurl}}/images\DC-mica-teardown-1.jpg' width="400" class='center' />|<img src='{{site.baseurl}}/images\DC-mica-teardown.jpg'  class='center' width="400"/>|

<div align="center"> 趁机解剖一个云母电容, 内部是镀银薄膜和云母片 </div>

更换良好的电容后, 装入金属外壳, 稳定性就基本上能保持几十分钟, 期间不需要再调整频率了.  尝试用 N750的瓷片电容去抵消中周和三极管的温度系数, 最终结果如下, 效果并不是特别明显, 绝不如屏蔽来的重要和直接. 温度补偿需要极大的耐心, 仔细测量, 费时, 并不容易得到良好效果. 

<img src='{{site.baseurl}}/images\DC-LO-temp-chart1.jpg'  class='center' />
<div align="center"> 波动幅度 200 Hz, 挺大的幅度, 对收听有很大影响 </div>


## 电路总结

最后, 把整个电路图贴出. 

<img src='{{site.baseurl}}/images\DC-block-digaram.png'  width="500"  class='center' />
<div align="center"> 框图 </div>

<img src='{{site.baseurl}}/images\DC-front-end.png'  class='center' />
<div align="center"> 前端 </div>
<img src='{{site.baseurl}}/images\DC-gain-boost-v2.jpg'  width="600" class='center' />
<div align="center"> 音频预放 </div>

<img src='{{site.baseurl}}/images\DC-LM386-mysch.jpg'  class='center'  width="500"/>
<div align="center"> LM386 功放 </div>

