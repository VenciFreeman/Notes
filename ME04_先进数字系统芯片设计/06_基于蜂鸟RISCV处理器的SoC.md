---
- 掌握RISCV处理器基本原理
- 掌握基于RISCV的SoC原理和工作模式
- 熟悉基本芯片主要模块原理和工作模式(I2C)
- 独立设计SoC模块，完成模块在SoC中的集成与仿真(DMA控制器)
---

# 基于蜂鸟RISCV处理器的SoC

[TOC]

## 简介

### 指令集

> Instruction Set Architecture

|     CPU架构     | IBM 701 | CDC 6600 |  IBM 360  | DEC PDP-8 | Intel 8008 |   Motorola 6800    |      DEC VAX      | Inerl 8086 |
| :-------------: | :-----: | :------: | :-------: | :-------: | :--------: | :----------------: | :---------------: | :--------: |
|  **诞生时间**   |  1953   |   1963   |   1964    |   1965    |    1972    |        1974        |       1977        |    1978    |
| **Intel 80386** | **ARM** | **MIPS** | **SPARC** | **Power** | **Alpha**  | **HP/Intel IA-64** | **AMD64 (EMT64)** | **RISCV**  |
|      1985       |  1985   |   1985   |   1987    |   1992    |    1992    |        2001        |       2003        |    2010    |

### RISCV

- 2010年发源于加州大学伯克利分校
  - 不受现有处理器架构复杂性和相关知识产权的限制
  - 全新的，简单且开发免费的指令集架
- 目标
  - 完全开放，可自由使用 (包括商用)
  - 成为一种真正适合软件实现且稳定的标准指令集架构

### 深入理解ISA

> 介于软件与CPU核心之间

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
|     RV64I      |     59     |   64位地址空间与整数指令及一部分32位的整数指令<用于服务器>   |
|     RV128I     |     71     |       128位地址空间与整数指令及一部分64位和32位的指令        |
| **扩展指令集** | **指令数** |                           **描述**                           |
|       M        |     8      |                整数乘法与除法指令 <图像处理>                 |
|       A        |     11     | 存储器原子 (Atomic)操作指令和Load-Reserved/Store-Conditional指令 <较少> |
|       F        |     26     |                   单精度 (32 bit)浮点指令                    |
|       D        |     26     |          双精度 (64 bit)浮点指令，必须支持F扩展指令          |

### RISC-V实现简介

- 架构
  - RISC-V是一种开放的指令集架构，而不是一款具体的处理器。任何组织与个人均可以依据RISC-V架构设计实现自己的处理器，只要是依据RISC-V标准设计的处理器，都可称为RISC-V处理器
- 微架构
  - 自RISC-V架构诞生以来，已经出现了数十个版本的RISC-V架构处理器，有开源免费的，也有商业公司开发用于内部项目的，还有商业IP公司开发的RISCV处理器IP

#### 当前主要开源RISCV处理器

- Rocket Core (开源 <最早，但效果不好>)
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
  - e203_srams，片上SRAM模块顶层
    - e203_itcm_ram，ITCM指令紧耦合存储器
    - e203_dtcm_ram，DTCM数据紧耦合存储器

### 流水线结构

> 严格来说，蜂鸟E203是一个变长流水线结，是非严格意义的二级流水线结构 

- 本次实验中
  - EAI不需要使用
  - Long-Pipes在不用乘法时也不需要使用

<img src="..\fig\ME04\ME04_chapter06_fig02.jpg" style="zoom:80%;" />

- 流水线的**第一级**为"取指" (由IFU完成)
- "译码" (由EXU中完成)、"执行" (由EXU中完成)和"写回" (由WB完成)，它们均处于同一个时钟周期，位于流水线的**第二级**
- "访存" (由LSU完成)阶段处于EXU之后的**第三级**流水线，但是LSU写回的结果仍然需要通过WB模块写回通用寄存器组

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

> 取值阶段的瓶颈就是新PC的生成

##### Mini-Decode

- 指令16位还是32位
  - 16位PC+2
  - 32位PC+4
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

- ICB总线：ITCM (64位) <指令是16/32位，取64位防止跨边界，且效率更高>，BIU (32位)
- 非对齐指令取址：采用剩余缓存 (Leftover Buffer)

