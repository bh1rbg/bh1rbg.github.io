---
layout: post
title: "ultra-audion Colpitts"
excerpt_separator: <!--more-->
---

这个振荡器是非常常见, 很多时候没有名字. 偶尔机遇, 我知道了他叫 ultra-audion Colpitts, 是一个利用三极管内部电容作为震荡反馈一部分的特殊电路. 最大的特点就是简单到令人发指, 各种无线电话筒, 90% 的电路是这种.

首测感觉有必要稍微看看一个这种电路, 是一次想要做个 AM 波段的实验发射机. 就觉得好奇, 这个玩意为什么能震荡呢, 正反馈通路到底在哪里.


<img src="{{site.baseurl}}/images/ultra-audion-transmiter.jpg" class="center" />


<!--more-->


## 各种无线电话筒

随便摘了两个, 全是这种电路. 这个振荡器的名字是很奇怪的, ultra-audion Colpitts, 直译叫 超音考毕兹 振荡器, 感觉都不像是一个名字, 而是描述. 并且 ultra-audion 这个词, 貌似很多情况下都是指再生, Regenerative. 

| :---: | :---:|
|![]({{site.baseurl}}/images/ultra-audion-bug1.jpg)|![]({{site.baseurl}}/images/ultra-audion-bug2.jpg)|


## 震荡原理

<img src="{{site.baseurl}}/images/ultra-audion-simple-sch.jpg" class="center" />

这个电路, 和上面各种话筒所用的振荡器是完全一样的. 之所以说他是 考毕兹 的一种, 它是利用了三极管的内部结电容 - Cbe. 通过Cbe到基极, 而基极是接地的.

这种电路还有下面的形式. 三极管的三个结电容作为谐振电路的谐振电容, 这肯定是不要稳定性了, 只要震荡就好了. 

<img src="{{site.baseurl}}/images/ultra-audion-sch.jpg" class="center" />



## 能有多简单

这种利用结电容的极端例子, 就是下面这个流行在各大论坛的无线电话筒. 实际情况是, 这种电路, 既有可能难以起振, 更别提多么稳定了. 它就是简洁美的极致例子.

<img src="{{site.baseurl}}/images/ultra-audion-tinny.jpg" class="center" />

## 搞定不起振

如果所用的三极管结电容很低, 而目标震荡频率不高, 就极有可能不能起振. 这种情况下换个Ft低的三极管, 有可能反而可以工作. 

<img src="{{site.baseurl}}/images/ultra-audion-fix.jpg" class="center" />

实在不行, 就放弃这种简洁, 转投真正的 Colpitts 电路吧, 只需要多接一个电容而已(图中39pF的电容).


