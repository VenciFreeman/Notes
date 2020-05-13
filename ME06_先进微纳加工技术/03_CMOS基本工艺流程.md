# CMOS基本工艺流程

[TOC]

## **硅晶**

<img src=" ../fig/ME06/ME06_chapter03_fig01.jpg" style="zoom:50%;" />

- 轻p型掺杂外延层 (epi)的纯硅晶片 (重掺杂)
- 外延层用于为设备提供清洁层，并防止CMOS晶体管闩锁效应

## **浅沟道形成**

> Shallow Trench Formation

<img src=" ../fig/ME06/ME06_chapter03_fig02.jpg" style="zoom:125%;" />

### 生长缓冲氧化层

> Grow Pad Oxide

- 硅高温热氧化，在表面生长出非常薄的 (~200Å)二氧化硅 (SiO~2~)层
- 将作为硅和后续氮化硅层之间的应力缓冲层

### 沉积氮化硅

> Deposit Silicon Nitride

- 使用化学气相沉积法沉积一层氮化硅 (Si~3~N~4~，~2500Å)
- 将在沟槽形成期间用作抛光的停止层

### 描绘沟道的图形化光刻胶

> Pattern Photoresist for Definition of Trenches

- 过程中最关键的图案化步骤之一
-  旋涂，曝光和显影0.5-1.0 μm的光刻胶

### 蚀刻氮化物和缓冲氧化物

> Etch Nitride and Pad Oxide

- 利用含氟 (或其他含卤素族)气体的反应离子刻蚀 (RIE)

### 蚀刻硅中的沟槽

> Etch Trenches in Silicon

- 使用利用氟化物的反应离子刻蚀
- 定义晶体管有效区域

### 去除光刻胶

> Remove Photoresist

- 使用氧等离子体蚀刻掉光刻胶层

### 用氧化物填充沟槽

> Fill Trenches with Oxide

- 沉积LPCVD氧化物层以保形填充沟槽
  - 该氧化物将防止电路中晶体管之间的“串扰”
  - 1 μm以上采用局部氧化，但这种方法会让有源区减小

<img src=" ../fig/ME06/ME06_chapter03_fig03.jpg" style="zoom:50%;" />

- 氧化消耗硅
- SiO~2~的体积约为Si的两倍
- 氧化物在Si表面下约0.46倍T~OX~回退

#### 鸟喙

<img src=" ../fig/ME06/ME06_chapter03_fig04.jpg" style="zoom:50%;" />

### 抛光沟槽氧化物

> Polish Trench Oxide

- 使用化学机械抛光 (CMP)去除表面氧化物
  -  CMP工艺设计为在氮化硅层后停止，进行表面平整化

### 去除氮化硅

> Remove Silicon Nitride

- 使用热磷酸 (H~3~PO~4~)进行湿法蚀刻，完成浅沟槽隔离 (STI)的形成

## **阱形成**

> Well Formation

<img src=" ../fig/ME06/ME06_chapter03_fig05.jpg" style="zoom:125%;" />

- 掺杂硼形成p阱，掺杂磷砷形成n阱
- n阱做pmos，p阱做nmos

### N阱形成

#### 涂覆N阱图形化光刻胶

> Pattern Photoresist for N-Well Formation

- 非关键掩模层
- 利用较厚的光刻胶来阻挡注入

#### 掺杂N阱

> Implant N-Well

- 重磷离子注入 (高能量)会为PMOS晶体管创建局部N型区域

#### 剥离N阱光刻胶

> Strip P-Well Photoresist

### P阱形成

#### 涂覆P阱图形化光刻胶

> Pattern Photoresist for P-Well Formation

- 非关键掩模层
- 利用较厚的光刻胶来阻挡注入

#### 掺杂P阱

> Implant P-Well

- 重硼离子注入 (高能量)会为NMOS晶体管创建局部P型区域

#### 剥离P阱光刻胶

> Strip N-Well Photoresist

### 退火阱注入

> Anneal Well Implants

- 修复注入对硅表面造成的损坏并电激活掺杂剂

-  使掺杂剂更深一些，但是使用快速热处理可以最大程度地减少掺杂剂扩散

## **栅形成**

> Gate Formation

<img src=" ../fig/ME06/ME06_chapter03_fig06.jpg" style="zoom:125%;" />

### 生长牺牲氧化层

> Grow Sacrificial Oxide

- 约25nm厚的氧化层，生长在硅表面，以减小表面缺陷

### 移除牺牲氧化层

> Grow Sacrificial Oxide

- 立即通过氢氟酸湿法去除牺牲氧化层，留下光滑的表面

### 生长栅氧

> Grow Gate Oxide

- 工艺中最关键的一步。生长非常薄 (20-100 Å)的氧化物层
- 该氧化物层将用作两个晶体管的栅极介电层
  - 必须非常干净，并生长到非常精确的厚度 (±1Å)

