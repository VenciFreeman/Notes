# 第十二章：先进封装技术：WLP与MCM

[TOC]

## **WLP的概念**

### 背景

- 半导体技术逐渐高密度化和高集成度化，芯片信号的传输量与日俱增，引脚数逐渐增加
- 封装行业逐渐由传统的
  - 双列直插式封装 (Dual Inline Package)
  - 小型封装 (Small Outline Package)
  - 引脚阵列封装 (Pin Grid Array)
- 逐步走向
  - 焊球阵列封装 (Ball Grid Array)
  - 芯片尺寸封装 (Chip Scale Package)
  - 倒装(Flip Chip)
  - 三维封装
- 现如今微电子产品的发展趋势
  - 高密度
  - 低成本
- 正是这些因素促进了晶圆级芯片尺寸封装的出现及发展

### 简介

- 以BGA技术为基础
  - 是一种经过改进和提高的CSP
  - 又称为圆片级芯片尺寸封装 (WL-CSP)
  - 由IBM公司在1964年为其360主机系统引入焊料凸点技术时出现并不断发展起来
- 描述
  - 以晶圆为加工对象
  - 在晶圆上同时对众多芯片进行封装 、老化 、测试 
  - 最后切割成单个器件
  - 可以直接贴装到基板或印刷电路板上
  - 使封装尺寸减小至IC 芯片的尺寸，生产成本大幅度下降

<img src="..\fig\ME01\ME01_chapter12_fig02.jpg" style="zoom:73%;" />

### 工艺概述

<img src="..\fig\ME01\ME01_chapter12_fig01.jpg" style="zoom:67%;" />

- 在晶圆阶段利用芯片较宽的划片槽，在周边构造互连 (通过增加薄膜再布线工艺和凸点制作工艺)，随后用玻璃、树脂等材料进行封装完成
- 主要结构包括
  - 首层聚合物层
  - 重布线层
  - 第二层聚合物层
  - 球下金属区 (新焊区)
  - 凸点

## **WLP与传统封装的比较**

### 概述

- 传统封装 (芯片级封装)是指将单个芯片从硅片上分离出来，再运输到柔性垫片、刚性基板或引线框架上，独立完成封装工序
  - 封装在划片之后
- 晶圆级封装以完整的硅片进行封装操作
  - 封装在划片之前

|   比较项目   |             传统封装             |               晶圆级封装                |
| :----------: | :------------------------------: | :-------------------------------------: |
|   封装步骤   |   先切割再对每一颗芯片进行封装   |         全部在晶圆片上进行封装          |
|   连线工艺   |       打线焊接 (Wire Bond)       |   重新布线及金属凸块 (Wafer bumping)    |
|   封装尺寸   |     大， 大约为芯片的4到10倍     |          小，与芯片的大小相同           |
|  外观引脚数  |               不限               |      目前适用于100条引脚以下的芯片      |
|     测试     |         需CP和FT两部测试         |        需CP测试，FT测试一般可省         |
|     成本     |      以每粒芯片计价，比较低      | 以每片晶圆计价，产量大/晶圆片大时有优势 |
|   材料选用   |         金线、引线框架等         |           光掩膜、铜、锡球等            |
|   设备投资   | 传统的打线机、塑封机等，相对较小 |         许多前端设备，相对较大          |
|   电气性能   |        已经发展到接近极限        |             有相当大的改善              |
| 工艺实施难度 |      技术相当成熟，实施容易      |      标准尚未制定，技术仍在发展中       |

### 优缺点

#### 优点

- 封装加工效率高，它以圆片形式的批量生产工艺进行制造；
- 具有倒装芯片封装的优点，即轻、薄、短、小
- 圆片级封装生产设施费用低，可充分利用圆片的制造设备，无须投资另建封装生产线
- 圆片级封装的芯片设计和封装设计可以统一考虑、同时进行，这将提高设计效率，减少设计费用
- 圆片级封装从芯片制造、封装到产品发往用户的整个过程中，中间环节大大减少，周期缩短很多，这必将导致成本的降低
- 圆片级封装的成本与每个圆片上的芯片数量密切相关，圆片上的芯片数越多，圆片级封装的成本也越低。圆片级封装是尺寸最小的低成本封装

#### 缺点

- 采用前工序设备设备费很贵
- 引出端限于芯片范围内，引出端数受到限制
- 对于低的圆片级再分布成品率和低的硅片凸点成品率，成本很高，特别是高成本的芯片
- 难以在硅片上测试和高温老化已知合格产品率 (KGD)

## **WLP的工艺技术**

### Georgia Tech

<img src="..\fig\ME01\ME01_chapter12_fig03.jpg" style="zoom:70%;" />

### TUB-IZM

<img src="..\fig\ME01\ME01_chapter12_fig04.jpg" style="zoom:70%;" />

### 圆片级封装工艺

#### 第一步：涂布第一层

- 涂布第一层聚合物薄膜 (Polymer Layer)，以加强芯片的钝化层 (Passivation)，起到应力缓冲的作用
  - 目前最常用的聚合物薄膜是光敏性聚酰亚胺 (Photo-sensitive Polymide)，简称PI，是一种负性胶
  - 早期的WLP选用BCB (Benzocyclobutene，苯丙环丁烯)作为重布线的聚合物薄膜
    - 低机械性能 (低断裂伸长率和拉伸强度)
    - 高工艺成本 (需要打底粘合层adhesion promoter)

<img src="..\fig\ME01\ME01_chapter12_fig05.jpg" style="zoom:70%;" />

#### 第二步：重布线层