### 执行单元

#### 简介

- 执行是处理器微架构的中枢核心阶段
- RISC-V架构追求简化硬件的哲学，具体对于执行 (包括译码)而言，RISC-V架构的如下特点可大幅简化其硬件实现
  - 整数指令都是两个操作数
  - 规整的指令编码格式
  - 精简的指令个数
  - 紧凑的16位指令
    - 占空间更小，存储的指令更多

#### 架构

<img src="..\fig\ME04\ME04_chapter06_fig04.jpg" style="zoom:80%;" />

- 将IFU通过IR寄存器发送给EXU的指令进行译码和派遣
- 通过译码出的操作数寄存器索引 (Index)读取Regfile
- 通过OITF维护指令的数据相关性
- 将指令派遣给不同的运算单元执行 (ALU、Long-Pipes、LSU及EAI)
  - ALU进行加减、移位与逻辑操作
- 将指令交付
- 将指令运算的结果写回Regfile (WB Arb)

#### 实现

- 寄存器堆
- Memory 

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
  - **分支预测**指令错误预测造成的后续**指令流取消**
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
  - Atomic Memory Operation (AMO)指令
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

  - 紧耦合指令存储器
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
- ~~Quad-SPI Flash~~
  - ~~用于连接外部Flash的QSPI接口~~
- ~~GPIO (32个)~~
- ~~QSPI (2个)~~
- ~~UART (2个)~~
- ~~PWM (3个)~~
- ~~常开域~~
  - LCLCGEN：低速时钟
  - WatchDog：看门狗计时器
  - RTC：实时计数器
  - PMU：电源管理

### 内存映射

#### SoC地址分配

|     总线分组     |           组件            |        地址区间         |                             描述                             |
| :--------------: | :-----------------------: | :---------------------: | :----------------------------------------------------------: |
|     Core直属     |           CLINT           | 0x0200_0000~0x0200_FFFF |              核本地中断控制，模块寄存器地址区间              |
|     Core直属     |           PLIC            | 0x0C00_0000~0x0CFF_FFFF |              平台级中断控制，模块寄存器地址区间              |
|     Core直属     |           IMCM            | 0x8000_0000~0x8001_FFFF |                         ITCM地址区间                         |
|     Core直属     |           DTCM            | 0x9000_0000~0x8001_FFFF |                         DTCM地址区间                         |
| 系统存储总线接口 |       Debug Module        | 0x0000_0000~0x0000_0FFF |       主要用于调试器使用，普通软件程序不应该使用此区间       |
| 系统存储总线接口 |            ROM            | 0x0000_1000~0x0000_1FFF | 开源的E203项目由于是FPGA原型，因此Mask-ROM代码为一行模型/在本SoC中考虑将其固化成为逻辑，而不是真正使用ROM IP |
| 系统存储总线接口 | Off-Chip QSPI0 Flash Read | 0x2000_0000~0x3FFF_FFFF |                  外部SPI Flash只读地址区间                   |
| 私有设备总线接口 |         Always-On         | 0x1000_0000~0x1000_7FFF |               包含PMU, RTC, WatchDog, LCLKGEN                |
| 私有设备总线接口 |          HCLKGEN          | 0x1000_8000~0x1000_8FFF |                       高速时钟生成模块                       |
|                  |           GPIO            | 0x1001_2000~0x1001_2FFF |                         GPIO地址区间                         |
|                  |           UART0           | 0x1001_3000~0x1001_3FFF |                    第一个UART模块地址区间                    |
|                  |           QSPI0           | 0x1001_4000~0x1001_4FFF |                    第一个QSPI模块地址区间                    |
|                  |           PWM0            | 0x1001_5000~0x1001_5FFF |                    第一个PWM模块地址区间                     |
|                  |           UART1           | 0x1002_3000~0x1002_3FFF |                    第二个UART模块地址区间                    |
|                  |           QSPI1           | 0x1002_4000~0x1002_4FFF |                    第二个QSPI模块地址区间                    |
|                  |           PWM1            | 0x1002_5000~0x1002_5FFF |                    第二个PWM模块地址区间                     |
|                  |           QSPI2           | 0x1003_4000~0x1003_4FFF |                    第三个QSPI模块地址区间                    |
|                  |           PWM2            | 0x1003_5000~0x1003_5FFF |                    第三个PWM模块地址区间                     |
|                  |        I2C Master         | 0x1004_2000~0x1004_2FFF |                          IC2 Master                          |

