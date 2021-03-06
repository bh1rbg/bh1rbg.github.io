---
layout: post
title: "TRF II  高阻检波器0V2收音机"
excerpt_separator: <!--more-->
---

场效应管高阻抗检波器的简单 RF 收音机.   如此简单, 又如此曲折.

<img src="{{site.baseurl}}/images/trf-ii-0v2-1.jpg" class="center" width="500" /> 



<!--more-->

## 异常震荡

非常简单的接了一个LC调谐电路, 通过几圈次级线圈, 直接连接到LM386放大器 (40DB 配置).  非常吃惊的是, 电台的声音非常的大. 大的离谱了. 40dB 的LM386 绝无可能做到这一点.

|<img src="{{site.baseurl}}/images/trf-ii-0v2-2.jpg" width="600"/> |<img src="{{site.baseurl}}/images/trf-ii-0v2-3.jpg"   width="600"/> |

接上示波器, 就一目了然了, 这个东西变成了一个再生接收机, 虽然完全不可控制, 也算是非常有趣.  http://theradioboard.com/rb/    论坛经常能看到很多用Lm386制作再生接收计的小项目.


##   单管放大器

 AA1TJ 在  'Talking Doll 40M regen receive' 这篇博客中采用了一个简单的, 带有音频变压器的放大器.  看起来很有趣. 

 |<img src="{{site.baseurl}}/images/trf-ii-0v2-5.jpg"   width="600"/>|<img src="{{site.baseurl}}/images/trf-ii-0v2-4.jpg" width="600"/> |

 
所以也照样子, 找了个情怀三极管,  做了一个.  做完才发现,  'Talking Doll ' 是个 CW 接收机, 这个放大器的输出变压器接了谐振电容, 来专门放大电报音频. 这个要进行下简单的改造, 把谐振电容去掉.


### 改造后的单管放大器

<img src="{{site.baseurl}}/images/trf-ii-0v2-6.jpg"   width="600"/>

输出是 4:1 的音频变压器, 实际上用了两个独立的2mH 电感做成的, 输出接在串连电感的中间, 喇叭是一副450 ohm(测试1), 和一个64 欧姆的耳机. 

450欧 耳机 测试结果如下:  
- 频率 690 HZ,  输入 20mV  输出 0.6v, 增益  600/20=30 倍
- 频率1.8 kHz 输入  20mV 输出 0.8v, 增益   40 倍

64欧 耳机 测试结果如下:  
-  20mV 输入, 可以很好的收听. 
-  690Hz 的时候, 输入20mv,  输出 120mV, 增益 6 倍


## 高阻检波器

这种叫做 "无限阻抗检波器" 的电路, 是电子管时代留下的叫法, 那时, 这种阻抗, 等价于无穷.  对应的现代版本, 就是一个偏置在几乎截止状态的一个JFET. 

<img src="{{site.baseurl}}/images/trf-ii-0v2-7.jpg"   width="600"/>

这种检波器非常有效的隔离开天线调谐器和放大电路,  后续电路不会影响调谐电路的Q值. 很多 "高保真"  爱好者采用这种检波电路. (估计是太古时代的高保真标准.)


## 随机短波接收机

有了检波器和音频放大器, 连接起来, 就立刻有了一个能收台的收音机.  之前做这种单管机时, 调试接收总是个问题, 因为室内无信号, 总要跑到室外或者靠近窗户, 才能调试机器.  自从15米长的天线架好后, 我感觉做单管机应该无往而不利了. 

|<img src="{{site.baseurl}}/images/trf-ii-0v2-7.jpg" width="600"/> |<img src="{{site.baseurl}}/images/trf-ii-0v2-6.jpg"   class="center"  width="600"/> |

现实是恨残酷的, 竟然就没有台.  当 JFET 检波器接入抽头时, 能收到台, 如果是接在线圈顶端, 就一个台都没有.  这样的结果, 高阻抗还有什么用呢. 

这奇怪的结果困扰了一个星期, 终于有一天, 意识到, 收到的电台都是短波, 根本不是中波广播台. 主要的原因是接线比较乱, 错误的将一个抽头接低, 导致实际有效的匝数很少, 也就只有短波台了. 