- 重布线层 (RDL)的制作
  - 重布线层的目的是对芯片的铝焊区位置进行重新布局
  - 使新焊区满足对焊料球最小间距的要求，并使新焊区按照阵列排布
  - 常见的RDL材料是电镀铜辅以打底的钛、铜溅射层

<img src="..\fig\ME01\ME01_chapter12_fig06.jpg" style="zoom:70%;" />

#### 第三步：涂布第二层

- 涂布第二层聚合物薄膜 (Polymer Layer)，使原片表面平坦化并保护RDL层
  - 第二层Polymer经过光刻后开出新焊区的位置

#### 第四步：UBM

- UBM(Under Bump Metallization，球下金属层)的制作
  - 采用和RDL一样的工艺

#### 第五步：植球

- 焊料球的直径一般为250 μm
- 焊料球通过掩模版(以保证对齐)的开孔被放置于UBM上，最后将植球后的硅片放入回流炉，焊料球融化与UBM形成良好结合

### 几种不同的晶圆级封装

#### Ball on I/O

<img src="..\fig\ME01\ME01_chapter12_fig07.jpg" style="zoom:70%;" />

- 和典型的倒装工艺相类似
  - 焊球通过焊点下的金属层与铝盘直接相连
  - 或者焊球通过再布线层 (Redistribution Layer,RDL)与硅片芯片直接相连
- 对焊球的结构有所限制
  - 一般限制在焊球间距为0.5 mm的6×6的阵列结构中，以达到热循环可靠性的要求

#### 焊球置于RDL上

<img src="..\fig\ME01\ME01_chapter12_fig08.jpg" style="zoom:70%;" />

- 焊球置于重布线层 (RDL)上，并且焊球通过二层聚合物介质层与硅芯片相连
  - 这种结构中没有焊球下金属层
  - 两层聚合物作为钝化层和再布线层
  - 同于第一种结构，尽管两者都有再布线层
- 聚合物介质薄膜层置于焊球和硅衬底
  - 聚合物层能够作为缓冲层来降低由于温度变化所引起的PCB和硅的热失配所产生的热-机械应力
- 能够拓展到焊球间距为0.5 mm的12×12的焊球阵列

#### 添加UBM

- 添加球下金属层 (UBM)
  - UBM的添加增加了制造的成本和工艺的复杂性
  - 但可以提高结构的热力学性能

<img src="..\fig\ME01\ME01_chapter12_fig09.jpg" style="zoom:70%;" />

#### 铜柱结构

- 采用铜柱结构
  - 首先电镀铜柱
  - 接着用环氧树脂密封

<img src="..\fig\ME01\ME01_chapter12_fig10.jpg" style="zoom:70%;" />

### 核心技术

- 核心关键技术是**薄膜再布线工艺**和**凸点制作工艺**
  - 采用两层聚合物作为保护层和介质层，生产成本大幅降低
  - 芯片尺寸真正减小至IC芯片尺寸，将芯片封装与制造融为一体

#### 凸点制作技术

- 凸点制作是圆片级封装工艺过程的关键工序
  - 在晶圆片的焊区铝电极上形成凸点
  - 圆片级封装的凸点制作技术主要有
    - 预制焊球
    - 丝网印刷
    - 电镀 (WLP)
  - 每种方法各有优缺点，适用于不同的工艺要求，选择合适的凸点制作工艺非常重要
  - 在晶圆凸点的制作中，金属沉积占到全部成本的50%以上

##### 预制焊球和丝网印刷

- 预制焊球和丝网印刷的植球方式
  - 成本低
  - 质量高
  - 工艺稳定
- 这两种植球方式应用广泛
- 需要注意
  - 植球过程中，精度与重复精度尤为重要
    - 由于微球不粘贴和网板脱模不良等缺陷，使微球植球偏移或缺失，造成最终芯片成品率降低
    - 此类不合格的芯片一般废弃不用，造成极大的浪费

##### 补球技术

- 为提高芯片成品率，研究人员设计研发处理缺球和粘球等现象的设备补球机
  - 采用单针形式和针转移修复技术在植球晶圆进入回流焊炉前的阶段
  - 批量对植球晶圆进行补球等工作

|  失效项目  |         修复工艺         |
| :--------: | :----------------------: |
|    缺球    |       点胶 → 补球        |
|   球偏移   | 吸走多余球 → 点胶 → 补球 |
| 球大小错误 | 吸走多余球 → 点胶 → 补球 |
|    多球    |        吸走多余球        |

- 补球的技术路线
  - 晶圆盒放置到上料位，在供球和供胶机构上放入一定量的微球和助焊剂
  - 六轴机械手将晶圆取出放置在预定位机构上进行植球失效检测前的校准预定位
  - 晶圆被机械手传送到搭载平台上
  - 图像检测系统对晶圆进行检测和处理，计算晶圆植球失效类型和位置信息
  - 根据视觉检测的处理结果，四轴机械手上的去多球机构对晶圆上的多球及不好的球进行吸取，并将废球放置在废球瓶里
  - 根据视觉系统检测的对位信息，执行点胶和补球动作
  - 清洗机构对点胶针头进行清洗
  - 完成所有补球和吸取多球动作后，图像检测处理系统再对晶圆检测一次，晶圆如果补球成功，则传送机械手将晶圆送回晶圆盒里

<img src="..\fig\ME01\ME01_chapter12_fig11.jpg" style="zoom:70%;" />

##### 微球供给

