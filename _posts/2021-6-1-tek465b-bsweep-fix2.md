---
layout: post
title: "Tektronix 465B B扫维修 (三)修复"
excerpt_separator: <!--more-->
---

虽然已经修复了B 触发放大器, 可B-sweep 依旧无法正常工作. 

<img src="{{site.baseurl}}/images/tek465b-bsweep-5.png" class="center" >

这里工作流程是, 信号放大器触发 ARMING TD, ARMING TD 触发后, 越变到0.5V 的高压状态, 此时流过电流反而更少, 因此剩余的的电流则流过 FIRING TD, 使得FIRING TD 跳变到高电压状态.

FIRING TD 产生的阶越信号开启控制电路的 B 触发门:
<!--more-->
<img src="{{site.baseurl}}/images/tek465b-bsweep-6.jpg" class="center" width="600">

FIRING TD 信号从 <62> 输入, 触发Q7053, Q7055组成的门电路, 从<63>输出到 B扫描电路, B扫开始. 

## 故障溯源

这里 FIRING TD 无法触发. 经过对换 A/B 触发电路的 隧道二极管, 确认隧道二极管工作正常.最可能的原因是 ARMING TD没有触发. 

ARMING TD 受控于逻辑电路, 用于实现 "hold off", 就是在一段时内禁止触发.

<img src="{{site.baseurl}}/images/tek465b-bsweep-14.png" class="center" width='450'>

当8处电压为 -0.5V时, 9 直接连接到ARMING TD, 将触发电流拉走. 使得 ARMING TD达不到触发电流而无法跳变到高电压, 从而实现hold off (也就是B扫的10圈延迟电位器控制的一段时间)

<61> 处直流电压为1.2V, 7处为5V, Q7155截止. 且 <61>处无方波信号, <61>这里应该在A扫开始一定的时间后变为低电平, 


<img src="{{site.baseurl}}/images/tek465b-bsweep-12.png" class="center" width='650' >

上图 <61> 处和这里的6 是联通的. 这是一个电压比较器, 将 A扫的锯齿波 (13V-2V)信号, 和B扫延迟电位器的控制电压进行比较, 当到指定电压, 也就是一定的延迟后, 比较器反转, 不再对B扫进行 "hold off", B扫描触发二极管(ARMING TD)被信号触发, B扫开始. 

测量 2, 4处, 都有方波, 并且可控(通过B扫电位器), 而 6 处方波消失. 4处波形如图.

<img src="{{site.baseurl}}/images/tek465b-bsweep-9.jpg" class="center" width='450' >

## 计算与

 2, 4处, 都有方波, 而输出的 6处无对应信号, 说明这周围电路有问题. 测量DC电位, 5,2处电位在标注值附近(误差0.2V内), 而4处电压 13V, 显著不同于15.9V的标注值.

断电测量Q7074, Q7075, 正常. 4处电压不足的意义是什么是值得研究的问题.

<img src="{{site.baseurl}}/images/tek465b-bsweep-12.png" class="center" width='650' >

6 处电压标注于测量点 <61>, 正常状态下为1.2V. 此处电压正常. 电路并没有标注15.9V是什么状态下的电压. 假设此处是Q7075/Q7067右侧三极管处于导通状态下的电压值. 

那么从55V经过 R7164电阻流过 (55-15.9)/5.6k ~= 7mA, 其中从R7065 流走 (15.9-15)/0.68 ~= 1.3mA.  R7179上流过 (-8-0.6)/2.26k ~= 3.3 mA 电流.  所以流入R7068/R7070 串连电路的电流是 7-1.3-3.3 ~= 2.4 mA. (注意Q7074截止)

但是根据4处电压 流过 R7068/R7070 串连电路的电流是 15.9/(8.6k+1k) ~= 1.6mA, 对不上2.4mA 的计算值. 不过, 稍等, R7068真的是8.6k么, 那个8字可有点奇怪. 经过仔细辨认, 它其实是5.6k. ^_^,  这就完全正确了. 

<img src="{{site.baseurl}}/images/tek465b-bsweep-14.png" class="center" width='450' >

## 修复

这意味着, 15.9V 是 4处的最低电压, 因为如果右侧两个三极管截止的话, 流过 R7164的电流就会大大减少, 因为 Q7067右侧三极管的电流不再流过 R7164.

这一点至关重要, 测量4处直流电位是13V, 不足15.9V, 而唯一可能的原因是 R7164 根本没有电流流过, 此处电压是 R7065和 R7068/R7070分压的结果.  如果R7164流过电流, 因为必然比Q7075导通时电流要小, 因此R7164上的压降更低, 4处电压就会高于 15.9V. Q7075并未损坏, 其基极电流可以忽略. 

综上所述, 唯一可能的原因就是R7164 没有电流流过, 也就是它开路. 

实际上机测试, 在R7164上并联5.6k电阻, 故障排除, 更换此电阻后问题解决. 

<img src="{{site.baseurl}}/images/tek465b-bsweep-11.jpg" class="center" width='450'>

此电阻压降高,功率大, 容易开路. 

