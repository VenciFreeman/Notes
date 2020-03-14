# 基于旋转器的前馈FFT架构

> Garrido M , Huang S J , Chen S G . Feedforward FFT Hardware Architectures Based on Rotator Allocation[J]. IEEE Transactions on Circuits and Systems I: Regular Papers, 2018, 65(2):581-592.

[TOC]

### 摘要

- 基于旋转器(rotaters)分配的新前馈FFT硬件架构
- 本文的旋转器分布方法可以<u>减少FFT中旋转器的数量和复杂性，降低硬件成本</u>
  - 基于旋转器分配的基-2
  - 基于旋转器分布的基-2<sup>k</sup>前馈架构

### 索引词

`快速傅立叶变换(FFT)`

`多路径延迟换向器(MDC)`

`流水线架构`

## 综述

### 流水线FFT架构

#### 优点

- 适合实时的高吞吐量
- 低延迟
- 相当低的面积和功耗

#### 三种类型

- 反馈(FB)
  - 单路延迟反馈(SDF)
    - 每个时钟周期处理一个样本
  - 多路延迟反馈(MDF)
    - 并行处理一个样本
- 前馈(FF)
  - 主要由多路延迟换向器(MDC)组成
  - 没有反馈回路
  - 每级数据处理后进入下一级
- 串行换向器(SC)
  - 使用串行数据的位置换电路

> MDC FFT已达到100%使用率和最少总内存量，但旋转器可优化

## FFT算法

### 基本算法

$$
X[k]=\sum_{n=0}^{N-1}x[n]W_N^{nk},~k=0,1,...,N\\
其中~W_N^{nk}=e^{-j\frac{2\pi}{N}nk}.
$$



### 旋转方式

$$
W_N^φ=e^{-j\frac{2\pi}{N}φ}
$$

- 不需要转换器
  - $φ=0$不需要旋转
  - $φ∈{0,\frac{N}{4},\frac{N}{2},\frac{3N}{4}}$，样本旋转$0°,270°,180°~或~90°$，分别对应于$1,-j,-1和j$

![16点基2DIF-FFT流图](https://github.com/VenciFreeman/Notes/blob/master/fig/FEEDFORWARD_FFT_HARDWARE_ARCHITECTURES_BASED_ON_ROTATOR_ALLOCATION_fig_1.png)

## FFT旋转器的类型及成本

### 16点FFT对称角度集

| Set 0 | Set 1 | Set 2 |
| :---: | :---: | :---: |
|   0   |  1 3  |   2   |
|   4   |  5 7  |   6   |
|   8   | 9 11  |  10   |
|  12   | 13 15 |  14   |

对称角度集：

- 角度$\frac{nπ}{2}±α$的集合，其中$n = 0，...，3$，$α∈[0,\frac{π}{4}]$
- 对称角度集合中的任何旋转都可以表示为
  - $α$的旋转
  - 其他旋转
  - 旋转系数的虚实部交换

![16点FFT旋转角度](https://github.com/VenciFreeman/Notes/blob/master/fig/FEEDFORWARD_FFT_HARDWARE_ARCHITECTURES_BASED_ON_ROTATOR_ALLOCATION_fig_2.png)

### 旋转器类型

- 普通旋转器：
  - 可以以任意角度(由输入提供)旋转
  - CORDIC算法
-  单个恒定转子(SCR)
  - 执行单个恒定角度旋转
- 多重恒定旋转器(MCR)
  - 旋转几个恒定角度中的一个角度
  - CCSSI算法

多路复用器等效于1/4加法器

## 设计FFT硬件结构的一般准则

### FFT的属性

- 对任何FFT体系结构和N通用
  - 需确保在每一级，任何时间任何输入的索引在b<sub>n-s</sub>上都不同 <唯一条件>
- FFT各级的旋转
  - 每一级各个样本都需旋转一个角度φ
    - φ取决于索引和级数。其仅取决于所选的FFT算法

### 结论

- 在蝶形运算输入处满足b<sub>n-s</sub>的性质，任何FFT硬件体系结构任一级的任何顺序都有可能
- 在任一F级，任何索引都对应一个特定的旋转因子
-  结果：可以交换不同级的数据处理顺序以优化旋转器分配

## 使用旋转器分配的FFT设计

- 目的是减少所需的旋转器数量，降低旋转器复杂度

### 布局示例

- a
  - 16点4并行FFT不同阶段数据流向
  - 数据从左向右流动
  - 矩阵中每一列在相同时钟周期上并行计算旋转
  - 同一行中旋转由同一旋转器在连续时钟周期中计算
- b
  - 由a转换，显示每个阶段的旋转器以及旋转存储器的内容

![16点4并行FFT](https://github.com/VenciFreeman/Notes/blob/master/fig/FEEDFORWARD_FFT_HARDWARE_ARCHITECTURES_BASED_ON_ROTATOR_ALLOCATION_fig_4.png)

## 针对基-2和基-2<sup>k</sup>的架构

## 本文方法与最新技术比较

## 实验结果及比较

## 主要结论