- 微球 (按材质可为锡球、铜球和银球等多种)供给是实现微球单球供给的关键步骤
  - 目前晶圆级封装中微球供给机构基本采用以下方式
    - 振动盘供球
      - 利用重力作用，将微球从瓶中输送到振动盘中，通过振动盘的微小震动使微球均匀分布在供球容器中并保持微球的适度跳跃以利于后序吸球头的吸取
    - 真空吸球盘供球
      - 真空吸球盘供球方式是在供球盒的底部开有与晶圆电路凸点对应的真空孔，通过扫球机构或者是供球盒本身的倾斜，使微球在供球盒底部流动从而被真空孔吸着
      - 微球吸着成功后，植球头对应地将微球吸着到植球头上
    - 传统焊球球盒直接供球
    - 球盒直接供球方式一般使用气缸使球瓶翻转以实现自动供球，微球直接落在网板上，通过特殊的植球头将微球压入到晶圆对应位置
- 适用于补球机的微球供球机构主要解决的问题
  - 供给的微球不粘连，不氧化，防止补球失效
  - 单次供给的微球不空缺不外溢残留，实现单球供给
    - 避免造成多余的微球散落造成微球浪费
    - 避免微球的导电特点影响补球机电气的安全性

##### 电镀植球

- 步骤
  - 在晶圆上完成UBM层的制作
  - 沉积厚胶并曝光，为电镀焊料料形成模板
  - 电镀之后，将光刻胶去除并刻蚀掉暴露出来的UBM 层
  - 最后再流形成焊料料球

<img src="..\fig\ME01\ME01_chapter12_fig12.jpg" style="zoom:70%;" />

- 电镀技术可以实现很窄的凸点间距并维持高产率
- 该项技术应用范围也很广，可以制作不同尺寸、间距和几何形状的凸点
- 电镀技术已经越来越广泛的在晶圆凸点制作中被使用，成为最具实用价值的方案

<img src="..\fig\ME01\ME01_chapter12_fig13.jpg" style="zoom:70%;" />

### 扇出型WLP

#### 扇入型与扇出型

- 从技术特点上看，WLP主要分为
  - 扇入型 (Fan-in)
    - 如果封装后的芯片尺寸和产品尺寸在二维平面上是一样大，芯片有足够的面积把所有的 I/O接口都放进去，就采用扇入型
  - 扇出型 (Fan-out) 
    - 如果芯片的尺寸不足以放下所有的 I/O接口时，就需要扇出型
    - 一般的扇出型在面积扩展的同时也加了有源/无源器件
- 传统的WLP封装多采用扇入型，应用于引脚数量较少的IC
- 扇出型封装出现的背景
  - IC信号输出引脚数目增加，对焊球间距 (Ball Pitch)的要求趋于严格
  - 印刷电路板 (PCB)结构对于IC封装后尺寸以及信号输出引脚位置的调整需求

#### 简介

- Fan Out WLP/FOWLP，全称为Fan-out Wafer Level Packag-ing
  - 采用拉线出来的方式，成本相对便宜
  - FOWLP可以让多种不同裸晶做成类似WLP制程一般，等于减一层封装
  - 假设放置多颗裸晶，等于省了多层封装，有助于降低成本
- 特殊的晶圆级封装，可以灵活的重新分布裸晶，封装区域进行了扩散

<img src="..\fig\ME01\ME01_chapter12_fig14.jpg" style="zoom:70%;" />

#### 工艺流程

##### 扩散式WLP

<img src="..\fig\ME01\ME01_chapter12_fig15.jpg" style="zoom:70%;" />

- 扩散式WLP采用晶圆重构技术，工艺过程如下
  - 在一块层压载板上布贴片胶带
    - 载板通常选用人工晶圆，胶带则起到固定芯片位置和保护芯片的作用
  - 将测试良好的芯片 (KGD)面向下重新粘接到一块载板上
    - 芯片之间的距离决定了封装时扩散面积的大小，可以根据需要自由控制
  - 用模塑料对芯片以及芯片之间的空隙进行填充
  - 将载板和胶带从系统中分离
    - 载板可以重复利用
  - 进行RDL和焊球工艺步骤

<img src="..\fig\ME01\ME01_chapter12_fig16.jpg" style="zoom:70%;" />

##### 扇出型WLP

- 晶圆的制备及切割– 将晶圆放入划片胶带中，切割成各个单元
- 准备金属载板– 清洁载板及清除一切污染物
- 层压粘合– 通过压力来激化粘合膜
- 重组晶圆– 将芯片从晶圆拾取及放置在金属载板上
- 制模– 以制模复合物密封载板
- 移走载板– 从载板上移走已成型的重建芯片
- 排列及重新布线– 在再分布层上(RDL)，提供金属化工艺制造I/O接口
- 晶圆凸块– 在I/O外连接口形成凸块
- 切割成各个单元– 将已成型的塑封体切割

#### 优势

##### 可靠性

- 对于微处理器，最佳性能表现为优化的可靠性，包括热性能和电气性能
- 产品或组件的可靠性最终决定了设备的使用寿命，以及它能够在一段时间内快速一致地同时执行多项任务
- 如果将多个芯片嵌入单个FOWLP中，与其他封装技术相比，整个电气路径更短，从而实现更快的信号传输
- 此外，可以实现更多与印刷电路板 (PrintedCircuit Board, PCB)的物理连接更好的热流，这对热性能至关重要
- 在FOWLP中，凸块不依赖于芯片表面，因此通过实施更多的RDL来扩大电气连接可以实现更高的VO密度
  - 在最先进的扇出封装中，为了最大限度地提高VO密度，最多可以同时使用四个RDL (Redistribution Layer) 
    - 有助于提高电气和散热性能，包括功耗

##### I/O密度