### 沉积多晶硅

> Deposit Polysilicon

- 使用LPCVD沉积多晶硅至150-300nm的厚度

### 图案化光刻胶描绘栅电极

> Pattern Photoresist to Define Gate Electrodes

- 工艺中最关键的图案化步骤
  - 多晶硅栅极长度的精确尺寸是晶体管开关速度的一阶决定因素
  - 由于该层的关键特性，因此使用了技术最先进的构图系统 (即DUV)以及比正常光刻胶薄的光刻胶

### 蚀刻多晶硅和剥离光刻胶

> Etch Polysilicon and Strip Resist

- 使用氟化学的反应性离子蚀刻
- 完成“门堆叠”的形成

### 氧化多晶硅

> Oxidize Polysilicon

- 生长在多晶硅顶部的薄层氧化物作为多晶硅和氮化硅间的缓冲层

<img src=" ../fig/ME06/ME06_chapter03_fig07.jpg" style="zoom:80%;" />

## **源/漏形成**

> Source/Drain Formation

<img src=" ../fig/ME06/ME06_chapter03_fig08.jpg" style="zoom:125%;" />

### NMOS

#### 用于NMOS晶体管尖端注入的图案化光刻胶

> Pattern Photoresist for NMOS Transistor Tip Implant

#### NMOS晶体管尖端注入

> NMOS Transistor Tip Implant

- 砷离子的及浅 (低能量)和低剂量的注入开始形成NMOS晶体管的源极和漏极
- “尖端”将用于减少栅极区域附近的热电子效应

#### 剥离光刻胶

> Strip Photoresist

### PMOS

#### 用于PMOS晶体管尖端注入的图案化光刻胶

> Pattern Photoresist for PMOS Transistor Tip Implant

#### PMOS晶体管尖端注入

> PMOS Transistor Tip Implant

- BF~2~离子的及浅 (低能量)和低剂量的注入开始形成PMOS晶体管的源极和漏极
- “尖端”将用于减少栅极区域附近的热电子效应

#### 剥离光刻胶

> Strip Photoresist

### 沉积氮化硅层

> Deposit Silicon Nitride Layer

- 使用化学气相沉积，厚度120-180 nm

### 蚀刻氮化物以形成间隔物侧壁

> Etch Nitride to Form Spacer Sidewalls

- 使用精确控制的RIE蚀刻，从水平表面去除薄的氮化物，但保留间隔物侧壁。
- 这些侧壁将精确地限定形成晶体管源极和漏极的注入区域

### NMOS

#### NMOS晶体管源/漏注入的图案化光刻胶

> Pattern Photoresist for NMOS Transistor Source/Drain Implant

- 隔离物在栅极区域附近遮盖了注入

- 剥离光刻胶并退火

#### NMOS晶体管源极/漏极注入

> NMOS Transistor Source/Drain Implant

- 浅层和高剂量砷离子注入完成了重掺杂NMOS晶体管源极和漏极的形成
-  隔离物在栅极区域附近遮盖了植入物

#### 剥离光刻胶

> Strip Photoresist

### PMOS

#### PMOS晶体管源/漏注入的图案化光刻胶

> Pattern Photoresist for PMOS Transistor Source/Drain Implant

#### PMOS晶体管源极/漏极注入

> PMOS Transistor Source/Drain Implant

- 浅层和高剂量BF~2~离子注入完成了重掺杂PMOS晶体管源极和漏极的形成
-  隔离物在栅极区域附近遮盖了植入物

#### 剥离光刻胶

> Strip Photoresist

### 退火

> Anneal

- 使用快速热退火实际上消除了掺杂剂在浅源极和漏极中的迁移。
- 电子设备已完全成型，剩下的就是将它们连接在一起

## **硅化物形成**

> Sillicide Formation

<img src=" ../fig/ME06/ME06_chapter03_fig09.jpg" style="zoom:125%;" />

### 剥离表面氧化物

> Strip Surface Oxides

- 快速浸入HF以暴露源极，栅极和漏极区域中的裸露硅

<img src=" ../fig/ME06/ME06_chapter03_fig10.jpg" style="zoom:80%;" />

### 沉积钛

> Deposit Titanium

- 在整个晶圆表面上溅射一层钛薄层 (200-400 Å)

### 钛硅化合物形成

> itanium Silicide Formation

- 在800℃的氮气中进行快速热处理会导致钛与硅发生反应，从而形成硅化钛，并使两者接触
- 在其他区域，钛保持不变
- 该过程使硅化物与暴露的硅完美对准，称为自对准工艺

### 钛蚀刻

> Titanium Etch

- 通过湿蚀刻去除未反应的钛
- 保留硅化钛
- TiSi~2~在硅和金属之间提供欧姆接触