\* 其他地址区间：上表中未用到的地址区间，均为写忽略，读返回0

### 自定义总线协议ICB

<img src="..\fig\ME04\ME04_chapter06_fig15.jpg" style="zoom:80%;" />

- ICB总线通道结构
  - 仅有两个独立的通道，读和写操作共用地址通道，共用结果返回通道
- ICB特性
  - 采用分离的地址和数据阶段
  - 采用地址区间寻址，支持任意主从数目
  - 支持地址非对齐的数据访问，使用字节掩码 (Write Mask)来控制部分写操作
  - 支持多个滞外交易 (Multiple Outstanding Transaction)
  - 非常易于添加流水线级数以获得高频的时序
  - 每个读/写操作都会在地址通道上产生地址
  - 不支持乱序返回乱序完成，反馈通道必须按顺序返回结果

#### ICB总线信号

|   通道   |            功能            | 方向 | 宽度 |    信号名     |                介绍                |
| :------: | :------------------------: | :--: | :--: | :-----------: | :--------------------------------: |
| 命令通道 | 主设备向从设备发起读写请求 | 输出 |  1   | icb_cmd_valid |   主设备向从设备发送读写请求信号   |
| 命令通道 | 主设备向从设备发起读写请求 | 输出 |  DW  | icb_cmd_addr  |              读写地址              |
| 命令通道 | 主设备向从设备发起读写请求 | 输出 |  1   | icb_cmd_read  |          读或写操作的指示          |
| 命令通道 | 主设备向从设备发起读写请求 | 输出 |  DW  | icb_cmd_wdata |            写操作的数据            |
| 命令通道 | 主设备向从设备发起读写请求 | 输出 | DW/8 | icb_cmd_wmask |          写操作的字节掩码          |
| 命令通道 | 主设备向从设备发起读写请求 | 输入 |  1   | icb_cmd_ready |   从设备向主设备返回读写接受信号   |
| 反馈通道 | 从设备向主设备返回读写结果 | 输入 |  1   | icb_rsp_valid | 从设备向主设备发送读写反馈请求信号 |
| 反馈通道 | 从设备向主设备返回读写结果 | 输入 |  DW  | icb_rsp_rdata |            读反馈的数据            |
| 反馈通道 | 从设备向主设备返回读写结果 | 输入 |  1   |  icb_rsp_err  |        读或写反馈的错误标志        |
| 反馈通道 | 从设备向主设备返回读写结果 | 输出 |  1   | icb_rsp_ready | 主设备向从设备返回读写反馈接受信号 |

#### 写操作同一周期返回结果

- 主设备向从设备通过ICB的Command Channel发送写操作请求 (icb_cmd_read为低)
  - 从设备立即接收该请求 (icb_cmd_ready为高)
- 从设备在同一个周期返回读结果且结果正确 (icb_rsp_err为低)
  - 主设备立即接收该结果 (icb_rsp_ready为高)

<img src="..\fig\ME04\ME04_chapter06_fig24.jpg" style="zoom:80%;" />

#### 读操作下一周期返回结果

- 主设备向从设备通过ICB的Command Channel发送读操作请求 (icb_cmd_read为高)
  - 从设备立即接收该请求 (icb_cmd_ready为高)
- 从设备在下一个周期返回读结果且结果正确 (icb_rsp_err为低)
  - 主设备立即接收该结果 (icb_rsp_ready为高)

<img src="..\fig\ME04\ME04_chapter06_fig25.jpg" style="zoom:80%;" />

#### 写操作下一周期返回结果

- 主设备向从设备通过ICB的Command Channel发送写操作请求 (icb_cmd_read为低)
  - 从设备立即接收该请求 (icb_cmd_ready为高)
- 从设备在下一个周期返回读结果且结果正确 (icb_rsp_err为低)
  - 主设备立即接收该结果 (icb_rsp_ready为高)