- RDL用作I/O布局的重新路由并启用更高的I/O数量
- 高I/O密度通常会有更好的电气性能
  - 因为更多的输出会导致芯片之间更快的电信号，并将电短路带来的风险降至最低
  - 较高的I/O密度也使封装能够并行执行更多操作
- 高I/O 数量允许封装更复杂及高速的芯片

**应用：嵌入式晶圆级球栅阵列**

<img src="..\fig\ME01\ME01_chapter12_fig17.jpg" style="zoom:70%;" />

##### 更多功能

- 现代消费电子产品为用户提供更多功能更强大的存储空间，触摸屏，语音识别，高性能CPU ，更长的电池寿命以及运动传感器

**如何在轻薄型电子产品中融入更多功能?**

- 整合。有多种方法可以使用 FOWLP来实现这一点
  - 通过嵌入来实现异构和均匀集成更多的集成电路和被动元件在同一个封装体内，并且利用更复杂的元件封装架构
    - 例如多芯片封装中多种功能的多个管芯嵌入同一封装内的模制化合物中
  - 另一种实现更高集成度和功能的方法是使用封装级封装
    - 如台积电在最新iPhone型号中使用的FOWLP 封装 (APE 上的DRAM) 
  - 还有许多其他扇出式封装技术采用2D，2.5D或3D架构以实现最大程度的集成

##### 更小尺寸

-  下一代智能手机需要更密集的封装，这可通过晶体管扩展 (摩尔定律)或使用创新封装技术的高级集成来实现
- 通过模具嵌入的实施，结合精细特征使用晶圆处理的可能性，FOWLP将形成高密度封装所需的RDL数量降至最低，同时不会受到过度的成本损失
- 由于RDL可以在整个覆盖模具区域形成，因此可以完全不需要IC衬底或内插器，这相对于传统封装技术而言大大降低了形状因数
- 通过集成，特别是通过在同一封装体内嵌入多个裸片并使用创新的封装架构，外形因素可以进一步降低
- FOWLP技术可使封装厚度减少20%
  - 与标准倒装芯片封装相比，FOWLP提供的封装外形尺寸减少至少40%

#### 缺点

- 焊接点的热机械行为
  - 因FOWLP的结构与BGA结构相似，所以FOWLP焊接点的热机械行为与BGA的结构相同
  - FOWLP中焊球的关键位置在硅晶片面积的下方，其最大热膨胀系数不匹配点会发生在硅晶片与PCB之间
- 晶片位置精确度
  - 在重新建构晶因时，必须要维持晶片从拾取及放置 (Pick and Place)于载具上的位置不发生偏移，甚至在铸模作业时，也不可发生偏移
  - 因为介电层开口，导线重新分布层与焊锡开口 (Solder Opening)制作，皆使用光学光刻技术，掩模对准晶困及曝光都是一次性的，所以对于晶片位置精确度要求非常高
- 胶体的剥落
  - 在常压时被胶体及其他聚合物所吸收的水分，在经过220-260回流焊 (Reflow) 时，水份会瞬间气化，进而产生高的内部蒸气压
  - 如果胶体组成不良，则易有胶体剥落的现象产生
- 晶圆的翘曲
  - 人工重新建构晶圆的翘曲 (War page)行为也是一项重大挑战
  - 重新建构晶圆含有塑胶、硅及金属材料，其硅与胶体之比例在x, y, z三方向不同，铸模在加热及冷却时热胀冷缩会影响晶圆的翘曲行为
  - 翘曲是基于扇出技术的关键挑战
    - 当使用较薄的封装时，除了异质材料和更多铜层之外，晶圆弯曲在加工之后发生
    - 晶圆弯曲是晶困上应力分布不均匀并影响成品率的结果
    - 为了克服这个问题，必须优化晶圆制造工艺和扇出设计流程
- 模具移位
  - 模具移位是另一个工艺难题，是指放置在载体晶圆上和包覆成型过程中模具轻微移动
  - 对于基于晶圆的技术来说，模具移位是一个挑战
  - 随着对面板格式的期望过渡，模具移位变得更加关键
    - 处理大方形格式一致和精确模头定位的设备尚未得到验证
    - 基于面板和面板的扇出封装的主要关注点：模具移位影响产量

## **WLP的应用及展望**

### 应用

- 圆片级封装技术的优势使其一出现就受到极大的关注，并迅速获得巨大的发展和广泛的应用
- 在移动电话等便携式产品中，已普遍采用圆片级封装型的EPROM、IPD (集成无源器件)、模拟芯片等器件
- 圆片级封装技术已广泛用于闪速存储器、EEPROM、高速DRAM、SRAM、LCD驱动器、射频器件、逻辑器件、电源/电池管理器件和模拟器件 (稳压器、温度传感器、控制器、运算放大器、功率放大器)等领域

### 未来

- 更大的芯片，更强大的功能
- WLCSP中的TSV，允许双面连线
- 堆叠3D WLP
- MEMS WLCSP

## MCM的背景

> MCM：多芯片组件

-  随着便携式电子系统复杂性的增加，对VLSI集成电路的低功率、轻型及小型封装的生产技术突出了越来越高的要求
- 同样，许多航空和军事应用也正在朝该方向发展
- 为了满足这些要求，在MCM x, y平面内的二维封装基础上，将裸芯片沿z轴层叠在一起
  - 在小型化方面就取得了极大地改进
  - 由于z平面技术总互连长度更短，降低寄生性的电容、电感，因而系统功耗约可降低30%
- 无论采用何种封装技术后的裸芯片，在封装后裸芯片的性能总是比未封装的要差一些
  - 对传统的混合集成电路(HIC)彻底的改变：多芯片组件 (Muti-chip Module，即MCM)
    - 把几块IC芯片或CSP组装在一块电路板上，构成功能电路板
    - 以美国IBM公司在1980年初期开发的热传导组件 (TCM)为例
