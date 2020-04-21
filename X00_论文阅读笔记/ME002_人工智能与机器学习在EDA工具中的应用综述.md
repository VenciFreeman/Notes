# 人工智能与机器学习在EDA工具中的应用综述

> **Artificial Intelligence and Machine Learning Applications in EDA tools Summary**

[TOC]

## Introduction

Electronic design automation (EDA) is a category of software tools for designing electronic systems such as integrated circuits and printed circuit boards<sup>[1]</sup>. The tools work together in a design flow that chip designers use to design and analyze entire semiconductor chips. Since a modern semiconductor chip can have billions of components, EDA tools are essential for their design.

电子设计自动化是一类用于设计电子系统，例如集成电路和印刷电路板的软件工具<sup>[1]</sup>。 这些工具在芯片设计师设计和分析芯片的整个设计流程中协同工作。现代半导体芯片可以包含数十亿个组件，因此EDA工具对于芯片的设计至关重要。

Artificial intelligence (AI) and machine learning (ML) have made remarkable achievements in recent years and becoming the main driving force for profound changes in electronic technology. EDA manufacturers represented by Cadence and Synopsys are trying to use these new technologies to optimize the chip design process. This article mainly explains the advantages and challenges of the application of artificial intelligence and machine learning in EDA tools in the form of a summary of the paper, and gives a summary about the future prospects and limitations of the technology at the end.

而人工智能与机器学习在近些年大放异彩，成为电子科技深刻变革的主要动力。以Cadence和Synopsys为代表的EDA厂商正尝试利用这些新技术对芯片设计流程进行优化。本文主要根据论文综述的形式来阐释人工智能与机器学习在EDA工具中应用的优势和存在的挑战，并在文章末尾对该技术的未来展望和局限性进行总结。

## Advantages

### Logic Optimization Algorithms

Finding and implementing optimization algorithms is a difficult task, especially with the novel logic primitives and potentially unconventional requirements of emerging technologies. A paper<sup>[2]</sup>published in 2018 IEEE International Symposium on Circuits and Systems (ISCAS) casted logic optimization as a deterministic Markov decision process (MDP), then We it took advantage of recent advances in deep reinforcement learning to build a system that learns how to navigate this process. 

寻找和实现优化算法是一项艰巨的任务，尤其是对于新的逻辑原语和新兴技术的潜在非常规需求而言。发表于2018年国际电路与系统专题研讨会的这篇论文<sup>[2]</sup>将逻辑优化作为确定性的马尔可夫决策过程，然后利用深度强化学习的最新进展构建了一个学习导航此过程的系统。

Some of the key features of DNNs are their capability to automatically determine relevant features and build hierarchical representations given a particular problem domain, and this ability of DNNs removes the need for handcrafted features. In the finally results, the deep reinforcement learning algorithm is able to find optimum representations for all 3-input functions, and it’s also able to reach 83% of potential improvement in size optimization of 4-input functions. Additionally, it’s able to find significant optimizations in larger 6-input disjoint subset decomposable (DSD) functions, reaching 89.5% of potential improvement and 86 of improvement compared to MCNC benchmark.

DNN的一些关键特征是它们能够自动确定相关特征并在给定特定问题域的情况下构建层次表示，这种功能消除了对手工功能的需求。最终的结果中，该深度学习算法可以实现3输入逻辑门的100%最佳表示，以及4输入逻辑门的84%最佳表示。除此之外，在较大的6输入不相交子集可分解功能中可以实现89.5%的潜在改进，以及相比MCNC基准测试的86%性能改进。

### Faster Placement for VLSI

Placement for very-large-scale integrated (VLSI) circuits is one of the most important steps for design closure, it's a critical but time-consuming step in the VLSI design flow. As it determines the locations of standard cells in the physical layout, its quality has significant impacts on the later stages in the flow such as routing and post-layout optimization. A placement solution also provides relatively accurate estimation to routed wire-length and congestion, which is valuable in guiding the earlier stages like logic synthesis. The commercial design flows often run core placement engines many times to achieve design closure. As placement involves large-scale numerical optimization, current placement usually takes hours for large designs, thus, slowing down design iterations. Therefore, ultra-fast yet high quality placement is always in strong demand.

VLSI的布局设计是非常关键且非常耗时的步骤。确定物理布局中标准单元的位置时，布局的质量会对后期优化产生重大影响，而布局解决方案中对布线长度和阻塞的估计也对早期逻辑综合有相当的价值。商业设计流程通常多次运行核心布局引擎以实现设计的闭合。因为布局涉及到大规模数值优化，所以当前的大型设计布局需要花费几个小时，这会减慢设计迭代的速度。因此，迫切需要实现超高速高质量布局。

A paper<sup>[3]</sup> published in the 56th Design Automation Conference (DAC) in 2019 proposed a novel GPU-accelerated placement framework DREAMPIace, by casting the analytical placement problem equivalently to training a neural net-work. It essentially solves a nonlinear optimization problem, and can achieve over 30 times speedup in global placement without quality degradation compared to the state-of-the-art multi-threaded placer RePlAce。

发表于2019年第56届设计自动化会议的一篇论文<sup>[3]</sup>提出了一种GPU加速布局框架，通过等效分析性布局来训练神经网络，从根本上解决了线性优化问题，相比于目前最先进的多线程布局框架在全局布局中可以实现30倍以上的速度，而质量不会下降。

### Solve Problems Encountered in the Traditional CAD Flows