<img src="..\fig\ME04\ME04_chapter06_fig26.jpg" style="zoom:80%;" />

#### 读操作四个周期返回结果

- 主设备向从设备通过ICB的Command Channel发送读操作请求 (icb_cmd_read为高)
  - 从设备立即接收该请求 (icb_cmd_ready为高)
- 从设备在四个周期后返回读结果且结果正确 (icb_rsp_err为低)
  - 主设备立即接收该结果 (icb_rsp_ready为高)

<img src="..\fig\ME04\ME04_chapter06_fig27.jpg" style="zoom:80%;" />

#### 写操作四个周期返回结果

- 主设备向从设备通过ICB的Command Channel发送写操作请求 (icb_cmd_read为低)
  - 从设备立即接收该请求 (icb_cmd_ready为高)
- 从设备在四个周期后返回结果且结果正确 (icb_rsp_err为低)
  - 主设备立即接收该结果 (icb_rsp_ready为高)

<img src="..\fig\ME04\ME04_chapter06_fig28.jpg" style="zoom:80%;" />

#### 连续四个读操作均四个周期返回结果

- 主设备向从设备通过ICB的Command Channel连续发送四个读操作请求 (icb_cmd_read为高)
  - 从设备均立即接收该请求 (icb_cmd_ready为高)
- 从设备在四个周期后连续返回四个读结果
  - 其中前三个结果正确 (icb_rsp_err为低)
  - 第四个结果错误 (icb_rsp_err为高)
  - 主设备均立即接收此四个结果 (icb_rsp_ready为高)

<img src="..\fig\ME04\ME04_chapter06_fig29.jpg" style="zoom:80%;" />

#### 连续四个写操作均四个周期返回结果

- 主设备向从设备通过ICB的Command Channel连续发送四个写操作请求 (icb_cmd_read为低)
  - 从设备均立即接收该请求 (icb_cmd_ready为高)
- 从设备在四个周期后连续返回四个写结果
  - 其中前三个结果正确 (icb_rsp_err为低)
  - 第四个结果错误 (icb_rsp_err为高)
  - 主设备均立即接收此四个结果 (icb_rsp_ready为高)

<img src="..\fig\ME04\ME04_chapter06_fig30.jpg" style="zoom:80%;" />

#### 读写混合

- 主设备向从设备通过ICB的Command Channel相继连续发送三个读和写操作请求
- 从设备立即接收了第一个和第三个请求
  - 第二个请求第一个周期并没有立即接受 (icb_cmd_ready为低)
  - 因此主设备一直将地址控制和写数据信号保持不变，直到下一周期该请求被从设备接受 (icb_cmd_ready为高)
- 从设备对于第一个和第二个请求都是在同一个周期就返回结果且被主设备立即接受
  - 对于第三个请求则是在下一个周期才返回结果
  - 主设备还没有立即接受 (icb_rsp_ready为低)
  - 因此从设备一直将返回信号保持不变，直到下一周期该返回结果被主设备接受

<img src="..\fig\ME04\ME04_chapter06_fig31.jpg" style="zoom:80%;" />

#### ICB总线硬件实现

##### 一主多从

- 通过地址区间选择分发通道
- 支持多个滞外交易

##### 多主一从

- 多输入进行仲裁 (轮询或优先级)
- 支持多个滞外交易

<img src="..\fig\ME04\ME04_chapter06_fig17.jpg" style="zoom:80%;" />

- 通过“一主多从”和“多主一从”进行有效组合

<img src="..\fig\ME04\ME04_chapter06_fig18.jpg" style="zoom:80%;" />

### BIU

> Bus Interface Unit

- BIU主要负责接受来自IFU和LSU单元的存储器访问请求，并使用标准的ICB接口，通过判断其访问的地址区间来访问外部不同接口
  - 快速IO接口
  - 私有外设接口
  - 系统存储接口
  - CLINT接口
  - PLIC接口

<img src="..\fig\ME04\ME04_chapter06_fig19.jpg" style="zoom:80%;" />

#### BIU微架构