- MCM是在混合集成电路技术基础上发展起来的一项微电子技术
- 其与混合集成电路产品并没有本质的区别
  - MCM具有更更高的性能、更多的功能和更小的体积
  - MCM属于高级混合集成电路产品

## MCM的定义及特点

### 定义

- 将2个以上的大规模集成电路裸芯片和其它微型元器件互连组装在同一块高密度多层基板上
- 并封装在同一管壳内构成功能齐全质量可靠的电子组件
- 并利用它实现芯片间互连的组件

<img src="..\fig\ME01\ME01_chapter12_fig18.jpg" style="zoom:70%;" />

### 特点

- MCM是将多块未封装的IC芯片高密度安装在同一基板上构成的部件
  - 省去了IC的封装材料和工艺
  - 节约了原材料
  - 减少了制造工艺
  - 缩小了封装尺寸和重量
- MCM是高密度组装产品，芯片面积占基板面积至少20％以上
  - 互连线长度极大缩短
  - 封装延迟时间缩小
  - 易于实现组件高速化
- MCM的多层布线基板导体层数应不少于4层
  - 能把模拟电路、数字电路、功率器件、光电器件、微波器件及各类片式化元器件合理而有效地组装在封装体内
  - 形成单一半导体集成电路不可能完成的多功能部件、子系统或系统
    - 使线路之间的串扰噪声减少
    - 阻抗易控
    - 电路性能提高
- MCM避免了单块IC封装的热阻、引线及焊接等一系列问题
  - 产品的可靠性获得极大提高
- MCM集中了先进的半导体IC的微细加工技术，厚、薄膜混合集成材料与工艺技术，厚膜、陶瓷与PCB的多层基板技术以及MCM电路的模拟、仿真、优化设计、散热和可靠性设计、芯片的高密度互连与封装等一系列新技术
  - 混合形式的全片规模集成 (WSI，wafer scale integration)

## MCM的分类

> 互连和封装电子学会 (IPC)标准

### MCM-L

> Multi Chip Module-Laminate，有机叠层布线基板

<img src="..\fig\ME01\ME01_chapter12_fig19.jpg" style="zoom:70%;" />

- 采用层压有机基材，制造采用普通印制板的加工方法
  - 应用印刷和蚀刻法制成铜导线，钻出盲孔、埋孔和通孔并镀铜，内层的互连由EDA (电子设计自动化)软件设计来定
- MCM-L由于采用普通的印制电路板的加工方法。优势：
  - 低成本
  - 工期短
  - 投放市场时间短

### MCM-C

> Multi Chip Module-Ceramic，陶瓷多层布线基板

<img src="..\fig\ME01\ME01_chapter12_fig20.jpg" style="zoom:70%;" />

- 陶瓷多层布线基板采用陶瓷烧制基材，导体是一层层烧制金属制成的，层间的通孔互连与导体一块生成
- 电阻可以在外层进行烧制，最后用激光修整到精确值
- 所有导体和电阻都印刷到基板上，加工方法颇为复杂

### MCM-D

> Multi Chip Module-Deposited Thin Film，薄膜多层布线基板

<img src="..\fig\ME01\ME01_chapter12_fig21.jpg" style="zoom:70%;" />

- 薄膜多层布线基板是用薄膜技术形成多层布线，以陶瓷 (氧化铝或氮化铝)或Si、Al 作为基板的组件
- 基片是由硅和宽度在1 m - 1 mm之间的导体构成，通孔则是由各种金属通过真空沉积而形成
- 布线密度在三种组件中是最高的，但成本也高

### MCM-Si

> Multi Chip Module-Silicon，硅基板

- 在Si衬底上使用二氧化硅介质

### MCM-C/D

> 厚薄膜混合多层基板

- 混合型的MCM-D/C即共烧陶瓷上淀积薄膜型

### 封装基板的电路结构比较

| 实用技术 | 互联密度 (in/in^2^) | 信号层数 (总层数) | 总长 (in/in^2^) | 通孔密度 (/in^2^) |
| :------: | :-----------------: | :---------------: | :-------------: | :---------------: |
|  MCM-L   |         30          |      12 (12)      |       360       |        100        |
|  MCM-C   |         50          |      20 (42)      |      1000       |       2500        |
|  MCM-D   |         350         |       4 (8)       |      1400       |       33000       |

## MCM的优缺点

### 优点

#### MCM

- 高速性能
  - 多个裸芯片高密度安装在一起，缩短了芯片之间的距离和传输路径长度，信号延迟大大减少，从而提高工作频率
- 高密度性能
  - MAC-C最多可达10层
  - MAC-D导体线宽/间距：5/10μm
  - MAC-D封装效率 达70%以上
- 高散热性能
  - 需采用新的散热技术，保证高性能和高密度的LSI不因散热不好而使性能和可靠性下降

#### MAC

- 低成本性能
  - 组装密度和工作频率都提高2~4倍，可以实现产品相对低的成本
  - 其中，MCM-L最具有低成本的发展前景

|              | 与SMT相比 | 与THT相比 |
| :----------: | :-------: | :-------: |
|   面积减小   |   3~6×    |  10~20×   |
|   重量减轻   |   0~3×    |    ~6×    |
| 信号延迟改善 |    2×     |    >3×    |
|   结温下降   |    20℃    |    20℃    |
|  可靠性改进  |    4×     |    >4×    |
|   相对成本   |   昂贵    |   昂贵    |

### 缺点及制约因素