The increase in size and complexity of designs, and the shortening of the design cycle have contributed to high R&D expenditures that allow fewer and fewer companies to develop new designs with ambitious goals for low power and high performance and stay competitive.

设计尺寸和复杂性的增加以及设计周期的缩短导致了高昂的研发支出，使得计划开发低功耗、高性能目标并保持竞争力的新设计的公司越来越少。

Machine learning can be applied to solve common optimization and classification problems encountered in the traditional CAD flows, including functional verification and debug <sup>[4]</sup>. This is an active area in areas ranging from functional and formal verification, yield modeling, noise and process variation modeling, analog circuit performance modeling to design rule checking, IP reuse, and ESD model development.

而机器学习可用于解决传统CAD流程中常遇到的优化和分类问题，包括功能验证和调试<sup>[4]</sup>。这是一个活跃的领域，从功能和形式验证、成品率建模、噪声和过程变化建模、模拟电路性能建模到设计规则检查、IP重用和ESD模型开发等。

## Challenges

### If the Platform Is Trustworthy or Not

How an algorithm goes into an application? That means making sure the platform is trustworthy in multiple ways. We have to trust that the function can be mapped from the software stack, through the various abstraction levels down to the hardware, and that the platform is working as we want it. This is a huge verification problem. And we should consider is it secure or not. Anyone can insert malicious code into the platform or into the software, can the data be tampered or stolen? EDA has to tackle the areas of uncertainty so that the users can focus on the dataset.

算法如何在应用程序的所有方面发挥作用？这意味着需要通过多种方式确保平台值得信赖。必须信任该功能可以从软件堆栈，通过各种抽象级别到硬件进行映射，并且该平台可以按期望的方式运行，这是一个巨大的验证问题。除此之外还需要考虑安全性。任何人都可以将恶意代码插入平台或软件中，数据是否可能被篡改或窃取？EDA必须解决这些不确定性，以便使用者可以专注于数据集。

### Ensure Systems Adapt in a Stable Way

We must ensure systems adapt in a stable way and we know when things change. So, we need formal verification processes to ensure stable learning and robust reactions to unexpected inputs. In addition, some machine-learning methods are black boxes that cannot tell you why they produced a particular answer, so we need more focus on building systems where learned parameters can be interpreted and reviewed, producing a probabilistic confidence for each answer. Many problems are related to a class of sequential decision and optimization problems measured against an objective function and constraints. For these types of problems, verification is even more critical and more complex to complete.

需要确保系统可以以稳定的方式适应环境，并且知道情况何时发生变化。因此，需要正式的验证流程，以确保稳定的学习和对意外输入的可靠反应。除此之外，一些机器学习的方法是黑匣子，无法解释为什么产生特定答案，因此需要更多地专注于构建可以解释和检查所学习参数的系统，从而为每个答案产生概率置信度。而对于一些问题，例如针对目标函数和约束条件衡量的一类顺序决策和优化问题，验证更加关键，并且完成起来也更加复杂。

## Prospects and Limitations

IC design has always been a compute-intensive and data-intensive activity. The advantages that AI and ML can deliver in EDA can allow developers to leverage the technology in a better manner. AI and ML allows EDA tools to work quicker and supply an enormous increase in output along with expanded accuracy as well. These technologies have great potential to provide guidance and automation for the whole design flow, increasing designer productivity as block complexity grows.

IC设计一直是计算密集型和数据密集型活动。人工智能和机器学习在EDA中的优势可以使开发人员更好地使用技术。借助人工智能和机器学习，EDA工具可以更迅速，并提供更大的吞吐量和更高的准确性。这些技术有潜力为整个设计流程提供指导和自动化。随着模块复杂性的提高，这些技术可以提高设计人员的生产率。

And the future AI and ML tech must address many of the fundamental needs for intelligent embedded systems required to adapt within their environment. These systems include applications such as ADAS, robotics, CAD, transportation, and logistics as well as distributed IoT apps. And future tech also will have greater emphasis on explainable AI, especially where human factors and safety are involved. In addition, it will require significant progress in verification processes and standards that can ensure robust adaptation. Progress in all these challenges will enable the realization of truly adaptive, commercial decision systems.

而未来的人工智能和深度学习技术也必须适应智能嵌入式系统的许多基本需求。这些系统包括ADAS、机器人技术、CAD、运输物流应用程序、以及分布式物联网应用程序。而未来技术也将更加强调可解释的AI，尤其是在涉及安全性和人为因素的地方。总的来说，要求在验证过程和标准方面取得更多进步，以确保稳定的适应性。在所有这些方面取得进展将使实现真正的适应性商业决策系统成为可能。

## References

1. "About the EDA Industry". Electronic Design Automation Consortium. Archived from the original on August 2, 2015. Retrieved July 29, 2015. 
2. W. Haaswijk et al., "Deep Learning for Logic Optimization Algorithms," 2018 IEEE International Symposium on Circuits and Systems (ISCAS), Florence, 2018, pp. 1-4.
3. Y. Lin, S. Dhar, W. Li, H. Ren, B. Khailany and D. Z. Pan, "DREAMPIace: Deep Learning Toolkit-Enabled GPU Acceleration for Modern VLSI Placement," 2019 56th ACM/IEEE Design Automation Conference (DAC), Las Vegas, NV, USA, 2019, pp. 1-6. 
4. M. Pandey, "Machine learning and systems for building the next generation of EDA tools," 2018 23rd Asia and South Pacific Design Automation Conference (ASP-DAC), Jeju, 2018, pp. 411-415.

 