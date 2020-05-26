---
- 掌握RISCV处理器基本原理
- 掌握基于RISCV的SoC原理和工作模式
- 熟悉基本芯片主要模块原理和工作模式(I2C)
- 独立设计SoC模块，完成模块在SoC中的集成与仿真(DMA控制器)
---



# 基于蜂鸟RISCV处理器的SoC

[TOC]

## 简介

### RISCV

- 2010年发源于加州大学伯克利分校
  - 不受现有处理器架构复杂性和相关知识产权的限制
  - 全新的，简单且开发免费的指令集架
- 目标
  - 完全开放，可自由使用
  - 真正适合软件实现且稳定

### 深入理解ISA

> 介于软件与硬件之间

- 数据类型
- 存储模型
- 软件可见的处理器状态
  - 通用寄存器
  - PC
  - 处理器状态
- 指令集
  - 指令类型与编码
  - 寻址模式
  - 数据结构
- 系统模型
  - 状态
  - 特权级别
  - 中断和异常
- 外部接口
  - 输入输出接口
  - 管理

### RISCV架构特点

- RISC-V的指令集使用模块化的方式进行组织，每一个模块使用一个英文字母来表示
- RISC-V最基本也唯一强制要求实现的指令集部分是由I字母表示的基本整数指令子集

|   基本指令集   |   指令数   |                             描述                             |
| :------------: | :--------: | :----------------------------------------------------------: |
|     RV32I      |     47     |        32位地址空间与整数指令，支持32个通用整数寄存器        |
|     RV32E      |     47     |            RV32I的子集，仅支持16个通用整数寄存器             |
|     RV64I      |     59     |         64位地址空间与整数指令及一部分32位的整数指令         |
|     RV128I     |     71     |       128位地址空间与整数指令及一部分64位和32位的指令        |
| **扩展指令集** | **指令数** |                           **描述**                           |
|       M        |     8      |                      整数乘法与除法指令                      |
|       A        |     11     | 存储器原子 (Atomic)操作指令和Load-Reserved/Store-Conditional指令 |
|       F        |     26     |                   单精度 (32 bit)浮点指令                    |
|       D        |     26     |          双精度 (64 bit)浮点指令，必须支持F扩展指令          |

### RISC-V实现简介

- 架构
  - RISC-V是一种开放的指令集架构，而不是一款具体的处理器。任何组织与个人均可以依据RISC-V架构设计实现自己的处理器，只要是依据RISC-V标准设计的处理器，都可称为RISC-V处理器
- 微架构
  - 自RISC-V架构诞生以来，已经出现了数十个版本的RISC-V架构处理器，有开源免费的，也有商业公司开发用于内部项目的，还有商业IP公司开发的RISCV处理器IP

#### 当前主要开源RISCV处理器

- Rocket Core (开源)
- BOOM Core (开源)
- Freedom SoC (开源)
- LowRISC SoC (开源)
- PULPino Core and SoC (开源)
- PicoRV32 Core (开源)
- ORCA Core (开源)
- SCR1 (开源)
- Codasip Core (商业)
- Andes Core (商业)
- Microsemi Core (商业)
- Nuclei Core (商业)

## 流水线

### 蜂鸟E203处理器内核

<img src="..\fig\ME04\ME04_chapter06_fig01.jpg" style="zoom:80%;" />

- e203_cpu_top 蜂鸟E203顶层模块
  - e203_cpu，逻辑模块顶层
    - e203_core，处理器核
      - e203_ifu，取指单元IFU
      - e203_exu，执行单元EXU
      - e203_lsu，存储器访问单元LSU
      - e203_biu，总线接口单元BIU
    - e203_clk_ctrl，控制各组件自动时钟门控
    - e203_irq_sync，异步中断转同步
    - e203_itcm_ctrl，ITCM访问控制
    - e203_dtcm_ctrl，DTCM访问控制
    - e203_reset_ctrl，将外部异步置位信号同步
  - e203_srams，SRAM模块顶层
    - e203_itcm_ram，ITCM指令紧耦合存储器
    - e203_dtcm_ram，DTCM数据紧耦合存储器

### 流水线结构

> 严格来说，蜂鸟E203是一个变长流水线结，是非严格意义的二级流水线结构

<img src="..\fig\ME04\ME04_chapter06_fig02.jpg" style="zoom:80%;" />

- 流水线的第一级为"取指" (由IFU完成)
- "译码" (由EXU中完成)、"执行" (由EXU中完成)和"写回" (由WB完成)，它们均处于同一个时钟周期，位于流水线的第二级
- "访存" (由LSU完成)阶段处于EXU之后的第三级流水线，但是LSU写回的结果仍然需要通过WB模块写回通用寄存器组

#### E203 IFU设计理念

- 蜂鸟E203假定绝大多数的取指都发生在ITCM中，这种假定具有合理性
  - 针对向嵌入式超低功耗场景设计：代码量不大
- 蜂鸟E203的ITCM使用单周期访问的SRAM
- 在一个周期内完成了指令读取 (假设是从ITCM中取指)、部分译码 (Mini-Decode)、分支预测 (Simple-BPU)， 和生成下一条待取指令的PC等连贯操作