- 两组输入：IFU、LSU (高优先级)
- 通过Ping-Pong Buffer切断外界与处理器内部之间的时序路径
- ICB汇合和分发模块的FIFO深度默认配置为1
- 若IFU访问了设备区间，则直接通过反馈通道返回错误标志

<img src="..\fig\ME04\ME04_chapter06_fig20.jpg" style="zoom:80%;" />

### 中断异常概述

<img src="..\fig\ME04\ME04_chapter06_fig21.jpg" style="zoom:80%;" />

- 中断机制和异常机制即在中断和异常发生时，处理器将暂停当前正在执行的程序，转而执行中断和异常处理程序，返回时处理器恢复之前被执行的程序
- 由于对于处理器而言中断和异常的处理机制基本上一样，所以合称广义异常
  - 同步异常，其原因可以精确定位到某一条执行指令
  - 异步异常，每次发生时指令的PC可能不一样，例如中断便时一种异步异常
    - 精确异步异常，在响应异常后的处理器状态能够精确反映为某一条指令的边界
    - 非精确异步异常，在响应异常后的处理器状态无法精确反映为某一条指令的边界

#### RISC-V的中断

- External Interrupt
  - 中断源自处理器外部，如GPIO等
  - PLIC (Platform Level Interrupt Controller)用于多个外部中断源的管理
  - mie寄存器可对其进行屏蔽和mip寄存器可反映其等待标志
- Timer Interrupt
  - 中断源自计时器
  - 中断是否产生由64-bit 寄存器mtime和mtimecamp的值相比较而决定 (CLINT模块)
  - mie寄存器可对其进行屏蔽和mip寄存器可反映其等待标志
- Software Interrupt
  - 中断源自软件触发
  - 中断是否产生由msip的值决定 (CLINT模块)
  - mie寄存器可对其进行屏蔽和mip寄存器可反映其等待标志
- Debug Interrupt
  - 此中断专用于实现调试器

#### RISC-V架构的中断优先级与中断嵌套

- 中断优先级：外部中断 > 软件中断 > 计时器中断
- 多个外部中断的优先级由PLIC控制
- RISC-V定义的默认硬件机制在进入异常后，中断会被全局关闭，无法响应新的中断，因此需要使用软件的方法或者用户实现自定义的硬件去支持中断嵌套功能
- 在中断嵌套的过程中，软件需要注意保存上下文和CSR相关寄存器至堆栈

##### RISC-V架构的中断和异常

|         类型          |       名称       |                             全称                             |                        描述                        |
| :-------------------: | :--------------: | :----------------------------------------------------------: | :------------------------------------------------: |
|          CSR          |      mtvec       | 机器模式异常入口基地址寄存器 (Machine Trap-Vector Base-Address Register) |              定义进入异常的程序PC地址              |
|          CSR          |      mcause      |       机器模式异常原因寄存器 (Machine Cause Register)        |                 反映进入异常的原因                 |
|          CSR          | mtval (mbadaddr) |      机器模式异常值寄存器 (Machine Trap Value Register)      |                 反映进入异常的信息                 |
|          CSR          |       mepc       |   机器模式异常PC寄存器 (Machine Exception Program Counter)   |               用于保存异常的返回地址               |
|          CSR          |     mstatus      |         机器模式状态寄存器 (Machine Status Register)         | mstatus寄存器中的MIE域和MPIE域用于反映中断全局使能 |
|          CSR          |       mie        | 机器模式中断使能寄存器 (Machine Interrupt Enable Registers)  |           用于控制不同类型中断的局部使能           |
|          CSR          |       mip        | 机器模式中断等待寄存器 (Machine Interrupt Pending Registers) |             反映不同类型中断的等待状态             |
| Memory address mapped |      mtime       |      机器模式计时器寄存器 (Machine-mode timer register)      |                   反映计时器的值                   |
| Memory address mapped |     mtimecmp     | 机器模式计时器比较值寄存器 (Machine-mode timer compare register) |                  配置计时器比较值                  |
| Memory address mapped |       msip       | 机器模式软件中断等待寄存器 (Machine-mode Software InterruptPending Register) |              用以产生或者清除软件中断              |
| Memory address mapped |       PLIC       |                     PLIC的所有功能寄存器                     |                PLIC的所有功能寄存器                |

