---
layout: post
title: "TRF III 长线调谐收音机"
excerpt_separator: <!--more-->
---

最近做完一个成功的矿石机, 一个天线调谐器和一个主调谐器, 算是半拉双调谐. 两者是紧耦合的. 紧接着, 自然就是要接上音频放大器听听TRF的效果.

<img src="{{site.baseurl}}/images/crystal-dt-receiver.jpg" class="center" width="600" /> 

<!--more-->

## 框图
仅简单的加入一个 LM386 音频放大器, 就能有不错的效果. 

双调谐已经能很不错的隔离短波的冲击, 选择性也可以. 如果没有天调组, 仅有主调谐线圈, 短波的影响将在所难免, 无论哪一种拓扑, 不可避免的多少都会变成短波机, 而不是中波.

<img src="{{site.baseurl}}/images/TRF-longwire-block.png" class="center" />


## LM386

|<img src="{{site.baseurl}}/images/lm386-photo1.jpg" />|<img src="{{site.baseurl}}/images/lm386-photo2.jpg" />|


|<img src="{{site.baseurl}}/images/lm386-sch.png" class="center" />|<img src="{{site.baseurl}}/images/lm386-pcb.png" class="center" />|


## 啄木鸟干扰
<img src="{{site.baseurl}}/images/duga-radar.png" class="center" />

<img src="{{site.baseurl}}/images/duga-radar-arm.png" class="center" />


## 环境干扰


<img src="{{site.baseurl}}/images/15m-ant-SA-day.jpg" />|<img src="{{site.baseurl}}/images/50m-ant-SA-day.jpg" />