认识到这一点后, 自然就能纠正这个问题. 不过, 中波依旧无台, 无论是用15 米长的天线, 还是到户外去测试.中波都是没有任何信号的. 

不过既然短波可以工作, 那就在短波波段试试各种检波二极管, 试试高阻检波器吧. 从某处购得的极为便宜的肖特基1N60似乎不怎么样, 也难怪那么便宜. 拆机的锗二极管, 古老的 2AP9确实好很多. 但是如果听过JFET高阻抗检波器的效果,  这些二极管检波器确实是惨点. 


### 1V1

是时候加一级射频放大器了, 那样灵敏度肯定高多了, 每一本教科书都这么说的. 

<img src="{{site.baseurl}}/images/trf-ii-0v2-8.jpg"  class="center"   width="600"/>

不过, 首先的问题是, 得让RF放大器安静下来, 图示的放大器很容易震荡: 用5.6uH 的RFC, 失败, 震荡严重, 换用一个 4.7mH 的 扼流圈, 终于不震荡了. 不过, 不幸的是, 还是收不到任何中波广播台.

最后, 不用扼流圈了, 直接换成了电阻, 竟然可以, 虽然只能听到一个台, 声音很小, 还必须在窗边.  用大天线的时候, 仍然是一片噪音. 

调试还得继续.


## 是我的耳机不够灵敏吗

我开始怀疑音频放大器增益太低, 用低阻抗耳机的时候增益仅有 15dB, 低的可怜. 同时也想搞明白, 音频级到底多大的信号才能舒适的收听广播. 

因此用信号发生器直接接到耳机, 计算输出到耳机的电压, 得到能刚刚能听见, 声音偏低, 舒适收听所需要的信幅度.  实验结果是: 

高灵敏度的手机耳机(64欧):
- 刚刚能听到,  3mV
- 声音偏低,  30 mV
-  舒适,  100mV

高阻抗但是不灵敏的耳机(450欧姆)
- 刚刚能听到,  33mV
-  舒适,  1000mV


### 再生/来复机器的灵敏度问题

根据TA7642的手册,  其灵敏度大约是600uV, 指的是输入到TA7642的信号幅度.  在电子管时代, 资料显示, 一个再生或者 Reflex 接收机的林敏度大约能到 15uV- 30uV 的程度.  晶体管的再生和来复机器就没有什么数据了.

### 另一个有趣的问题是, 天线上的信号大概是多少uV 呢?

对于磁棒天线, 实际上是有计算公式可以计算天线输出的信号强度的. 涉及到计算磁棒的有效磁导率, 等效天线长度等. 总之 一个120 mm的磁棒,  配合不同地区的估计电场强度, 可以估计天线输出信号大值范围.  对于中等信号强度(远郊县, 0.5mV/m), 输出信号强度大值在 100uV 到 1000uV 范围内. 

为了听清楚, 用上面测试中使用的耳机收听(灵敏的那个耳机),  需要将信号放大 33mv/0.5mV = 66  倍, 大约需要 35 db 到 40dB 的增益. 

显然,  音频放大的增益实在是太低了.  短波信号, 由于我的长线天线非常适合接收短波信号, 所以短波广播台信号非常强大,  就远远不需要高增益的音频级就能收听. 

## 0V2

既然知道了问题所在, 就简单了, 再来一级音频放大器级联起来.  一开始希望用两级带变压器的放大器, 不过那样音频级就产生了强震荡.  最后, 音频第一级用的是电阻负载. 

<img src="{{site.baseurl}}/images/trf-ii-0v2-9.jpg"   class="center" width="450" /> 


整体电路就是图中两部分的拼接. 并没有采用射频放大器.  并且效果惊人的好,  室外收听几乎能听到所有本地电台和邻近城市的电台. 声音也很好. 

|<img src="{{site.baseurl}}/images/trf-ii-0v2-7.jpg" width="600"/> |<img src="{{site.baseurl}}/images/trf-ii-0v2-10.jpg"   class="center"  width="600"/> |