#### E203处理器的中断接口

- 在处理器顶层接口中有4根中断输入信号，分别是软件中断、计时器中断、外部中断和调试中断
  - CLINT模块产生一根软件中断信号和一根计时器中断信号， 通给蜂鸟E203处理器
  - PLIC模块接入多个外部中断源将其仲裁后生成一根外部中断信号， 通给蜂鸟E203处理器
  - SoC层面的调试模块生成一根调试中断，通给蜂鸟E203处理器核
  - 所有的中断信号均由蜂鸟E203处理器核的交付模块进行处理

#### CLINT

> Core Local Interrupts Controller

- CLINT是一个存储器地址映射的模块，挂载在蜂鸟E203 BIU上
  - 软件中断：msip寄存器最低位，软件写1产生软件中断，写0清除该中断
  - 计时器中断：mtime ≥ mtimecmp时产生计时器中断，软件可改写mtimecmp的值 (大于mtime)来清除该中断
- 注：CLINT计时器根据低速输入节拍信号 (来自电源常开域)进行计时，上电后默认一直计数，可通过蜂鸟E203自定义CSR寄存器mcounterstop来关闭

|    地址     | 寄存器名称 |      功能描述      |
| :---------: | :--------: | :----------------: |
| 0x0200_0000 |    msip    |    生成软件中断    |
| 0x0200_4000 |  mtimecmp  | 配置计时器的比较值 |
| 0x0200_BFFB |   mtime    |   反映计时器的值   |

#### PLIC

> Platform Level Interrupt Controller

- PLIC是一个存储器地址映射的模块，挂载在蜂鸟E203 BIU上

<img src="..\fig\ME04\ME04_chapter06_fig22.jpg" style="zoom:80%;" />

| PLIC源中断号 |        来源         |
| :----------: | :-----------------: |
|      0       | 预留为表示没有中断  |
|      1       |       wdogcmp       |
|      2       |       rtccmp        |
|     3, 4     |    uart0, uart1     |
|   5, 6, 7    | qspi0, qspi1, qspi2 |
|    8...39    |   gpio0...gpio31    |
|   40---43    | pwm0cmp0...pwm0cmp3 |
|   44---47    | pwm1cmp0...pwm1cmp3 |
|   48---51    | pwm2cmp0...pwm2cmp3 |

## 开发环境

### 蜂鸟E203调试机制的实现

- 处理器对于运行于其上的软件程序提供调试能力是至关重要的
- 调试机制是个非常复杂的软硬件协作机制，软硬件的实现难度很大
- 对于处理器的调试功能而言，常用的两种是“交互式调试”和“追踪调试”
  - 交互式调试 (Interactive Debug)
    - 最常见的调试功能
    - 调试器软件 (如GDB)能够直接对处理器取得控制权，进而对其以一种交互方式进行调试
    - 缺点是对处理器的运行具有打扰性
  - 追踪调试 (Trace Debug)
    - 调试器只跟踪记录处理器核执行过的所有程序指令，而不会打断干扰处理器的执行过程
    - 相比交互式调试的实现难度更大，硬件开销也更大

<img src="..\fig\ME04\ME04_chapter06_fig23.jpg" style="zoom:80%;" />

- 蜂鸟E203的调试机制的硬件实现调试机制如下 (未支持跟踪调试)
  - 在调试主机上通过GDB设置某行程序的断点
  - 修改存储器中断点处PC地址的指令，将其替换为ebreak
  - 当执行到ebreak指令时，进入调试模式的异常处理程序 (一段在Debug-Rom中定义的固定程序)
  - 主机端的GDB软件一直在检测调试模块，得知处理器核已经停在了断点处时，便把对应的信息显示在GDB界面上
  - 若要读取某个寄存器的值，则通过GDB对调试模块下达命令
    - 调试模块便开始对处理器内核进行控制，将寄存器值读出，主机端GDB在监测调试模块状态时得知此信息，便显示在其界面上
  - 当希望退出调试模式，则可以调用dret指令来触发

