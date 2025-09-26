# <p align="center">轮足机器人开篇</p>
##  轮足机器人简介
![轮足机器人照片](https://github.com/Limitput/Wheeled-robot-my/blob/main/image/%E5%BC%80%E6%BA%90%E5%85%A8%E8%BA%AB%E7%85%A7.jpg)
一种可以均衡地形的机器人，可以竞速跳跃，**跨越障碍、上下楼梯、保持平衡**
在平坦、坚硬的表面上（如马路、室内地板），轮子具有**速度快、能耗低、控制简单、运动平稳**的巨大优势。
看样子很不错虽然打算老实考研，但是过程过于枯燥，于是选择缓慢的开启一个项目配合考研同步进行
![3205电机](https://github.com/Limitput/Wheeled-robot-my/blob/main/image/3205%E7%94%B5%E6%9C%BA.png)
![2804电机](https://github.com/Limitput/Wheeled-robot-my/blob/main/image/2804%E7%94%B5%E6%9C%BA.png)
## 硬件方面
- 轮组选择
目前有3205无刷电机和2804无刷电机两个选项
二者的参数对比如下

|参数|2804 电机|3205 电机|
| - | - | - |
|**核心尺寸**|**定子直径: 28mm** ；**定子高度: 4mm**|**定子直径: 32mm**；**定子高度: 5mm**|
|**重量（g）**|30 - 38 g|45 - 55 g|
|**KV值范围**|800 - 1600 KV|700 - 1300 KV|
|**最大持续电流（A）**|15 - 25 A|20 - 35 A|
|**最大功率（W）**|300 - 500 W|450 - 750 W|
|**推荐电调（A）**|30A - 40A|40A - 60A|
|**专项**|**灵活、高效、轻量**（平衡性好）|**扭矩大、动力猛、重量大**（偏运动）|
|**价格**|24R|25R|

如果我能获得充足的预算的话应该会上4010电机，毕竟全方位碾压上面的东西
![4010电机](https://github.com/Limitput/Wheeled-robot-my/blob/main/image/4010%E7%94%B5%E6%9C%BA.png)

- 滑轮驱动选择，目前初步打算自己制作，但由于还没有学习过FOC驱动，于是打算先用开源硬件过度一下
机械结构目前使用[灯开源的四舵机二无刷结构](https://www.bilibili.com/video/BV1kz421B73V?spm_id_from=333.788.videopod.sections&vd_source=bb311f54a7671df0ea69db4afaf49631)
驱动还是漫长的选型比较好，或者等我先研究清楚[drv8301](https://www.bilibili.com/video/BV1NT4y1m7iy/?spm_id_from=333.337.search-card.all.click&vd_source=bb311f54a7671df0ea69db4afaf49631)？需要时间，所以前期的FOC学习先用matlab来仿真实践一下（qvq）
- 关节就先采用四个金属舵机进行替代型号是[GDWDS041](https://item.taobao.com/item.htm?abbucket=9&id=822105777693&mi_id=0000nbFLiI__PFfbfBkLcKQyhjINVwvAbS6nAfM4387tD5w&ns=1&skuId=5700115170704&spm=a21n57.1.hoverItem.1&utparam=%7B%22aplus_abtest%22:%2295969d8fd33971d31a28468b02d6e955%22%7D&xxc=taobaoSearch)
- 陀螺仪的话，采用[bmi088](https://blog.csdn.net/asdashhv/article/details/124413960)就好，希望板载能一次性使用。预计会采取恒温系统以降低温漂。备选是[ICM42688](https://oshwhub.com/xrobot/9-axis-3-0)
- 主控就选择浮点运算还可以的（不至于没有），且较为便宜的G431（主要是带FPU，算的更快），性能更强。
-
## 软件方面
- 主控STM32G431rbt6。
- 需要解决的问题
 1. 优先需要解决的问题就是FOC的学习和应用，具体的教程包含但不限于[基于STM的无感FOC控制原理](https://www.bilibili.com/video/BV1Fx76zzEcP/?spm_id_from=333.337.search-card.all.click&vd_source=bb311f54a7671df0ea69db4afaf49631)、[FOC算法](https://www.bilibili.com/video/BV1x84y1V76u?spm_id_from=333.788.videopod.sections&vd_source=bb311f54a7671df0ea69db4afaf49631)
 2. 陀螺仪的使用以及搭配。首先就是[陀螺仪原始数据的读取](https://blog.csdn.net/asdashhv/article/details/124413960)，对原始数据进行[防零漂处理](https://www.iotword.com/14737.html)，然后就是对原始数据进行[卡尔曼滤波](https://blog.csdn.net/qq_31775031/article/details/117067785)（可以用matlab进行仿真）。
 3. 然后就是轮足机器人的[运动学解析](https://www.bilibili.com/video/BV1kz421B73V?spm_id_from=333.788.videopod.sections&vd_source=bb3strikethrough text11f54a7671df0ea69db4afaf49631)了，这个还是不错的，有人视频带着1对1学习。
 4. 最重要的一点，**坚持**，哪怕进度慢也一小步一小步的走

> 一点自己的小见解

线代的信息发展还是很好用的，但是如果真的面临需要独立面对英文数据手册的时候，~~我其实也不知道应该怎么做~~，感觉需要锻炼一下自己独立阅读的能力。但是不是现在，毕竟还是要考研捏ʅ（´◔౪◔）ʃ，本文的初衷也是敦促自己在考研的时候不忘记之前的知识同时给无聊的考研生活上点色彩。
就这样吧,花了一上午的时间整理和写作，该进行今天的考研了，祝好。