## **第一互连层**

> 1st Interconnect Layer

<img src=" ../fig/ME06/ME06_chapter03_fig11.jpg" style="zoom:125%;" />

### 沉积BPSG

> Deposit BPSG

- 通过CVD沉积掺杂有少量硼和磷的二氧化硅
  - 厚度约为1μ
  - 提升薄层的流动能力
  - 防止污染
  - 使器件与第一金属层电绝缘

### 抛光BPSG

> Polish BPSG

- 使用CMP (化学机械抛光)在BPSG层上获得平坦的表面
- 如果不去除，则来自下面形貌的表面上的凸块将对后续的光刻步骤造成问题，并降低金属步骤的覆盖率

### 图案化光刻胶以定义接触

> Pattern Photoresist to Define Contacts

### 触点蚀刻

> Contact Etch

- 使用氟化合物细致设计的RIE蚀刻
- 实现垂直侧壁

### 去除光刻胶

> Strip Photoresist

### 氮化钛沉积

> Titanium Nitride Deposition

- TiN的厚度约为200Å
- 将帮助随后的钨层粘附到氧化物上

### 钨沉积

> Tungsten Deposition

- 钨可以保形地沉积 (通过CVD)并可以填充接触孔
- 厚度必须至少为触点直径的一半

### 抛光钨

> Polish Tungsten

- CMP用于去除表面钨
- 其余的钨形成“塞子”
- 表面上的氮化钛也被去除

<img src=" ../fig/ME06/ME06_chapter03_fig12.jpg" style="zoom:80%;" />

### 沉积第一金属层

> Deposit Metal 1 Layer

- 每个互连层实际上是不同层的三明治结构
- 通过溅射沉积膜

### 第一金属层互连的图案化光刻胶

> Pattern Photoresist for Metal 1 Interconnects

### 蚀刻第一金属层

> Etch Metal 1

- 利用氯化合物的RIE蚀刻
- 由于存在多个不同的金属层，因此需要多个蚀刻步骤

### 去除光刻胶

> Strip Photoresist

- 第一互连层完成

<img src=" ../fig/ME06/ME06_chapter03_fig13.jpg" style="zoom:80%;" />

## 第2至第n互连层

> 2nd throught Nth Interconnect Layer

<img src=" ../fig/ME06/ME06_chapter03_fig14.jpg" style="zoom:125%;" />

### 沉积IMD1

> Deposit IMD1

- 使用CVD沉积未掺杂的二氧化硅，并蚀刻以填充金属线之间 (约1微米)
- 该层将金属层彼此电绝缘

### 抛光IMD1

> Polish IMD1

- 化学机械抛光用于在IMD层上实现平坦表面
- 如果表面粗糙，则来自下面形貌的表面上的凸块将对后续的光刻造成问题，并降低金属台阶覆盖率

### 图案化光刻胶以定义通孔

> Pattern Photoresist to Define Vias

- 通孔是IMD层中的接触孔，可实现金属层之间的电气通路

### 通孔刻蚀

> Via Etch

- 经过精心设计的RIE蚀刻，使用氟化合物获得垂直侧壁

### 去除光刻胶

> Strip Photoresist

### 沉积氮化钛和钨

> Deposit Titanium Nitride and Tungsten

- 与第一互连层相同

### 抛光钨

> Polish Tungsten

<img src=" ../fig/ME06/ME06_chapter03_fig15.jpg" style="zoom:80%;" />

### 沉积第二金属层

> Deposit Metal 2

- 后续的金属堆叠类似于Metal1
- 但随着其运行时间更长且载有更多电流，其厚度和宽度趋于增加

### 第二金属层互连的图案化光刻胶

> Pattern Photoresist for Metal 2 Interconnects

- 相邻的金属层彼此垂直地构图，以使各层之间的电感耦合最小化 (在横截面图中未显示)

### 蚀刻第二金属层

> Etch Metal 2

- 利用氯化合物的RIE蚀刻
- 由于存在多个不同的金属层，因此需要多个蚀刻步骤

### 去除光刻胶

> Strip Photoresist

- 第二互连层完成

## **钝化**

> (芯片表面保护) Passivation

<img src=" ../fig/ME06/ME06_chapter03_fig16.jpg" style="zoom:125%;" />

### 沉积钝化层

> Deposit Passivation Layer

- 钝化的类型很多 (氮化硅，氮氧化硅，聚酰亚胺等)
- 目的是保护整个电路免受刮擦，污染和潮湿

### 图案化钝化层

> Pattern Passivation Layer

- 聚酰亚胺钝化是可光定义的
-  其他钝化层需要图案化的光刻胶，然后进行蚀刻步骤
- 焊盘开口允许芯片接电

<img src=" ../fig/ME06/ME06_chapter03_fig17.jpg" style="zoom:80%;" />