- DTM (Debug Transport Module)
  - 在蜂鸟E203处理器中DTM主要是将JTAG标准接口转换成为内部的调试总线 (Debug Bus)
    - 主要是使用状态机对JTAG协议进行解析转换成调试总线
    - 由于DTM模块处于JTAG时钟域，与调试总线要访问的调试模块不属于同一个时钟域，因此需要被同步
- 调试模块 (Debug Module)
  - 实现了RISC-V调试文档“0.11版本”中定义的若干寄存器、Debug-ROM和Debug-RAM
    - 这些资源既可以被调试总线访问到，也可以被系统存储总线访问到
  - Debug-ROM包含了处理器进入调试模式下需要执行的异常处理程序
  - Debug-RAM主要在运行Debug-ROM中固定异常处理程序时作为数据段使用，用于存放
    一些临时数据和中间数据

#### 调试机制指令的实现

- ebreak：触发处理器进入异常模式 (调试模式)
- 调试中断一旦被接收，便会冲刷流水线，处理器PC跳转到0x800地址
  - CSR寄存器dpc的值更新为当前正在执行的指令PC
  - CSR寄存器dcsr的cause域值更新为引发进入调试模式的触发原因
- dret：触发处理器退出异常模式 (调试模式)
- 被当作一种跳转指令来执行，跳转PC为CSR寄存器dpc的值
- 将dcsr寄存器中的cause域清除

### RISC-V软件工具链

> RISC-V软件工具链由开源社区维护，可通过RISC-V基金会网站找到相关信息并下载

- riscv-tools (ISA Simulator and Tests)
  - riscv-isa-sim：基于C/C++开发的指令集模拟器“Spike”
  - riscv-openocd：基于OpenOCD的RISC-V调试器软件
  - riscv-opcodes：RISC-V操作码信息转换脚本
  - riscv-tests：一组RISC-V指令集测试用例
  - riscv-pk：RISC-V可执行程序运行环境软件，同时提供最简单的bootloader
- riscv-gnu-toolchain
  - riscv-gcc：GCC 编译器
  - riscv-binutils：二进制工具 (链接器，汇编器等)
  - riscv-gdb：GDB调试工具
  - riscv-glibc：GNU C标准库实现
  - riscv-newlib：开源C标准库，主要用于嵌入式系统
  - riscv-qemu：支持RISC-V 的QEMU模拟器

#### E203的测试平台

>在e200_opensource项目中创建了一个简单的由Verilog编写的TestBench测试平台

- riscv-tests是由RISC-V架构开发者维护的开源项目，包含一些测试处理器是否符合指令集架构定义的测试程序，均由汇编语言编写
- e200_opensource项目中riscv-tools 下的riscv-tests目录克隆了原始riscvtests项目，并在其基础上添加了更多测试用例，且生成更多log文

##### 主要功能

- 例化DUT文件，生成clock和reset信号
- 初始化ITCM
  - 根据运行命令解析出测试用例名称，并使用Verilog的readmemh函数读入相应的文件内容，然后使用其内容初始化ITCM
- 测试结果分析
  - 在运行结束后分析该测试用例执行结果，对x3寄存器的值进行判断，若其值为1，则通过测试，向终端输出PASS字样，否则输出FAIL字样

#### HBird-E-SDK

- HBird-E-SDK一个基于Linux环境的针对蜂鸟E203 SoC进行嵌入式软件开发的平台，是以SiFive公司开源的Freedom-E-SDK为蓝本，在其基础上进行的二次开发

```verilog
title= "bird-e-sdk"
bsp 					  // 存放板级支持包的目录
	hbird-e200 		// 存放蜂鸟E203的BSP文件
		env 				// 存放一些基本的支持性文件
		drivers 		// 存放底层设备驱动文件
		include 		// 存放一些头文件
		stubs 			// 存放移植newlib的底层桩函数
		tools 			// 存放一些工具脚本文件
software 				// 存放示例程序的源代码
 	hello_world 	// hello_world示例程序
	demo_gpio 		// GPIO示例程序
	demo_iasm 		// 内嵌汇编示例程序
 	dhrystone 		// Dhrystone跑分程序
 	coremark 			// Coremark跑分程序
 	FreeRTOS 			// FreeRTOS示例程序
prebuilt_tools 	// 存放工具链的目录
Makefile 				// 主Makefile文件
```