- 没有标准的设计规范和生产工艺
  - 缺乏已知合格 (KGD)，设备、材料和工艺成本比较昂贵，MCM的成本一直居高不下
  - 只要一个元器件失效，整个组件就得报废，这也造成了商业应用难以接受的高成本
- MCM失去众多应用市场
  - 当今半导体技术发展迅速，ASIC的密度越来越高，功率越来越大，其提升速度远远超过了早期的预测
- KGD来源问题一直没有从根本上得到解决
  - MCM所组装的LSI 、VLSI 和ASIC通常为裸芯片，我国裸芯片主要来源于国外，KGD以及高频和大功率芯片的来源更是一项亟待解决的问题
  - 直接限制设计人员方案的选择，很大的程度上妨碍着MCM的推广应用
- 竞争
  - 诸如芯片级封装 (CSP)、倒装芯片封装 (FCP)﹑多芯片封装 (MCP)等新型微电子技术的出现，以其极具竞争力的性价比对MCM构成了竞争态势，并对MCM的未来发展形成了威胁

## MCM的设计技术

### 设计考虑

- 设计目的：考虑所采用的技术对MCM整体性能、可靠性、功率和综合成本的影响
- 设计模拟分析的基础在于 建立合理的数学模型和应用软件
- 设计需要考虑
  - 电性能问题：互联寄生参数：R, L, C
  - 成本问题 (尤其在中、低档批量产品应用中)
  - 系统成本率和可靠性问题
  - 功率及散热问题

#### 几大问题

- 电性能问题
  - 在传统的电子封装中，和互连有关的寄生参数包括采用WB技术将芯片连接到封装基板上的寄生电阻、寄生电容、寄生电感以及焊接引脚或表面安装封装的电阻、电感、电容
- 成本问题
  - MCM主要用于高性能、高速度及高可靠领域时，其成本并非是特别重要的因素
  - MCM使用在汽车领域，在大批量生产时，的确是性能价格比较好的电子产品
  - MCM往往要增加一些附加的成本，例如增加裸芯片的筛选测试成本和重新布线成本
- 系统成品率和可靠性问题
  - 系统成品率是单个元器件成品率的函数
  - MCM的系统成品率与芯片、基板和键合工艺等参数密切相关，其中芯片的成本占MCM成本的首位
  - 因此要保证裸芯片的成品率，否则复杂的MCM系统成品率难以保持很高
- 功率及散热问题
  - 元器件的MCM基板上的组装密度高产生了散热问题
  - MCM的热设计自然成为MCM设计中的关键内容之一

### MCM热设计

- 目的
  - 保证 MCM组件工作的可靠性
  - 目前主要采用两种途径
    - 气体冷却技术
    - 液体冷却技术来进行MCM的设计
  - 目前又出现了气体、液体混合冷却技术，但应用很少
- 热分析的应用软件主要分四类
  - 第一类是电子热控制应用制作的软件
  - 第二类是使用分立或集中参数元件的网络热分析软件
  - 第三类是以有限元为基础的热分析软件
  - 第四类是适合于MCM的CAD工具中的热分析软件

> 使用最广泛的热分析软件是通用的网络热分析器。这些软件可处理热阻网络的复杂问题

### MCM的组装技术

- MAC组装技术是指通过一定的连接方式将元器件组装到MCM基板上，再安装在金属或陶瓷封装中，组成一个多功能MAM组件
- MAC组装技术为制造MCM的关键技术之一
  - 极大的影响MCM组件的体积和重量
  - 决定产品性能和成本率的重要因素
- MCM的组装技术包括
  - 芯片与基板的粘接
  - 芯片与基板的电气连接
  - 基板与外壳的物理连接和电气连接

#### 芯片与基板的粘接

- 粘接材料分为两大类
  - 有机粘接剂
  - 无机粘接剂

|   无机粘结剂    |  有机粘接剂  | 有机粘接剂 |
| :-------------: | :----------: | :--------: |
|      类型       |    热固型    |   热塑型   |
| Au-Si等共晶焊料 |   环氧树脂   |  聚酰亚胺  |
|   Ag玻璃浆料    |   聚酰亚胺   |  聚酰亚胺  |
|     软焊料      | 胺基甲酸乙酯 |  聚酰亚胺  |

##### 两类粘接材料优缺点

|                  环氧树脂                  |                        环氧树脂                         |                         合金焊料                         |                  合金焊料                  |
| :----------------------------------------: | :-----------------------------------------------------: | :------------------------------------------------------: | :----------------------------------------: |
|                  **优点**                  |                        **缺点**                         |                         **优点**                         |                  **缺点**                  |
|           固化温度低 (150-180℃)            |               有放气危险 (H~2~O、NH~3~等)               |         导热率高，对大功率电器提供良好 散热路径          | 处理温度高，300℃以上高温可能损伤焊丝和器件 |
| 批量处理成本低，可使用浆料、粘接带或预制件 | 有离子污染危险 (CL^-^、F^-^、Na^+^、K^+^)，可能产生颗粒 |                       预制件可买到                       |        较高的焊料熔化温度，限制返修        |
|        在温度、压力下软化，容易返修        |        导电型的界面接触电阻可能随时间延长而增加         |                                                          |      工艺不当可能会产生金属颗粒或溅射      |
|              有导电和绝缘两种              |            获得好的附着性需控制粘接面清洁度             | 不放气，电路可满足K级,低水气含量，要求<(3~5)×10^-3^(V/V) |                 只有导电型                 |

#### 芯片与基板的电气连接

##### WB引线键合