### 取址单元

<img src="..\fig\ME04\ME04_chapter06_fig03.jpg" style="zoom:80%;" />

- IFU在取出指令后，会将其放置于和EXU单元接口的IR (Instruction Register)寄存器中
- 该指令的PC值也会被放置于和EXU单元接口的PC寄存器中
- EXU单元将使用此IR和PC进行后续的执行操作

#### 主要功能

- 对取回的指令进行简单译码 (Mini-Decode)
- 简单的分支预测 (Simple-BPU)
- 生成取指的PC (PC生成)
- 根据PC的地址访问ITCM或BIU (地址判断)

#### 实现

##### Mini-Decode

- 指令16位还是32位
- 判断普通指令还是分支跳转指令
- 分支跳转指令的类型和细节

##### Simple-BPU

- 采用最简单的静态预测 (BTFN)
- 对于jarl指令需要访问通用寄存器组进行一定优化设计

##### PC生成

- Reset：pc_rtvec
- 顺序取指：根据当前指令判断自增值
- 分支指令：根据Simple-BPU预测
- 流水线冲刷：EXU送过来的新PC值

##### 访问ITCM和BIU

- ICB总线：ITCM (64位)，BIU (32位)
- 非对齐指令取址：采用剩余缓存 (Leftover Buffer)

### 执行单元

#### 简介

- 执行是处理器微架构的中枢核心阶段
- RISC-V架构追求简化硬件的哲学，具体对于执行 (包括译码)而言，RISC-V架构的如下特点可大幅简化其硬件实现
  - 整数指令都是两个操作数
  - 规整的指令编码格式
  - 精简的指令个数
  - 紧凑的16位指令

#### 架构

<img src="..\fig\ME04\ME04_chapter06_fig04.jpg" style="zoom:80%;" />

- 将IFU通过IR寄存器发送给EXU的指令进行译码和派遣
- 通过译码出的操作数寄存器索引 (Index)读取Regfile
- 通过OITF维护指令的数据相关性
- 将指令派遣给不同的运算单元执行 (ALU、Long-Pipes、LSU及EAI)
- 将指令交付
- 将指令运算的结果写回Regfile (WB Arb)

#### 实现

<img src="..\fig\ME04\ME04_chapter06_fig05.jpg" style="zoom:80%;" />

- 译码 (Decode)
  - 组合逻辑组成
  - 根据RISC-V指令编码规则进行译码，产生不同的指令类型信息，操作数寄存器索引、立即数等
- CSR寄存器
  - 处理器内部寄存器，使用其自身地址编码空间
  - 访问采用专用的CSR读写指令，包括CSRRW、CSRRS、CSRRC、CSRRWI、CSRRSI、CSRRCI指令
- 整数通用寄存器组 (Integer-Regfile)
  - 可配置为16个 (RV32I)或者32个 (RV32E)
  - 可配置为用锁存器（Latch）实现，减小面积和功耗

##### 蜂鸟E203实现

> 共享一份实际的运算数据通路

<img src="..\fig\ME04\ME04_chapter06_fig07.jpg" style="zoom:80%;" />

- 普通ALU运算：主要负责普通ALU指令 (逻辑运算，加减法，移位等指令)的执行
- 访存地址生成：主要负责Load、Store和“A”扩展指令的地址生成
- 分支预测解析：主要负责Branch和Jump指令的结果解析和执行
- CSR读写控制：主要负责CSR指令的执行
- 多周期乘除法器：主要负责乘法和除法指令的执行

### 指令发射派遣

<img src="..\fig\ME04\ME04_chapter06_fig06.jpg" style="zoom:80%;" />

- 通过valid-ready握手模式将指令派遣给ALU
- 解决流水线冲突
  - 资源冲突
    - 通过valid-ready握手行为，阻塞指令派遣
  - 数据冲突
    - 蜂鸟E203的流水线中正在派遣的指令只可能与尚未执行完毕的长指令之间产生RAW和WAW相关性
- 每次派遣一条长指令，则会分配在OITF中分配一个表项
  - 每次派遣指令，将本指令的操作数索引同OITF各表项进行对比，存在冲突则阻塞指令派遣

### 交付与写回

#### 简介

- 大幅简化“交付”的硬件 (非E203)
  - 指令没有条件码，无须处理单条指令“取消”的情形
  - 所有的运算指令都不会产生异常，无须担心多周期指令写回结果后会产生错误异常
- 只需要实处现理两类流水线冲刷
  - 分支预测指令错误预测造成的后续指令流取消
  - 中断和异常造成的后续指令流取消

#### E203交付硬件实现

<img src="..\fig\ME04\ME04_chapter06_fig08.jpg" style="zoom:80%;" />

- 分支预测指令的处理
  - 预测失败则进行流水线冲刷，产生新的PC地址
- 中断与异常
- 多周期长指令
  - 先交付，后写回
  - 乘除法等运算错误，不产生异常
  - Load、Store等错误，作为异步异常处理

#### E203写回硬件实现

<img src="..\fig\ME04\ME04_chapter06_fig09.jpg" style="zoom:80%;" />

