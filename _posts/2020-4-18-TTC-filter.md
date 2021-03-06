---
layout: post
title: "TTC滤波器"
excerpt_separator: <!--more-->
---

手上这种中周骨架有很多过剩存货, 可以做短波 DTC/TTF (双调谐/三调谐) 滤波器.  

<img src="{{site.baseurl}}/images/green-bobin-coil.jpg" class="center" width="250">

这个PCB也是做了好久了, 这是一个 TTC (三调谐) 滤波器通用板, 适合10mm中周. 正是时候拿出来做一个TTC滤波器(7-7.2 Mhz)试试了.

<img src="{{site.baseurl}}/images/ttc-pcb.jpg" class="center" width="650">


<!--more-->

## 设计

一个双调谐/三调谐滤波器, 看到最多的建议是通过差调整滤波器让通带平坦, 调整耦合度来控制带宽. 这种做法可能得到一个比较好的结果很吃力. 调整过程中, 看不到任何滤波器设计的影子: 这到底是巴特沃斯、切比雪夫, 还是贝塞尔滤波器?

<<EMRFD>> (中文译名 《射频电路设计实战宝典》) 的作者, W7ZOI, 在<<EMRFD>>一书中给出了DTC的设计公式和步骤. 

<img src="{{site.baseurl}}/images/dtc-design-formula.png" class="center" width="500">

这里面的关键是 k, q 参数的选取, 他们控制着最终滤波器的特性, 这显然是一个Butterwoth 滤波器. 实际中, 自然不需要稿纸演算, 这组公式实际告诉我的是, 随便混搭出来的滤波器, 可能远不是你看到的那样, 也远非优化值, 就更别说最优了. 特别是如果有3个, 或者5,7个调谐组, 恐怕调整就相当难了.

<<EMRFD> 随书CD中有TTC设计软件.  此种中周电感, Q 值可能在 100 左右, 终端串联电容取建议最小值 47pf.

<img src="{{site.baseurl}}/images/dtc-design-1.png" class="center" width="450">

做好电路, 用信号源和频谱仪做幅度验证, 发现  插损(insert Loss) 大到离谱, 约 -30 dB, 并且无法调整到哪怕-10db. 这不是滤波器, 这是什么鬼. 

测试并不一定需要频谱分析仪, 考虑到这只有 7 Mhz, 毫伏表, 示波器, 微功率计皆可作验证. 信号源也可以用自制振荡器来代替.

## 测试

不得已, 必须测量一下这个线圈的 Q 值. 因为并无 Q表, 所以采用 3dB 带宽法测量. 实际测量此线圈 Q 值只有 50. 这就需要对设计进行调整, 带宽放松到400khz, 因为6.5Mhz 到 7Mhz 并无广播电台, 所以宽一点也可以. 最终所得设计参数如下:

<img src="{{site.baseurl}}/images/dtc-design-2.png" class="center" width="450">

然后感觉这次得有信心了, 高高兴兴测试, 结结实实打脸. 插损仍然是非常高, 无法匹配设计.

## 调整

不得已, 就对电路进行了一些无目的尝试, 有一些现象非常有启发性:

* 中间谐振器主导大部分插损, 如果调整中间谐振器无法将插损大幅度降低, 基本上调整就没有希望了. 
* 两侧谐振器可以优化 50欧姆匹配 -- 提高 Retrun Loss. 

最终, 发现将终端串联电容(68p) 提高到150pF, 终端匹配电容改为220pF, 可以将插损调整到4.5dB ! 


<img src="{{site.baseurl}}/images/dtc-design-3.png" class="center" width="450">

这是很打脸的事情, 主张设计先行, 实际调试出来的电路却与设计想去甚远. 但无论如何, 这都是曙光.


## 让设计和实际相符

这个串联电容, 取最小值可能是个错误.  47p 在 7 Mhz 有 400 欧姆的容抗. 而150pF, 则降低到150欧姆. 实验中采用 68p:220p , 调整后的滤波器, 很容易在远离设计频率的时候出现严重问题: 频率响应起伏不定. 而不是平滑下降.

采用串联电容阻抗要取低的原则, 得到了如下的设计, 与最终实际电路高度一致, 这才是想要的效果.

<img src="{{site.baseurl}}/images/ttc-7Mhz-final-design.jpg" class="center" width="550">

实际电路中, 谐振电容采用了不同的值 -- 这很容易通过调整中周补偿过来.

<img src="{{site.baseurl}}/images/dtc-design-4.png" class="center" width="450">

耦合电容7pF, 和终端阻抗变换电容(150p:940p) 完全按照设计值 -- 这两个参数控制了谐振的耦合度, 以及呈现给谐振电路的阻抗, 几乎是全部重要的因素了. 调整感受也顺畅, 快速:

* 调整中间中周, 让插损最小 -- 很容易调整到 -6dB 以内.
* 调整两端中周, 让插损进一步减小 -- 基本和设计值相同: 4.5 dB 左右. (Q值取60 到 70,  估计插损4dB 到 5dB)
* 实测带宽 430 Khz, 略宽于设计 (6.75 Mhz 到 7.17 Mhz), 中心频率 6.95Mhz, 设计 7Mhz.
* RL: 优于 -15dB

TTC对终结电阻有一定要求, 用在实际电路, 一般需要一个终结放大器(或者LNA) 做好阻抗匹配.  通过调整两端的谐振器, 让损耗最小的做法从信号实际收听的效果来看尚可, 但仍不是正确选择. 

调整好的TTC 接入 FT-180A接收机, 可以无需调整正常工作, 从侧面说明FT-180A输入阻抗是接近50欧姆的. 接入自制 DC 接收机则需要调整, 此DC接收机输入阻抗并不是50欧姆, 实际上并不适合直接使用这个TTC滤波器. 需要在DC接收机内增加一个LNA(低噪音放大器), 来匹配TTC滤波器.

