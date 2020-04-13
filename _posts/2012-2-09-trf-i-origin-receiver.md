---
layout: default
title: "TRF I"
---

TRF收音机紧邻矿石收音机. 矿石收音机装上音频放大器, 就可以叫做一个TRF了. 如果从未做过收音机, TRF似乎是个不错的选择, 可以增强diy的信念, 获得宝贵经验.

![]({{ site.baseurl }}/images/trf-i-hb-pcb.jpg)


## 从矿石机开始

![]({{ site.baseurl }}/images/trf-i-crystalradio-sch.jpg){: align="center" }

矿石收音机的结构简单, 一副天地线, 一个二极管和一个高阻抗耳机. 但是要求其实很多了.

*首先天地线是成功的关键, 天线要长, 要高, 最好15米起, 至少离开地面 2, 3米吧, 很多人架在楼顶.

*高阻抗耳机也挺重要的, 要不就来个变压器进行下阻抗变换. 最重要的是, 耳机要灵敏度高才行. 最合适的就是舌簧耳机, 这种耳机那是越来越少了.

*最后, 也是最重要的, 你距离电台的远近. 如果不是城区, 甚至是偏远地区, 就有可能根本没有强限号, 中波矿石机很难成功.

*这个电路极为简单, 选择性是很差的. 信号强的地方, 耳机里听到很多电台一起说话, 很是热闹.



![]({{ site.baseurl }}/images/trf-i-nice-crystal.jpg){: align="center" }

艺术品一样的矿石收音机.



## 准备天线一副

中波收音机里常见的磁棒天线, 是不大可能在混凝土房子的室内收到任何信号的. 所以, 搞了一个大环天线. 说是大环, 其实直径很小, 才区区 40 cm 左右, 这个大环将作为谐振线圈直接作为TRF收音机的调谐线圈.

![]({{ site.baseurl }}/images/trf-i-loop-ant.jpg){: width="500" }



## 第一部TRF

![]({{ site.baseurl }}/images/trf-i-trf-sch-1.jpg){: align="center" }

这就是第一部要实验的TRF收音机电路了. 乍看之下, 最奇怪的地方是检波电路哪里去了. 本意呢是要用三极管检波, 后来仔细审视,感觉二静态电流取得比较大, 这可能导致检波效率不高.  把 9018 510k 电阻换成 1兆欧姆可能更好, 而9014的偏置二电阻可以减小少许, 可以实验决定.



## 改进1:调谐线圈抽头

![]({{ site.baseurl }}/images/trf-i-trf-sch-tap.jpg){: align="center" }


## 改进1: bootstrap
![]({{ site.baseurl }}/images/trf-i-trf-sch-2.jpg){: align="center" }

## 改进2: 高阻检波
![]({{ site.baseurl }}/images/trf-i-trf-sch-final.jpg){: align="center" }

