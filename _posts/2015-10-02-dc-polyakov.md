---
layout: post
title: "DC Polyakov 直变频接收机"
excerpt_separator: <!--more-->
---

直变频接收机, DC 接收机, 又叫 零中频接收机. 省掉了超外差的中频变压器, 采用超高增益的音频放大器来代替中频放大器或取灵敏度. 

简化的同时也带来许多挑战, 音频稳定性就是最大的问题. DC接收机多用于 CW, SSB 还算是比较严肃的接收机. 之前也没有做过接收SSB信号的接收机, 一切都很新鲜, 充满挑战.

<img src='{{site.baseurl}}/images\DC-block-digaram.png'  class='center' width="500" />
<div align='center'> DC接收机框图 </div>

 
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


##  音频增益和稳定性 

<img src='{{site.baseurl}}/images\DC-my-gain-proto.jpg'  class='center' />
<img src='{{site.baseurl}}/images\DC-my-gain.jpg'  class='center' />


<img src='{{site.baseurl}}/images\DC-gain-boost-intrest.png'  class='center' />

<img src='{{site.baseurl}}/images\DC-gain-boost.png'  class='center' />
<img src='{{site.baseurl}}/images\DC-LM386-70db.gif'  class='center' />
<img src='{{site.baseurl}}/images\DC-LM386-deadbug.jpg'  class='center' />

<img src='{{site.baseurl}}/images\DC-LM386.jpg'  class='center' />

## LO 稳定性

<img src='{{site.baseurl}}/images\DC-LO-v1.jpg'  class='center' />

<img src='{{site.baseurl}}/images\DC-LO-mica.jpg'  class='center' />
<img src='{{site.baseurl}}/images\DC-LO-temp-chart1.jpg'  class='center' />



|<img src='{{site.baseurl}}/images\DC-mica-teardown-1.jpg' class='center' />|<img src='{{site.baseurl}}/images\DC-mica-teardown.jpg'  class='center' />|


## 电路总结

<img src='{{site.baseurl}}/images\DC-block-digaram.png'  width="500"  class='center' />
<img src='{{site.baseurl}}/images\DC-front-end.png'  class='center' />
<img src='{{site.baseurl}}/images\DC-gain-boost-v2.jpg'  width="600" class='center' />
<img src='{{site.baseurl}}/images\DC-LM386-mysch.jpg'  class='center'  width="500"/>


<iframe src="//player.bilibili.com/player.html?bvid=BV1oe411x7Be&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