|    方法    |      材料      |   温度   | 压力 |  时间  |
| :--------: | :------------: | :------: | :--: | :----: |
|   燃压焊   | Au丝，AL或焊区 | 300~400℃ |  高  | ~40 ms |
|  超声键合  | Au丝，AL或焊区 |   室温   |  低  | ~20 ms |
| 热压超声焊 | Au丝，AL或焊区 | 150~225℃ |  低  | ~20 ms |

##### TAB载带自动焊

<img src="..\fig\ME01\ME01_chapter12_fig22.jpg" style="zoom:70%;" />

- 通过载带连接芯片与基板；芯片与载带又通过焊料 凸点进行连接。
- 载带由聚酯、环氧树脂（或PI）薄膜和Cu箔组成 。
- 关键技术：凸点制作、内引线焊接ILB和外引线焊接OLB

##### FCB倒装焊

- 优点
  - 具有最短的电信号路径
  - 互联密度高
  - 散热好，电路产生的热直接从芯片背面散出
  - 为最理想的MCM组装工艺
- 缺点
  - 焊料凸点芯片制作困难
  - 不能检测内部连接完整性
  - 返修困难

<img src="..\fig\ME01\ME01_chapter12_fig23.jpg" style="zoom:70%;" />

#### 基板与外壳的物理和电气连接

- MCM基板与封装外壳底部连接有三种方法
  - 粘接剂连接
  - 焊接 (Pb-Sn焊膏)
  - 机械固定
- MAC基板与封装外壳的电气连接方式：
  - 采用WB互联引线，将封装外壳的外引脚与基板上的互联焊区连接起来
  - 互联引线为18~50 μm直径的Au或Al丝
  - 对于大功率MCM，Al丝直径为0.1~0.5 mm

### MCM检测技术

- 在 MCM的制造过程中，要进行多级检验和电性能测试以保证MCM的质量和可靠性
- 主要有三个方面的测试
  - 基板测试
    - 在制造过程中和组装元器件之前进行
  - 元器件测试
    - 在组装到基板上之前进行
  - 成品组件测试
    - 组件测试与故障诊断是在组装后并返修完有缺陷的元器件后，最后封装之前进行

#### 基板测试

- MCM基板包含有全部元器件连接的导体布线及互连通孔，测试的目的是验证基板布线及通孔的互连和导通，监控制造过程中的质量
- 测试主要针对基板表面焊区上相连的电气网络，这些焊区起着电信号出入基板的连接作用
  - 一些焊区与组装在基板上的芯片相连，另一些焊区与组件外的分立元器件相连
- 把一个或多个探针与基板上的焊区相接触，就可进行电气网络测试
- 测试内容还包括阻抗、信号传输延迟、串扰和高压泄漏的测量

#### 元器件测试

- MCM使用的芯片质量是生产高成品率 MCM的关键因素
  - 生产优质芯片的工艺必须符合既定的工艺流程，否则加工成本很高
  - 芯片应放在自动处理装置进行老化和终测
- 测试裸芯片的夹具分为三类
  - 小型固定载体
  - 临时封装或载体
  - 裸芯片插座
- TAB就是一种小型固定载体，是裸芯片测试较成熟的方法之一

### MCM返修技术

- 修是MCM制造过程中必须重视的一个环节
  - 尽管人们希望任何MCM组件都不需要返修，但当前要彻底取消是不合理的
- 随着工艺水平、工艺质量、大规模制造能力和自动化程度的提高，返修可以逐步取消

<img src="..\fig\ME01\ME01_chapter12_fig24.jpg" style="zoom:70%;" />

#### 返修的分类

- WB器件的返修
- 粘接芯片和基板的返修
- 倒装芯片的返修
- TAB连接芯片的返修
- 导带的返修

## 3D-MCM简介及其应用

### 三维多芯片组件及其应用

#### 概述