- 仅单周期指令
  - 顺序发射
  - 顺序执行
  - 顺序写回
- 仅长周期指令 (不同的执行单元)
  - 顺序发射
  - 乱序执行
  - 顺序写回
- 单周期指令和长周期
  - 顺序发射
  - 乱序执行
  - 乱序写回

### RISC-V架构特点

- 可配置的通用寄存器组
  - 通用寄存器个数
  - 通用寄存器宽度
  - 浮点寄存器组
- 规整的指令编码
  - 通用寄存器索引位置不变
- 简洁的存储器访问指令
  - Load & Store
  - 仅支持小端格式
  - 不支持地址自增/自减模式
  - 采用松散存储器模型
- 高效的分支跳转指令
  - 2条无条件跳转指令 (jar&jarl)
  - 6条带条件跳转指令 (单条指令完成比较与跳转)
  - 采用默认的静态分支预测机制：BTFN (Back Taken， Forward Not Taken)

## 存储系统

### RISC-V架构的存储器访问

#### 对于存储器访问指令的简化

- RISC-V的简化硬件哲学，对于存储器访问指令而言，通过如下特点大幅简化硬件实现
  - 仅支持小端模式
  - 无地址自增自减模式
  - 无“一次读或写多个数据”指令

#### 存储器相关指令

- Load & Store指令
  - LH、LHU、LB、LBU、LW
  - SB、SH、SW
- “A”扩展指令
  - Atomic Memory Operation（AMO）指令
  - Load-Reserved和Store-Conditional指令
- Fence指令
  - Fence
  - Fence.I

#### E203存储器子系统的实现

<img src="..\fig\ME04\ME04_chapter06_fig10.jpg" style="zoom:80%;" />

- AGU (Address Generation Unit)

  - 存储器访问地址生成
  - 属于ALU的一个子单元，共享数据运算通路
  - 对于非对齐地址访问，产生异常
  - 通过ICB总线与LSU交互 (没有产生异常的情况)

- LSU (Load Store Unit)

  - 存储器访问控制模块
  - 两组输入ICB总线接口：AGU、EAI (高优先级)
  - 三组输出ICB总线接口：ITCM、DTCM、BIU
  - 通过写回接口将结果写回
  - 出现存储器访问错误，则传送异常给交付模块

- ITCM (Instruction Tightly Coupled Memory)

  <img src="..\fig\ME04\ME04_chapter06_fig11.jpg" style="zoom:80%;" />

  - 指令存储器
  - 64位单口SRAM，大小和基地址可配 (config.v)
  - IFU>LSU>外部访问 (优先级)

- DTCM (Instruction Tightly Coupled Memory)

  <img src="..\fig\ME04\ME04_chapter06_fig12.jpg" style="zoom:80%;" />

  - 数据存储器
  - 32位单口SRAM，大小和基地址可配 (config.v)
  - LSU>外部访问 (优先级)

## SoC系统

### HBird-E203-Soc简介

> 外设只保留I2C和UART

<img src="..\fig\ME04\ME04_chapter06_fig13.jpg" style="zoom:80%;" />

HBird-E203-SoC开源项目是以Freedom E310 SoC (SiFive公司开源项目)为蓝本，在其基础上进行二次开发成为蜂鸟E203配套的SoC，其中主要做了如下修改:

- 将其E31 Core替换成蜂鸟E203处理器核
- 将TileLink总线替换成蜂鸟E203处理器的ICB总线
- 保留所有外设IP，如UART、SPI和PWM等(直接使用其可综合的Verilog代码，无须使用Chisel语言进行编译转换)

#### 简介

<img src="..\fig\ME04\ME04_chapter06_fig14.jpg" style="zoom:80%;" />

- HCLIKGEN
  - 高速时钟生成，供给主体域
- CLINT
  - 实现RISC-V架构定义的标准Timer和软件中断功能
- PLIC
  - 平台中断控制器
- JTAG
  - 连接外部调试器与内部调试模块
- Debug模块
  - 用于支持外部JTAG通过该模块调试处理器核
- Quad-SPI Flash
  - 用于连接外部Flash的QSPI接口
- GPIO (32个)
- QSPI (2个)
- UART (2个)
- PWM (3个)
- 常开域
  - LCLCGEN：低速时钟
  - WatchDog：看门狗计时器
  - RTC：实时计数器
  - PMU：电源管理

### 自定义总线协议ICB

<img src="..\fig\ME04\ME04_chapter06_fig15.jpg" style="zoom:80%;" />

- ICB总线通道结构
  - 仅有两个独立的通道，读和写操作共
    用地址通道，共用结果返回通道
- ICB特性
  - 采用分离的地址和数据阶段
  - 采用地址区间寻址，支持任意主从数目
  - 支持地址非对齐的数据访问，使用字节掩码 (Write Mask)来控制部分写操作
  - 支持多个滞外交易 (Multiple Outstanding Transaction)
  - 非常易于添加流水线级数以获得高频的时序
  - 每个读/写操作都会在地址通道上产生地址
  - 不支持乱序返回乱序完成，反馈通道必须按顺序返回结果

## 开发环境