- 三维多芯片组件 (简称3D-MCM)是在二维多芯片组件 (即2D-MCM，通常指的MCM均系二维）技术基础上发展起来的高级多芯片组件技术

#### 区别

- 3D-MCM是通过采用三维 (x, y, z方向)结构形式对IC芯片进行立体结构的三维集成技术
- 而2D-MCM则是在二维 (x, y方向)对IC芯片集成，即采用二维结构形式对IC芯片进行高密度组装，是IC芯片的二维集成技术

#### 应用

- 三维多芯片组件技术是现代微组装技术发展的重要方向，是微电子技术领域跨世纪的一项关键技术
- 由于宇航、卫星、计算机及通信等军事和民用领域对提高组装密度、减轻重量、减小体积、高性能和高可靠性等方面的迫切需求
- 加之3D-MCM在满足上述要求方面具有的独特优点，因此该项新技术近年来在国外得到迅速发展

### 发展驱动力

- 电子系统 (整机)对系统集成的迫切需求
  - 电子系统 (整机)向小型化、高性能化、多功能化、高可靠和低成本发展已成为目前的主要趋势，从而对系统集成的要求也越来越迫切
  - 实现系统集成的技术途径主要有两个
    - 一是半导体单片集成技术
    - 二是采用MCM技术
  - 前者通过晶片规模的集成技术 (WSI)，将高性能数字集成电路 (含存储器、微处理器、图象和信号处理器等)和模拟集成电路 (含各种放大器、变换器等)集成为单片集成系统
  - 后者通过三维多芯片组件 (3D-MCM或MCM-V)技术实现WSI的功能。
  - 可能在相当一段时间内，实现系统集成的主要技术途径仍将是3D-MCM技术
    - 这对于半导体集成电路工业还不甚发达的我国尤其如此
- 二维组装密度 (组装效率)的限制
  - 现代微组装技术的发展已到了接近二维组装所能达到的理论上最大的组装密度，目前2D-MCM的组装效率最高达85%，而采用3D-MCM可实现更高的组装密度 (组装效率)
  - 3D-MCM的组装效率则已可达200%以上
    - 因此为了进一步提高组装密度，实现更小的体积和更多的功能，也必须从二微组装向三维微组装发展

### 优点

> “四个减小”、“六个增大”

- 进一步减小了体积，减轻了重量
  - 3D-MCM相当于2D-MCM而言，可使系统的体积缩小10倍以上，重量减轻6倍以上
- 减小信号传输延迟时间
  - 由于VHSI的发展和应用，使得芯片之间互连线的长度已成为影响系统 (整机)信号传输延迟的关键
  - 3D-MCM中芯片之间的互连长度比2D-MCM短得多，因此可进一步减小信号传输延迟时间
- 减小信号噪声
  - 在数字信号系统中，主要有四种噪声来源
    - 反射噪声
    - 串扰噪声
    - 同步触发噪声
    - 电磁干扰
  - 这些噪声与信号在互连线中传输时的上升时间相关，即与互连线长短相关
  - 3D-MCM可通过进一步缩短互连线的长度来降低信号噪声
- 减小功耗
  - 电子系统中互连线功耗的表达式可写为$p=fCV^2$
    - $f$：信号频率
    - $V$：互连线两端的电压差
    - $C$：互连线的寄生电容
  - 由此看出互连线的长度越短，寄生电容越小，功耗就越低
  - 如前所述，3D-MCM相对于2D-MCM而言可进一步缩短互连线，因此也可降低功耗
- 进一步增大组装效率
  - 2D-MCM的组装效率目前最高可达85%
  - 从理论上来讲，2D-MCM组装效率要达到100%是不可能的，这是2D-MCM本身的结构限制所决定的
  - 而3D-MCM的组装效率目前已高达200%
- 增大互连效率
  - 互连效率系指组件单位面积的互连点数
  - 3D-MCM与2D-MCM及SMT技术单位连接点数相比较，每单位面积的连接点数比2D-MCM多1\~3个数量级以上，比SMT技术多1\~4个数量级以上
- 增大信号带宽
  - 互连带宽，特别是存储器带宽往往是影响计算机和通信系统性能的重要因素
  - 降低延迟时间和增大总线宽度是增大信号宽度的重要方法
  - 3D-MCM正好具有实现此特性的突出优点
- 增加信号传输 (处理)速度
  - 如前所述，3D-MCM可大大减小信号传输 (处理)延迟时间，从而也就大大提高了信号传输速度
- 增加功能
  - 由于3D-MCM比2D-MCM具有更高的组装效率和电互连效率，因此可集成更多的功能，实现多功能的部件以至系统 (整机)
- 进一步提高可靠性
  - 由于3D-MCM内部单位面积的互连点数大大增加，具有更高的集成度
  - 使其整机 (或系统)的外部连接点数和插板都大大减小，因此可靠性得到进一步提高

### 结构类型

> 三维存储器组件多采用两种3D-MCM结构形式：一是2D-MCM叠层型3D-MCM，另一是IC芯片叠层型3D-MCM

<img src="..\fig\ME01\ME01_chapter12_fig25.jpg" style="zoom:70%;" />

- 埋置型
  - 在多层基板的底层埋置 IC芯片，再在多层布线顶层组装 IC芯片，其间通过多层布线进行高密度连接, 基板多用硅或其他高导热基板 (AlN、Al等)
- 有源基板型
  - 在基板 (通常为Si或 GaAs)上直接制作多种数字半导体集成电路
  - 再在其上制作多层布线
  - 然后在多层布线顶层组装模拟IC芯片和集成传感器芯片、光电子功能芯片等
- 3D‐MCM
  - 把多个二维封装实行叠装、互连，把2D封装组装成3D封装结构
  - 将多块组装有IC芯片 (可单、双面组装)的多层布线基板进行叠装、互连

### 应用实例

#### 大容量存储器组件

- 采用多芯片组件技术制作高性能大容量的存储器组件是MCM技术的重要应用领域之一
- 高速成像系统发展的需求，进一步推动了存储器多芯片组件从二维技术向三维技术发展
  - 目前的成像系统，其像素已多达9×10^6^像素/帧，需要采用100帧/秒以上的数据存储
  - 若将此数据存储转换为数据存储带宽，则需要达Gbit/s的存储容量，已远超出了目前一般的Mbit/s的存储容量
  - 采用三维MCM技术实现大容量的存储器组件则不失为一个良好的解决途径

##### AT&T移动电话MCM BGA封装

<img src="..\fig\ME01\ME01_chapter12_fig26.jpg" style="zoom:70%;" />

##### 带外壳及灌硅胶的MCM BGA封装

<img src="..\fig\ME01\ME01_chapter12_fig27.jpg" style="zoom:70%;" />

### MCM发展趋势

- MCM早在80年代初期就曾以多种形式存在，但由于成本昂贵,大都只用于军事、航天及大型计算机上
- 随着技术的进步及成本的降低，近年来，MCM在计算机、通信、雷达、数据处理、汽车行业、工业设备、仪器与医疗等电子系统产品上得到越来越广泛的应用，成为最有发展前途的高级微组装技术
- 目前2D-MCM组装效率最高可达85%，已接近二维组装所能达到的最大理论极限，这已成为混合集成电路持续发展的障碍
- 为了改变这种状况，三维的多芯片组件应运而生，其最高组装密度可达200%
- 3D-MCM是为适应军事宇航、卫星、计算机、通信的迫切需要而近年来在国外得到迅速发展的高新技术，是实现系统集成的重要技术途径